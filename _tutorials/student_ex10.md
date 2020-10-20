---
topic: "Student: ex10"
desc: "Exceptions"
indent: true
code_repo: https://github.com/ucsb-cs156/student-tutorial
code_branch: ex10
---

# {{page.topic}} - {{page.desc}}

{% include student_tutorial_header.html %}

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

```java
@Test(expected = IllegalArgumentException.class)
    public void test_constructor_zeroPerm() {
        Student s = new Student("Test",0);
    }

    @Test(expected = IllegalArgumentException.class)
    public void test_constructor_negPerm() {
        Student s = new Student("Test",-1);
    }

    @Test(expected = IllegalArgumentException.class)
    public void test_constructor_tooBigPerm() {
        Student s = new Student("Test",10000000);
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
