# Functional Programming in Daml: Lab2

**Learning objective**: To use primitive and collection data types and functions associated with them to process data

**Prerequisite**
1. Daml SDK installed and setup
2. Daml Fundamentals Training: Functional Programming in Daml - Lessons 1 to 7 completed.

## Problem statement 1

*This problem has two parts*

There is a list of tuples provided to you as shown below: 

```
song = [("do", "a deer, a female deer"), ("re", "a drop of golden sun"), ("mi", "a name, I call myself"), ("fa", "a long long way to run")]
```

Each tuple has a note, e.g. 'do', and a meaning, 'a deer, a female deer'. 

1. **Without using any itertive functions** such as map, mapA, forA, etc., extract the notes and meanings into two separate lists and print them first in the given order, and then in the reverse order. 

    You can use lists, tuples, and functions associated with these data types. 

    *Yes, it will be annoying not being able to use iterative functions! But it will help you learn some basics of using variables and functions associated with lists and tuples in Daml.*

    A sample output is shown below:

    ```
    ["do","re","mi","fa"]
    ["a deer, a female deer","a drop of golden sun","a name, I call myself","a long long way to run"]
    ["fa","mi","re","do"]
    ["a long long way to run","a name, I call myself","a drop of golden sun","a deer, a female deer"]
    ```

2. Create a Map called **notesMap** from the song list defined above. Use notesMap to print the meaning of all notes one by one as shown below:

    ```
    Some "a deer, a female deer"
    Some "a drop of golden sun"
    Some "a name, I call myself"
    Some "a long long way to run"
    ```


## Problem statement 2

Write a function named **termFrequency** that takes a word and a string of words and returns the frequency of that word in the string. For example, 

```
debug $ termFrequency "long" "a long long way to run"
```
should print
```
0.3333333333
```

Hint: You may find the following functions useful:

Text functions
- [words](https://docs.daml.com/daml/stdlib/DA-Text.html#function-da-text-words-34636)

List functions
- [length](https://docs.daml.com/daml/stdlib/Prelude.html#function-da-internal-prelude-length-32819)
- [filter](https://docs.daml.com/daml/stdlib/Prelude.html#function-da-internal-prelude-filter-41317) 

Data type conversion
- [intToDecimal](https://docs.daml.com/daml/stdlib/Prelude.html#function-da-internal-prelude-inttodecimal-16628)
