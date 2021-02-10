---
topic: "Student: ex16"
desc: "Sorting"
indent: true
code_repo: https://github.com/ucsb-cs156/student-tutorial
code_branch: ex16
---

Code for this exercise: <https://github.com/ucsb-cs156/student-tutorial/tree/ex16>

In the previous exercise, we looked a sorting by name using a simple `java.util.Comparator<Student>`, implemented as a separate named class.

Our `Student` class is kind of boring at the moment; it just has `name` and `perm`; and we've already built ways to sort on both of those.

To make it more interesting, so that we can look at more exotic ways of sorting, we'll first do some updating to the `Student` class itself.

In ex16, we'll:
* split `name` into `first` and `last`
* add `units` as another field

Since these are pretty straightforward modifications, we'll let the code speak for itself; there isn't much else to say.

We will note that we only partially refactored the test coverage; finishing that job is left as a future exercise.

With `name` split into `first` and `last`, and the addition of `units`, we now have four things to sort on (including `perm`), so we
are well prepared for ex17.
