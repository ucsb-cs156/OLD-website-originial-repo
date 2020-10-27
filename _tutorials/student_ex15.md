---
topic: "Student: ex15"
desc: "Sorting with Comparators, and introduction to Lambda expressions"
indent: true
code_repo: https://github.com/ucsb-cs156/student-tutorial
code_branch: ex15
---

In ex14, we looked at implementing the `java.lang.Comparable<T>` interface.  This allows us to define what Java calls a *natural order* for a class.   

If you have an `ArrayList<Foo> myarray;` for any class `Foo` that implements the `java.lang.Comparable<Foo>` interface, you can sort that array  can be sorted by simply invoking `myarray.sort();`.    

However, the limitation of the `Comparable<T>` method is that you can only define *one way* to sort a particular class.  For example, if we define sorting by perm, ascending, as the *natural order* for `Student`, then `myarray.sort()` will only every sort in this specific order.

In ex15, we'll look at a more flexible way to define sort orders using something called a `java.util.Comparator<T>`.  This is a special object that, as the saying goes *has one job*.  That job is to define a way of comparing two objects of type `T`.    Each `Comparator` can be defined to sort by a different field; for example:

* One Comparator might sort by perm, ascending.
* Another Comparator might sort by name, in alphabetical order
* Another Comparator might sort (if we add `gpa` to the Student object) by GPA descending.

Consider also, a `Course` object that might have attributes `department`, and `course number` and `section number`.  We might make a single comparator that sorts first by department, then by course number, and finally by section number.

In this exercise

* We'll look at the `java.util.Comparator<T>` interface
* We'll discuss how it differs from `java.lang.Comparable<T>`
* We'll look at various ways of implementing a Comparator:
  * As a separate named class
  * As a named inner class
  * As a "defined on the fly" instance of a class
  * As a lambda expression
