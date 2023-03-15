**Lab3**

**Learning objective**: To apply ensure, assert, abort, and trace functions in templates

**Prerequisite**
1. Daml SDK installed and setup
2. Daml Fundamentals Training: Testing in Daml - Lessons 1 to 4 completed.

## Problem statement 1
*This problem has four parts*

1. Continuing with the CLP Application from the previous lab, modify the CLPAccount template to **ensure** that the customerID is at least 4 characters long. 

    The following test-script should fail because the customerId is less than 4 characters long.

    ```
    -- create test-data structure
    data CLPData = CLPData with 
        customer: Party 
        airline: Party 
        airlineServiceCid: ContractId AirlineService

    -- create function to allocate values to test-data structure
    setupCLPData: Text -> Text -> Script CLPData 
    setupCLPData t1 t2 = script do 
        customer <- allocateParty (t1)
        airline <- allocateParty (t2)
        airlineServiceCid <- submit airline do 
            createCmd AirlineService with 
                customer 
                airline
        
        return $ CLPData with 
            ..

    testScript1: Script () 
    testScript1 = do 
        clpData <- setupCLPData "Alice" "Epic"
        now <- getTime
        
        aliceApplicationCid <- submit clpData.customer do 
            exerciseCmd clpData.airlineServiceCid CreateBlankApplication 

        aliceApplicationCid <- submit clpData.customer do 
            exerciseCmd aliceApplicationCid SubmitApplication 
                with 
                    appCustomer = clpData.customer 
                    appAirline = clpData.airline
                    customerId = "123"   --this is less than 3 chars which will cause the failure
                    customerName = "Alice"
                    customerAddress = "ABC Main Street, NY"
                    customerEmail = "alice@wonderland.io"
                    customerPhone = "123-555-1234"
                    appTimeStamp = now 
                    customerDob = date 2000 Jan 10

        aliceAccountCid <- submit clpData.airline do 
            exerciseCmd aliceApplicationCid ReviewApplication 

        
        return ()
    ```

2. Modify the CLPApplication template as given below:

    - use  **assertMsg** function in the **ReviewApplication** choice with a message "Assertion:Failure Duplicate customer Id" if the airline finds another account with same customer Id. 


    With this change, run the testScript2 given below. It should fail with the message: 

    ```
    Script execution failed on commit at TestLab3:85:24:
    Unhandled exception:  DA.Exception.AssertionFailed:AssertionFailed@3f4deaf145a15cdcfa762c058005e2edb9baa75bb7f95a4f8f6f937378e86415 with
        message = "Assertion failure: Duplicate customer Id"
    ```

    ```
    testScript2: Script () 
    testScript2 = do 
        customer1 <- allocateParty ("Alice")
        customer2 <- allocateParty ("Bob")
        airline <- allocateParty ("Epic")

        airlineServiceCid <- submit airline do 
            createCmd AirlineService with 
                customer = customer1
                airline

        now <- getTime

        aliceApplicationCid <- submit customer1 do 
            exerciseCmd airlineServiceCid CreateBlankApplication 

        aliceApplicationCid <- submit customer1 do 
            exerciseCmd aliceApplicationCid SubmitApplication 
                with 
                    appCustomer = customer1 
                    appAirline = airline
                    customerId = "1234"
                    customerName = "Alice"
                    customerAddress = "ABC Main Street, NY"
                    customerEmail = "alice@wonderland.io"
                    customerPhone = "123-555-1234"
                    appTimeStamp = now 
                    customerDob = date 2000 Jan 10

        aliceAccountCid <- submit airline do 
            exerciseCmd aliceApplicationCid ReviewApplication 

        airlineServiceCid <- submit airline do 
            createCmd AirlineService with 
                customer = customer2
                airline

        bobApplicationCid <- submit customer2 do 
            exerciseCmd airlineServiceCid CreateBlankApplication 

        bobApplicationCid <- submit customer2 do 
            exerciseCmd bobApplicationCid SubmitApplication 
                with 
                    appCustomer = customer2 
                    appAirline = airline
                    customerId = "1234"
                    customerName = "Bob"
                    customerAddress = "XYZC Main Street, NY"
                    customerEmail = "bob@nomansland.io"
                    customerPhone = "123-555-5678"
                    appTimeStamp = now 
                    customerDob = date 2000 Jul 10

        bobAccountCid <- submit airline do 
            exerciseCmd bobApplicationCid ReviewApplication 


        return ()
    ```

3. Comment out the assertion from the template, and now write an **abort** statement in the ReviewApplication choice so that when there is an account with the same Id, then the script should abort with a message "Aborting: Duplicate customer Id"

    The error message should look something like this:

    ```
    Script execution failed on commit at TestLab3:109:22:
    Unhandled exception:  DA.Exception.GeneralError:GeneralError@86828b9843465f419db1ef8a8ee741d1eef645df02375ebf509cdc8c3ddd16cb with
                            message = "Aborting: Duplicate customer ID"
    ```


4. Comment out the abort statement from the template, and now write two **trace** statements so that:
- when the application finds a duplicate id, it prints "Duplicate id. Application rejected" and returns nothing.
- when the application does not find a duplicate, it prints "Creating account" and then creates the account.

    Given the scenario in testScript2 above where Alice's account is successfully created while Bob's application is rejected because of duplicate id, the Trace should show the following two print statements:

    ```
    Trace: 
    "Creating account"
    "Duplicate id. Application rejected"
    ```