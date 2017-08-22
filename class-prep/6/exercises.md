---
title: Class 6 Prep Exercises
currentMenu: classes
---

1. In your `Student` class from the [exercises for class 5 prep](../5/exercises.html), update the code to reflect the constructor additions that were added in [Classes and Objects: Encapsulating Behavior](../../csharp4python/classes-and-objects-encapsulating-behavior/). Complete the implementations of `AddGrade` and `GetGradeLevel`. For the method `AddGrade`, you'll need to update the student's GPA. To do this, note that GPA is computed via the formula:
    ```nohighlight
    Gpa = (total quality score) / (total number of credits)
    ```
    The total quality score is the sum of the quality scores of all classes, and the quality score for a class is found by multiplying the point score (0.0-4.0) by the number of credits. For example, if a student received an A (worth 4 points) in a 3-credit course and a B (worth 3 points) in a 4-credit course, their quality score would be: 4.0 \* 3 + 3.0 \* 4 = 24. And their GPA would then be 24 / 7 = 3.43.

    To update the GPA, you'll need to update the quality score. You can compute the existing quality score by calculating `Gpa * NumberOfCredits`. Then update the quality score and `NumberOfCredits`, and compute the new GPA with the new numbers.

    In `GetGradeLevel` you will need to determine the level of the student based on the number of credits: freshman (0-29 credits), sophomore (30-59 credits), junior (60-89 credits), or senior (90+ credits).
1. Add custom `Equals()` and `ToString()` methods to the `Student` class.
2. Carry out the above two exercises for the `Course` class, which you started in the [exercises for class 5 prep](../5/exercises.html).
