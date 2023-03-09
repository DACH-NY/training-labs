**Lab4**

**Learning objective**: To use conditional control flow statements to manage the program's logical flow

**Prerequisite**
1. Daml SDK installed and setup
2. Daml Fundamentals Training: Functional Programming in Daml - Lessons 1 to 9 completed.

## Problem statement 1
*This problem is based on the Lesson: Conditional control flow*

A University has the following grading-scheme based on scores out of 100 points. 

| Score            | Letter grade |
|------------------|------------- |
| 90.0 or above      | A            |
| from 80.0 to less than or equal to 90.0         | B            |
| from 70.0 to less that or equal to 80.0         | C            |
| Less than 70.0     | F            |


Write four functions as specified below:


| Function            | Specification |
|------------------|------------- |
| ``` getLetterGradeUsingIf: Decimal -> Text ```| takes a score and returns its corresponding letter grade. It uses if-then-else.            |
| ```getScoreUsingCase: Text -> Text```         | takes a letter-grade and returns a range of score. It uses case-statements            |
| ```getLetterGradeUsingGuards: Decimal -> Text``` | takes a score and returns its corresponding letter grade. it uses Guards            |
| ```getAverageGradeLetter: Decimal -> Decimal -> Text```     | takes two scores and returns the letter-grade corresponding to their average. Uses Guards with 'where' to compute average            |


Use the following script to test your functions: 
```

testGrades = script do 
    
    debug $ getLetterGradeUsingIf 90.0
    debug $ getLetterGradeUsingIf 85.0
    debug $ getLetterGradeUsingIf 75.0
    debug $ getLetterGradeUsingIf 65.00
    debug "----------"
    debug $ getScoreUsingCase "A"
    debug $ getScoreUsingCase "B"
    debug $ getScoreUsingCase "C"
    debug $ getScoreUsingCase "F"
    debug $ getScoreUsingCase "X"
    debug "----------"
    debug $ getLetterGradeUsingGuards 90.0
    debug $ getLetterGradeUsingGuards 80.0
    debug $ getLetterGradeUsingGuards 70.0
    debug $ getLetterGradeUsingGuards 60.0
    debug "----------"
    debug $ getAverageGradeLetter 75.0 83.0
    debug $ getAverageGradeLetter 95.0 83.0
    debug $ getAverageGradeLetter 98.0 83.0
    debug $ getAverageGradeLetter 60.0 70.0

    return()
```

If everything works correctly, the output should look like as shown below: 

```
Trace: 
  "A"
  "B"
  "C"
  "F"
  "----------"
  "Score 90+"
  "80 to 90"
  "70 to 80"
  "less than 70"
  "Invalid grade letter"
  "----------"
  "A"
  "B"
  "C"
  "D"
  "----------"
  "C"
  "B"
  "A"
  "F"
```
# Problem Statement 2

Write a function named **triangleArea** that calculates the area of a triangle. It takes a list as an input that has the lengths of three sides of a triangle. It returns a value depending on the four scenarios given below:

| Scenario            | Return value |
|------------------|------------- |
| 1. If the length of the list is less or more than 3      | an error message **Error: Triangle has 3 sides**            |
| 2. If any of the three sizes is 0         | an error message **Error: Side of a triangle cannot be 0.0**            |
| 3. If any side is greater than the sum of the other two         | an error message **Error: This can't be a triangle as per Triangle Inequality Theorem: a + b >= c**            |
| 4. All valid inputs     | Triangle area =   &Sqrt; ( s * (s-a)  * (s-b) * (s-c) / 2 )     where s = (a + b + c)/2   |


Here is the script to test your function:

```
testTriangle = script do 

    debug $ triangleArea [4.0, 2.0, 5.0]
    debug $ triangleArea [1.0, 2.0, 3.0]
    debug $ triangleArea [1.0, 2.0]
    debug $ triangleArea [1.0, 2.0, 0.0]

    return ()
```
And here is the expected script output:

```
Trace: 
  Right 3.7996710379
  Left "Error: This can't be a triangle as per Triangle Inequality Theorem: a + b >= c"
  Left "Error: Triangle has 3 sides"
  Left "Error: Side of a triangle cannot be 0.0"
```

Hints: 
1. As evident from the output, you need to use Either in the return type of triangleArea function.
2. You may find list functions (e.g. head, tail, maximum, sum, etc.) useful when checking for the scenarios.
3. It may help to create another helper function to calculate the area when the inputs are valid. 




