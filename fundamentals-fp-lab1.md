# Functional Programming in Daml: Lab1

**Learning objective**: To write and test a function in Daml

**Prerequisite**
1. Daml SDK installed and setup
2. Daml Fundamentals Training: Functional Programming in Daml - Lessons 1 to 5 completed.

## Problem statement 1

*This problem has three parts.*

1. Write a function named **quadFunction** that takes three integers for x, y, and z. It returns the value of

   ![quadEquation](fundamentals-fp-lab1-equation.png)


2. Write a test-script that 

- Tests **quadFunction** as

    ```
        quadFunction 1 2 3
    ```

- Prints the result in the Script output as shown below:


    ```
        Transactions: 

        Active contracts: 

        Return value: {}

        Trace: 
        10

    ```

3. Write a **lambda function** in the test script that does the same calculation as the quadFunction described above and prints the same result as shown above. 


## Problem statement 2
*This problem is adapted from [Learn You a Haskell for Great Good!](http://learnyouahaskell.com/starting-out#babys-first-functions)*

*This problem has three parts*

1. Write a function named **doubleMe** that takes an integer and returns its double 
2. Using the **doubleMe** function, write another function called **doubleUs** that takes two integers, doubles each of them, adds them up and returns the result.

    As a sample, the following statements: 

    ```
        debug $ doubleMe 3
        debug $ doubleUs 3 4
    ```

    will produce the following result:

    ```
    Transactions: 

    Active contracts: 

    Return value: {}

    Trace: 
    6
    14
    ```

3. Write an expression in the test-script using **doubleUs** with an **inFix notation** to get the same result as 

    ```
    debug $ doubleUs 3 4
    ```
