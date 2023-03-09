**Lab3**

**Learning objective**: To create and use custom data types and type-classes

**Prerequisite**
1. Daml SDK installed and setup
2. Daml Fundamentals Training: Functional Programming in Daml - Lessons 1 to 8 completed.

## Problem statement 1
*This problem has two parts*

1. Create a data type called **Person** that has two fields - name and email - both of type Text. Make Person an instance of Show, Eq, and Ord. Then test it out using the following test script: 

    ```
    testPerson = script do 
        let 
            person1 = Person with 
                name = "Alice"
                email = "alice@earth.com"
        
            person2 = Person with 
                name = "Bob"
                email = "bob@earth.com"

        debug person1
        debug $ person1 == person2
        debug $ person1 < person2
        return ()
    ```

    The testPerson Script should yield the result shown below:

    ```
    Trace: 
    Person {name = "Alice", email = "alice@earth.com"}
    False
    True
    ```

2. Create a type class named **Reachable** that has a function named **reachOut**. Make the Person data type defined above an instance of Reachable. The reachOut function takes a record of Person type as an input and returns a text string that uses the Person's name and email. For example, if a Person record has name as "Alice" and email as "alice@earth.com", then reachOut function should return:

**"Hello Alice at alice@earth.com"**

Here is the script to test your code:
```
testReachable = script do
    let
        myFriend = Person with 
            name = "Alice"
            email = "alice@earth.com"

        message: Text =  reachOut myFriend

    debug $ message
```
And here is the expected output

```
Trace: 
  "Hello Alice at alice@earth.com"
```
