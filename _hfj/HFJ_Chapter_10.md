---
title: Head First Java, 2nd Edition
chapter: 10
sort_key: "10"
textbook: HFJ
desc:  "Numbers Matter"
---


# Chapter 10: Numbers Matter


# The big picture (p. 273)

The title of the Chapter is "Numbers Matter", and from that you might get the idea that the chapter is all about numeric stuff.

That's not the whole story. The chapter uses the fact that most of the methods of java.lang.Math are static to talk about static methods, as well as the final keyword.

The chapter then takes a detour in to the wrapper objects: Boolean, Character, Byte, Short, Integer, Long, Float and Double, as well as talking about number formatting (the printf type stuff that got added in Java 5.0).

Finally, the Chapter goes off on a real tangent and talks about working with Dates (java.util.Calendar)

So in addition to learning how to do sine, cosine, etc, you'll see a few other things:

* A case where you'd want to make the constructor for a class private
* The difference between static and non-static methods
* What the wrapper objects are for
* Autoboxing and unboxing of primitives
* How to format numbers
* How to work with dates

# Chapter 10, page-by-page

# page 274-275: How to do sin, cos, etc. and what static means

So, take a look at the javadoc for the `java.lang.Math` class:

* <http://download.oracle.com/javase/6/docs/api/java/lang/Math.html>

You'll see that it has the usual stuff that you'd find in `#include <math.h>` in C, or `#include <cmath>` in C++: `E`, `PI`, `sin`, `cos`, etc.

Because the class `Math` is in the `java.lang package` (just like `java.lang.String` is), you don't have to do any import to get access to Math methods—you can just use them, like this:

```java
// http://www.cs.ucsb.edu/~pconrad/cs56/textbooks/hfj2e/code/ch10/p274/MathDemo.java

public class MathDemo {

    public static void main (String [] args) {
	System.out.println("Math.round(42.2)     ="+Math.round(42.2) );
	System.out.println("Math.min(56,12)      ="+Math.min(56,12)  );
	System.out.println("Math.abs(-343)       ="+Math.abs(-343)   );
	System.out.println("Math.E               ="+Math.E             );
	System.out.println("Math.PI              ="+Math.PI            );
	System.out.println("Math.sin(Math.PI/2)  ="+Math.sin(Math.PI/2));
	System.out.println("Math.cos(Math.PI/2)  ="+Math.cos(Math.PI/2));
    }
}
```

Sample output:

```
-bash-4.1$ java MathDemo 
Math.round(42.2)     =42
Math.min(56,12)      =12
Math.abs(-343)       =343
Math.E               =2.718281828459045
Math.PI              =3.141592653589793
Math.sin(Math.PI/2)  =1.0
Math.cos(Math.PI/2)  =6.123233995736766E-17
-bash-4.1$ 
```

The bigger concept on this page though is the idea that the `java.lang.Math` class is one for which we can never create an instance. The class exists only for the purpose of being a place for its static methods to have a place to live.

Static methods (or variables) are methods (or variables) that are not associated with an instance of the class, but with the class itself.

There is only one instance of any given static method, and it is accessed not through an instance of the class, but through the class name. (This is pretty similar to how it works in C++.)

So, this is an example of a case where you might make the constructor for the class private.

## Potential Exam Questions

Here's an exam/homework question for which the answer is not (necessarily) spelled out for you in the book—it may require some "higher-order thinking".

On page 274 (On Campus Off Campus) we see that the constructor for the `Math` class is private.

For this question, you are being asked to "defend" the decision to make the constructor private. Explain what you think the rationale is for making the constructor private. In your explanation, be specific about what the situation would be if the constructor were NOT private, and someone were able to create an instance of the java.lang.Math class, and why making it private might be perceived as a better design choice.

# page 276-277: More on static methods

So, here are some questions about the material on these two pages:

## Potential Exam Questions

* Does it ever make sense to both static and non-static methods in the same class?
* If so, does it ever make sense to create an instance of such a class?
* Does it ever make sense to have all static methods in a class?
* If so, does it ever make sense to create an instance of such a class?
* Does it ever make sense to have all non-static methods in a class?
* If so, does it ever make sense to create an instance of such a class?
* Is it possible to invoke a non-static method of class Foo without an instance of class Foo?
* Is it possible to invoke a static method of class Foo without creating an instance of class Foo?


A question that may require "higher order thinking"...

The `Math` class has only static methods, and is not meant to be instantiated. The designers of that class enforced this by making its constructor private. Another way to make `Math` be a class that you can't make an instance of would be to make it an `abstract` class (see Chapter 8). Although that would achieve the goal of making it so that Math can't be instantiated, there's something not quite right about that approach—what is it that doesn't quite make sense about making `Math` an abstract class?

<!--
## page 278-281: More on static variables
## page 282-283: the final keyword
## page 284-285
## page 286
## page 287-291: Wrappers and autoboxing/unboxing of primitives
## page 292-293: Converting between strings and numbers
## page 294-300: Number formatting (printf type stuff in Java)
## page 300-306: Dates and java.util.Calendar
## page 307: static import (use with caution)
## page 308-309: Fireside chat: review of instance vs. static variables
## page 310-314: Exercises
-->
