# Lab5

**Learning objective**: To control program flow using iterative functions.

**Prerequisite**
1. Daml SDK installed and setup
2. Daml Fundamentals Training: Functional Programming in Daml - Lessons 1 to 10 completed.

## Problem statement 1

There is a list of tuples provided to you as shown below: 

```
song = [("do", "a deer, a female deer"), ("re", "a drop of golden sun"), ("mi", "a name, I call myself"), ("fa", "a long long way to run")]
```

Each tuple has a note, e.g. 'do', and a meaning, 'a deer, a female deer'. 

Given this data, write a script to extract the notes and meanings into two separate lists and print them first in the given order. 

A sample output is as shown below:

```
Trace: 
  ["do","re","mi","fa"]
  ["a deer, a female deer","a drop of golden sun","a name, I call myself","a long long way to run"]
```

Hint:
- You may find [map](https://docs.daml.com/search.html?query=map) function useful


## Problem statement 2

*This problem has two parts*

1. Using the [map](https://docs.daml.com/search.html?query=map) function, write a function named **multiTermFrequency** that takes a Text, say x, and a list of Texts, say y, as input. It then returns a list of numbers with each number at index i representing the frequency of x in the i-th element in y. 

    Here is a script to test your function:

    ```
    testMultiTermFrequency = script do 
        let x = "hello"
        let y = [ "hello from the other side I must have called a thousand times", 
                "You say goodbye and I say hello hello hello",
                "hello is it me you’re looking for",
                "hello hello is anyone home"
                ]

        debug $ multiTermFrequency x y
        return()
    ```

    It should produce the following output:

    
    ```
    Trace: 
    [0.0833333333,0.3333333333,0.1428571429,0.4]
    ```



2. Write the same function as above using **[foldr](https://docs.daml.com/search.html?query=foldr)** instead of map function

**Hint**:
- If you did [Lab2](https://github.com/neelamdwivedi-da/associate-labs/blob/main/Lab2.md) where you wrote a function named **termFrequency**, then you should be able to reuse it here. 
