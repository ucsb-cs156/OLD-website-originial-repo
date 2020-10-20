---
topic: "Student: ex08"
desc: "Fixing up code coverage"
indent: true
code_repo: https://github.com/ucsb-cs156/student-tutorial
code_branch: ex09
---

# {{page.topic}} - {{page.desc}}

{% include student_tutorial_header.html %}

# Overview

In this example we show how to use the 
code coverage and mutation testing reports
to add missing tests.

# Starting where we left off

Let's start by running the mutation
testing report on the code in branch `ex08`

```
ucsb-cs156/student-tutorial % git checkout ex08
Already on 'ex08'
ucsb-cs156/student-tutorial % mvn test org.pitest:pitest-maven:mutationCoverage
...
=======================================================
- Statistics
=======================================================
>> Generated 10 mutations Killed 2 (20%)
>> Ran 2 tests (0.2 tests per mutation)
```

When we open up the reports (as we did in ex08) we
see that the line of code not covered in `Student.java` 
is the line for the `toString` method:

* Remember: the file to open up to see the reports is this one: <tt>target/pit-reports/<i>yyyymmddhhmmss</i>/index.html</tt> where <tt><i>yyyymmddhhmmss</i></tt> is a date/time stamp.

![student.java-50.png](student.java-50.png)

So, let's write a JUnit test for the `toString` method.

We'll add that to `StudentTest.java` which is located in the folder `src/test/java/edu/ucsb/cs156/student/`

Here's what the code looks like:

```java
 @Test
    public void test_toString1() {
        Student s = new Student();
        String expected = "[name: Sample Student, perm:9999999]";
        assertEquals(expected, s.toString());
    }
```

Note that we always start a JUnit test with `@Test`.  This is what marks the method as one that should be
run when we type `mvn test`.

The `assertEquals` method takes two parameters, the
first of which should be the expected value, and the
second of which should be the actual value computed
by the unit under test, in this case, the `toString` method.

With this test in place, the first thing to do is run
`mvn test` to ensure it compiles and passes:

On our first run, we get this:

```
Failed tests:   test_toString1(edu.ucsb.cs156.student.StudentTest): expected:<...ample Student, perm:[]9999999]> but was:<...ample Student, perm:[ ]9999999]>
```

This tells us that we have an extra space in our *actual* output that wasn't there in the expected output.  We can adjust either the expected or the
actual output to match; we'll adjust the expected
output in this case.

We modify the test like this:

```java
String expected = "[name: Sample Student, perm: 9999999]";
```

We run again and get this:

```
Tests run: 4, Failures: 0, Errors: 0, Skipped: 0
```

Now we can run the mutation tests and see if we were successful.  We'll add `clean` to the line so that
we only have one pit report:

```
mvn clean test org.pitest:pitest-maven:mutationCoverage
```

The result is this:

```
>> Generated 10 mutations Killed 3 (30%)
>> Ran 3 tests (0.3 tests per mutation)
```

That's better than before.  And when we open up the file, we see that Student.java now has 100% test
coverage, while Main.java has 0% test coverage.

```
Breakdown by Class
Name          Line Coverage 	Mutation Coverage
Main.java       0%     0/17           0%   0/7
Student.java 	100%  11/11         100%   3/3
```

Now the question arises: should we write tests for this Main?

If we look at what this Main is doing, we can see that it's purposes were really only to:

1. Serve as an example of a class with a `main` method.
2. Serve as an example of how to pass command line parameters
3. Serve as an example of how to convert a `String` to an `int`
4. Provide a way of testing our `Studnet` class before we had JUnit testing set up.
