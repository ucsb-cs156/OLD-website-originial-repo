---
topic: "Student: ex07"
desc: "Setting up pitest mutation testing"
indent: true
code_repo: https://github.com/ucsb-cs156/student-tutorial
code_branch: ex07
---

# {{page.topic}} - {{page.desc}}

{% include student_tutorial_header.html %}

# Overview

In this example we go beyond line and branch coverage,
to an even better way of checking the rigor of a test suite:
mutation testing.

The website for [pitest](https://pitest.org) has a nice summary
of what mutation testing is, so I'm just going to quote from it:

> ## What is mutation testing?
> How it works in 51 words
>
> Mutation testing is conceptually quite simple.
>
> Faults (or mutations) are automatically seeded into your code, 
> then your tests are run. If your tests fail then the mutation 
> is killed, if your tests pass then the mutation lived.
>
> The quality of your tests can be gauged from the percentage of 
> mutations killed.
> 
> ## What?
> Really it is quite simple
>
> To put it another way - PIT runs your unit tests against 
> automatically modified versions of your application code. When
> the application code changes, it should produce different 
> results and cause the unit tests to fail. If a unit test does
> not fail in this situation, it may indicate an issue with the
>  test suite.
>
> #Why?
> What's wrong with line coverage?
>
> Traditional test coverage (i.e line, statement, branch, etc.)
> measures only which code is executed by your tests. It does
>  not check that your tests are actually able to detect faults
> in the executed code. It is therefore only able to identify
> code that is definitely not tested.
>
> The most extreme examples of the problem are tests with no 
> assertions. Fortunately these are uncommon in most code bases.
> Much more common is code that is only partially tested by its
> suite. A suite that only partially tests code can still
> execute all its branches (examples).
>
> As it is actually able to detect whether each statement is 
> meaningfully tested, mutation testing is the gold standard
> against which all other types of coverage are measured.

# So how does this work in practice?

So, to clarify, you will run mutation testing once you've
gotten to 100% line/branch coverage, or as close to it as
you can get.  At that point, you run:

```
mvn test org.pitest:pitest-maven:mutationCoverage
```

(Yeah, no one is going to expect you to memorize that command.
We might expect you to know `mvn compile`, `mvn package`, and `mvn test`, and maybe even `mvn test jacoco:report`, but not this one.)

When you run that command, each of the java files under `src/main/java` will be *mutated*; the pitest software will create mutant versions of that code in an attempt to deliberately introduce bugs.

Then, each of those mutants meets one of two fates:
* *killed* if test suite finds it (i.e. if if fails some test in the test suite)
* *survives* if the test suite doesn't detect the mutation

There is also a third possibility: if the portion of the code mutated is never even run by the test suite, you might get a report that
there was *no coverage*.

As an aside, this highlights the justification for separating out the
`src/main/java` code from the `/src/test/java` code: 
* We use the code in `src/test/java` to check the correctness of
  the code under `src/main/java`
* We mutate the code under `src/main/java` in order to evaluate the
  tests under `src/test/java`.

  
The output of the pitest report will show you how many mutants are killed, survived, or had no coverage.  The goal is to kill 100% of the mutants.

# How to set up pitest coverage for a Maven project

To set up pitest coverage for Maven project, we only need to make some
change to the `pom.xml`.

Optionally, we might also add pitest into our GitHub workflow; we'll mention that
in a separate section below.



# Adding pitest to our GitHub workflow

To add pitest to our GitHub workflow, we only need to add a small number of lines 
to the bottom of our existing `.github/workflow/maven.yml` file.

Here are the new lines:

```

```


# How do I know which mutants were killed, survived, or not covered?

The output you get on your console will tell you a summary
of the fate of each mutant.   You can see more detailed output by using a web browser to open up the file:

* <tt>target/pit-reports/<i>yyyymmddhhmm</i>/index.html</tt>

Note that <tt><i>yyyymmddhhmm</i></tt> will be replaced by a date/timestamp; each time you run the Maven command to run
pitest, it will produce a new version of the report with a new timestamp.  

It may be convenient to use `mvn clean` before running a pitest mutation report; that way there will only be one such directory rather than multiple ones.

# Another way to see the Pitest report: GitHub Actions artifacts

Another way to see the pitest report is to let the GitHub Actions run for your
repo (which happens each time you push a change to GitHub).   When you do, you should
see that there is a link for "Artifacts" when you examine the Github Actions results.

If you download the artifacts, you'll get a .zip file that you can download, and
open.  Inside that zip file, you'll find an `index.html` file that you can open in a
web browser.  That will show you the Pitest mutation report.

![click the green check](click-green-check-50.png)

![click where it says details](click-details-50.png)

![click on artifacts](click-artifacts-50.png)

![click to download zip](click-to-download-zip-50.png)
