---
topic: "Student: ex01"
desc: "private data members, public constructors, integers from command line arguments, main methods, built in toString method, simple compilation/execution with javac/java"
indent: true
code_repo: https://github.com/ucsb-cs156/student-tutorial
code_branch: ex01
---


<style>
div.niceTable table {
   border-collapse: collapse;
}


div.niceTable table * td {
   border: 1px solid black;
   border-collapse: collapse;
}
  
div.niceTable table * td:first-child {
   font-family: monospace;
   white-space: pre;
}
  
  
div.niceTable table * th {
   border: 1px solid black;
   border-collapse: collapse;
}
  
</style>

# student-tutorial/ex01

{% include student_example_header.html %}

# Overview

In this first article, we will first explain what the `Student` class is supposed to do, i.e. provide an abstraction for a UCSB Student   

We'll then show some Java code with two classes: starter code for a `Student` class, and a driver class 

The code will be presented in a repository of source code ("repo") for short that is stored using the `git` version control system, a free and open source software package for version control. 

This `git` repo is hosted as open source on [github.com](https://github.com), a commerical company (acquired by Microsoft in 2018) that provides cloud-based hosting for `git` repositories, plus other web-based tools for software development.

This lesson will not include a full discussion of git/github&mdash;just the briefest overview of the minimal information needed to make use of the code in this repo.

## `Student.java`: starter code for a Java class

The starting point `Student` class that has the minimum we need to get started, mostly in "stub" form:

* private instance variables for `name` and `perm`

* a default constructor, `Student()`, that takes no arguments, and
  creates an instance of class `Student`.  We'll assume that this
  creates an instance of `Student` with the name `Sample Student`
  and the perm `9999999`

* a constructor that takes arguments for `name` and `perm`

* code to get values for those arguments from the command line, and pass them to the constructor. 

* code that prints out these values using the `toString()` method of the class `Object`

We'll see that the built in `toString()` method is not of much use.  In the next
example, we'll override it to make something more useful.  (Note on overriding: See https://ucsb-cs`56.github.io/topics/java_overriding_vs_overloading/ )

## `Main.java`: a sample "driver" class

We'll also provide Java code for a "driver" class with a`main` method&mdash;one that illustrates how to invoke the constructor for the `Student` class, and then invoke one or more of the methods of the object instance.

That main class will illustrate how to get simple integer parameters from the command line via the `args` parameter to main (the equivalent of `argc`/`argv` in C/C++).


# Basic description of the Student class

The Student class provides an abstraction for a UCSB Student.


This tutorial will not try to motivate *why* we need a class for UCSB Students.   We will assume that there is some need to represent these in a program.   We'll assume that once some Java code has gotten input from somewhere for the names and perms of a student, it needs to

* Construct objects that represent these students
* Do some computation over those objects (e.g. computing the average GPA,
  sorting a collection of students by GPA, etc.).

  We acknowledge that
  in this chapter of the tutorial, with fields only for
  name and perm, there aren't
  many interesting computations we can do yet, but we'll be adding additional
  fields as we proceed through the chapters in the tutorial.
  
We'll assume, for now, that instances of the class are immutable, i.e. we provide a way to construct objects, and getters for name and perm, but no setters for name and perm.   We may change this assumption at some point in the tutorial.

# Accessing the code from the github repo

The example code that supports this lesson is in a repository ("repo" for short) at this link.  Note that this link is showing the branch <tt>{{page.code_branch}}</tt>, *not* the <tt>main</tt> branch of the repo.

* <{{page.code_repo}}/tree/{{page.code_branch}}>

A detailed discussion of git and github is a topic for a different tutorial; for this lesson, we'll just go over the minimal 
information you need to get started with the code.  

* You can browse the code, as well as downloading it all in a .zip file at the link shown above.
* On a system where `git` is installed (such as [CSIL](/topics/CSIL/), you can use this command to create a copy of the repository that has a link back to the original so that you can pull updates at any time:
   
   * <tt>git clone {{page.code_repo}}.git</tt>

That will create a subdirectory containing the contents of the repo; `cd` into it and you can start working with the code.

For more detail, consult these articles: [git](/topics/git/), [github](/topics/github).

# What are each of the files?

Here's a brief over view of each of the files in the repo, and their purpose.



<div class="niceTable" markdown="1">  

| Filename | Purpose |
|-|-|
| .gitignore	| Tells `git` which files should be ignored when updating the repo (e.g. temporary files, executable files). | 
| LICENSE	| Open Source repos often have a license in them that specifies the copyright and any restrictions placed on how the code may be used. | 
| Main.java | Java code for driver program; a class containing a `main` method. |
| README.md	| A file that describes the contents of the repo.  The `.md` extension indicates that this is a [Markdown](/topics/markdown/) file.   Markdown is a format that allows us to create web content; it is similar to HTML, but has a simplified syntax.   | 
| Student.java | A file that defines a `Student` class.

</div>

# Simple compiling and executing with `javac` and `java` commands:

The following summary shows compiling and running the simplest possible way
at a `bash` command line using plain old `javac` and `java`:

```bash
ucsb-cs156/student-ex01 % ls
LICENSE		Main.java	README.md	Student.java
ucsb-cs156/student-ex01 % javac Main.java
ucsb-cs156/student-ex01 % ls
LICENSE		Main.java	Student.class
Main.class	README.md	Student.java
ucsb-cs156/student-ex01 % java Main
Usage: java Main name perm
  perm should be a positive integer between 1 and 9999999
ucsb-cs156/student-ex01 % java Main Chris 1234567
s1 = Student@38cccef
s2 = Student@64b8f8f4
ucsb-cs156/student-ex01 % 
```

A few things to note:
* When we compile `Main.java`, since it refers to class `Student`, that
  file automatically gets compiled to.
* The compiled code goes into a file called `Main.class` and `Student.class`
* We can only *run* a class that contains a `main` method.
* We do not specify the `.class` extension when running.
* We instead, specify the name of the class.
* The `Rational.class` and `Main.class` files remain separate.

    * There is no "linking" phase as in C++/C that combines them into a single program
    * There is a way to combine multiple `.class` files into a single `.jar` file, but this is
        not the same as linking, as explained [here](https://ucsb-cs156.github.io/topics/java_jars/)
        
* When we write `System.out.println("s1 = " + s1);` we are trying to do string concatentation on two instances
  of the class `java.lang.String`.   Since `s1` is a reference to an instance of class `String`, it can't
  be concatenated to a String.  In this case, the JVM will try to invoke a `toString()` method on the
  object to convert it to a String.
* The `toString()` method that gets invoked here is actually part of the class `java.lang.Object`

# Every class (directly or indirectly) `extends Object`

When we write `public class Foo extends Bar {` it signifies that Bar
is the parent class of Foo, i.e. the Foo inherits from Bar.

If we write just `public class Foo`, unlike in C++ where that would
signify that Foo has no parent class, in Java, any time we write this,
it is the same as writing `public class Foo extends java.lang.Object`.

Notes:

* Classes that start with `java.lang.` are part of the Java Language.
* That includes `java.lang.String` and `java.lang.Object`, just to name a couple.
* We don't have to write `java.lang.Object`; for any class that is part of the `java.lang.` package, we can leave off the `java.lang.` prefix, and just write `Object`.


One implication of this is that nearly every instance of every class in Java
has a `public String toString()` method, because:

* If it doesn't have its own, it inherits one.
* It may inherit one from its parent class, grandparent class, great-grandparent class, etc.
* But in the limit, if none of those classes have one, there will always be one in java.lang.Object.
* Ok, there are bizarre corner cases where someone deliberately tries to mess this up, 
    say by declaring a private toString() method and making it inaccessible to us.  But mostly, you can rely on there being one.

The thing is, the toString() method we inherit from java.lang.String is seldom what we want.

For example, in the output above, we see that the output of:

```java
        System.out.println("s1 = " + s1); // implicit: r1.toString()
        System.out.println("s2 = " + s2); // implicit: r2.toString()
```

Is this:

```
s1 = Student@38cccef
s2 = Student@64b8f8f4
```

To fix this, we need to override the toString method.  We'll do this
in the next article, [Student: ex02](/tutorials/student_ex02/)

<div class="github-preview-only">On website: https://ucsb-cs156.github.io/tutorials/student_ex01/</div>
