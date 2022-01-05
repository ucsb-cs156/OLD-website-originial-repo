---
topic: "Student: ex10"
desc: "Exceptions"
indent: true
code_repo: https://github.com/ucsb-cs156/student-tutorial
code_branch: ex10
---

# {{page.topic}} - {{page.desc}}

{% include student_tutorial_header.html %}

# NOTE: NOT YET UPDATED FOR JAVA 17 and JUNIT 5 (TODO for W22, 01/05/22)

# Overview

In this example we show how to use exceptions
to add error checking to inputs.  

The only two data values we have so far are
`name` and `perm`.  Since names can take a variety
of forms, we'll focus our attention on `perm`.

A `perm` number should be a positive integer between
1 and 9999999 (i.e. any seven digit number other than 0).  Furthermore, a perm can take either
a six digit form, or a seven digit form; if it has
a seven digit form, the last digit is a check digit (we think, produced by the [Luhn Algorithm](https://en.wikipedia.org/wiki/Luhn_algorithm)).


So we may want to prevent a `Student` object from being produced with an invalid perm.

We'll start by defining the desired behavior with some test cases.  Each test case name is something that
describes the behavior we expect.  In the cases
where the perm number passed in is not acceptable,
we will expect the code to throw an `IllegalArgumentException`.  

Note: If you are not familiar with exceptions,
you may find it helpful to do some reading
in the textbook(s):
* HFJ2 Chapter 11 covers Exceptions
* pp. 75-77 in Chapter 2 of JN7 also cover Exceptions

Here's how we write a test for an expected exception.  We'll need to unpack this a bit, since it introduces a few elements of Java syntax that aren't in our Head First Java textbook (though they are in the JN7 textbook) and that you may not have seen before, namely:

* the `IllegalArgumentException.class` expression
* the lambda expression: `() -> { }`

First, here's the whole test.  Then we'll unpack it a little at a time:

```java
    @Test
    public void test_constructor_zeroPerm() {
        assertThrows( IllegalArgumentException.class, () -> {
                Student s = new Student("Test",0);
        });
    }
```

So let's start by looking just at just the `assertThrows` method.

It takes two parameters.  
* The first is `IllegalArgumentException.class`.  This is an instance of the `java.lang.Class<T>` class [documented here](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Class.html).   That is, the expression `IllegalArgumentException.class` refers to a Java Object that respresents the class `IllegalArgumentException`, and has methods such as `getMethods()`, `getFields()`, etc.
* The second is the entire expression:
  
  ```
  () -> {
     Student s = new Student("Test",0);
  }
  ```
 
  This is a so-called Lambda Expression, and is a way of representing a Java function(method) that can be called with no parameters (hence the empty `()`), and the body of the method is the part in `{}`.
  
  A lambda expression allows us, among other things, to pass a block of code as a parameter to a function.  In this case the type of the parameter is `org.junit.jupiter.api.Executable` documented [here]() that that isn't really important to understand at this point.  Later in the course, we'll come back and talk much more about lambda expressions, and their relationship to Java Interfaces, and specifically a kind of interface called a "functional interface".
  
For now, it's enough to know this:

* When you want to test whether some code throws an exception in a JUnit test, use `assertThrows`
* Pass the name of the expected exception followed by `.class` as the first parameter
* For the second parameter, write `() -> { codeGoesHere(); }` where `codeGoesHere();` can be as much Java code
  as you need to generate the exception.



Here are the rest of the tests that we introduce in this version:

```
    @Test
    public void test_constructor_negPerm() {
        assertThrows( IllegalArgumentException.class, () -> {
            Student s = new Student("Test",-1);
        });
    }

    @Test
    public void test_constructor_tooBigPerm() {
        assertThrows( IllegalArgumentException.class, () -> {
            Student s = new Student("Test",10000000);
        });
    }

    @Test
    public void test_constructor_perm_1_ok() {
        Student s = new Student("Test",1);
        assertEquals(1,s.getPerm());
    }

    @Test
    public void test_constructor_perm_9999999_ok() {
        Student s = new Student("Test",9999999);
        assertEquals(9999999,s.getPerm());
    }
```

We add these tests, and we get some test failures, as we expected:

```
Failed tests:   test_constructor_tooBigPerm(edu.ucsb.cs156.student.StudentTest): Expected exception: java.lang.IllegalArgumentException
  test_constructor_negPerm(edu.ucsb.cs156.student.StudentTest): Expected exception: java.lang.IllegalArgumentException
  test_constructor_zeroPerm(edu.ucsb.cs156.student.StudentTest): Expected exception: java.lang.IllegalArgumentException

Tests run: 9, Failures: 3, Errors: 0, Skipped: 0
```

So now we set about making the tests pass.

Here is the new version of our constructor:

```java
   public Student(String name, int perm) {

        if (perm < 1 || perm > 9999999) {
            throw new IllegalArgumentException("Unacceptable value for perm: " + perm);
        }

        this.name = name;
        this.perm = perm;
   }
```

We see with this than `mvn test` produces no errors:

```
Results :

Tests run: 9, Failures: 0, Errors: 0, Skipped: 0
```

Further, we check the mutation test coverage:

```
ucsb-cs156/student-tutorial % mvn clean test org.pitest:pitest-maven:mutationCoverage
...
>> Generated 7 mutations Killed 7 (100%)
>> Ran 10 tests (1.43 tests per mutation)
```

So, that's a win.  But how about that check digit?

We'll tackle that in ex11.
