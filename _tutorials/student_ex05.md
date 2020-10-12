---
topic: "Student: ex05"
desc: "Setting up GitHub Actions"
indent: true
code_repo: https://github.com/ucsb-cs156/student-tutorial
code_branch: ex05
---

# {{page.topic}} - {{page.desc}}

{% include student_tutorial_header.html %}

# Overview

In this example we introduce GitHub Actions to 
run JUnit tests.

GitHub Actions is a platform for "continuous integration" of our
code, i.e. automatically testing our *entire code base* after every commit

Continuous Integration (CI) is an industry standard practice for professional software development.   It’s called Continuous Integration because:

* It’s *Continuous*: you do it as you push commits into your branch
* It’s an Integration: you are looking at the impact of 
  your    changes not just on the parts of the code base you think you are impacting, but on the entire code base as an integral whole.

You can read more about CI systems here: <https://ucsb-cs156.github.io/topics/ci/>

To set up GitHub Actions for any repo, we take two steps:
* Create a directory called `.github/workflows`.  
  - To create it, we can type `mkdir -p .github/workflows`
  - Note that
    because the directory name `.github` starts with a `.`, it
    will be a hidden directory on many systems.

    On Unix, you use `ls -a` to show hidden files/directories.

* Into the directory `.github/workflows`, we put a file
  that specifies the actions to be taken, using a syntax
  called YAML (pronounced "Yam-el"; it rhymes with "Camel")
  - `.yml` is the file extension for YAML files.
  - `.yml` syntax is used by many systems, not just GitHub Actions 
  
Note that, at least for now, you are not required to learn the special syntax of the `.yml` files used
for GitHub actions; we'll provide the contents and modifications needed.   We may learn little bits and pieces
of it as needed.   But if you want a reference for it, you can find
one here: 
* [Workflow Syntax for GitHub Actions](https://docs.github.com/en/free-pro-team@latest/actions/reference/workflow-syntax-for-github-actions)
  


Here is a `.yml` file that will run JUnit tests on a Java 11 Maven project.  We'll call it `.github/workflows/maven.yml` since it is a workflow for Maven.

```
name: Java CI

on:
  pull_request:
  push:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1
      - name: Set up JDK 11
        uses: actions/setup-java@v1
        with:
          java-version: 11.0.x
      - name: Build with Maven
        run: mvn test 
```
  
The directory structure should look like this:

![maven-dir-with-github-actions-50.png](maven-dir-with-github-actions-50.png)

With this in place, if we commit a change and put it to GitHub, we should see that our commit has either a yellow circle, green check or red X next to it, as illustrated by these three images:

Green check indicates all tests passed:

![green check](green-check-50.png)

Yellow circle indicates tests are still running (no results yet):

![yellow circle](yellow-circle-50.png)

Red X indicates either that at least one test failed, or the 
entire testing script failed in some way:

![red X](red-x-50.png)

If you click on the green check, yellow circle, or red X, you'll 
get a pop up with more information, and a link to the details.

That's all we are going to cover this in this example.
In the next example, we'll add some plugins to our `pom.xml`
and modify our script so that it can also perform test coverage,
which is also known as code coverage.

