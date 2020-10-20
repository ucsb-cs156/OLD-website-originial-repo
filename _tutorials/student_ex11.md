---
topic: "Student: ex11"
desc: "More on Exceptions, static methods"
indent: true
code_repo: https://github.com/ucsb-cs156/student-tutorial
code_branch: ex11
---

# {{page.topic}} - {{page.desc}}

{% include student_tutorial_header.html %}

# Overview

In this example we show how to write a static method
to compute the

[Luhn Checksum](https://en.wikipedia.org/wiki/Luhn_algorithm)) and how to test it.

We first should write some tests.  For that we can
do the calculation by hand on a few six digit perms:

Take `123456`.  Applying the [Luhn algorithm](https://en.wikipedia.org/wiki/Luhn_algorithm), we get:
 
```
1 + 2x2 + 3 + 4x2 + 5 + 6x2 =
1 +  4  + 3 +  8  + 5 + 12  =  33
```

To get to a number divisble by 10, we need to add 7,
so the check digit is 7: `1234567`

For another example, consider: `111111`

```
1 + 1x2 + 1 + 1x2 + 1 + 1x2 = 
1 +  2  + 1 +  2 +  1 +  2  = 9
```

To get to a number divisible by 10, we need to add 1,
so the check digit is 1: `1111111`.

With this in mind, we now have at least two test cases
for computing check digits over six digit numbers.

So, we can write some test cases for a utility method
that we'll put into its own class called `Luhn.java`.

* We'll write a stub for it first
* Then we'll write some tests
* Finally we'll write an implementation
* Then we'll check the mutations testing.





  