---
topic: "git: fixup commit"
desc: "Fixing an error you made in a previous commit"
indent: true
category_prefix: "git: "
---


See also, this video: <https://youtu.be/sgW9_D0vK5A>

Inevitably, you discover as you work in a feature branch, that you made a mistake in an earlier commit.

Of course you can just fix it with a new commit, but then you end up with a commit history like this:

```
0a89f pc - add students controller to support CRUD operations for students
34s9c pc - add front end React form component for student CRUD operations
3240a pc - fix spelling error in parameter name in students controller
7bd40 pc - add yet another missing HTTP header in controller
d0240 pc - add missing HTTP header in students controller
```

The last three commits are just fixing errors that are in the controller; the new file added in the first commit.

And those commits are now separated from the original commit by one dealing with a React form; an entirely separate concern.

Wouldn't it be nice if you just fix up the original commit?  Now you can.

The technique is explained in:
* This video by P. Conrad: <https://youtu.be/sgW9_D0vK5A>
* This web page by Florent Lebreton <https://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html>

But here's the short version:

