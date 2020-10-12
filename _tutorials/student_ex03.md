---
topic: "Student: ex03"
desc: "Converting to Maven"
indent: true
code_repo: https://github.com/ucsb-cs156/student-tutorial
code_branch: ex03
---

# student-example/ex02

{% include student_tutorial_header.html %}




# Overview

In this example we introduce the use of Maven for compiling.

The example code that supports this lesson is in a repository ("repo" for short) at this link.  Note that this link is showing the branch <tt>{{page.code_branch}}</tt>, *not* the <tt>main</tt> branch of the repo.

* <{{page.code_repo}}/tree/{{page.code_branch}}>

If you have already cloned this repo and are at the command line, you can switch to the <tt>{{page.code_branch}}</tt> branch with this command:

* <tt>git checkout {{page.code_branch}}</tt>


# Converting to Maven

While it's good to know how to work with plain old Java code using `java` and `javac`, once
 you get beyond relatively small projects, you need more powerful tools.

There's a dillema:
* It's easiest to switch to these more powerful tools when the project is still relatively small.
* On the other hand, the *value* of doing so can be tough to see when the project is still small.

To help make the case for the value of Maven, shortly after introducing it, we'll show how to
use some sophisticated tools to do testing, measure test coverage, and measure the effectiveness of
a suite of test cases.   This can all be shown on a relatively small code base, but would be difficult
to accomplish without using a tool such as Maven.

In this example, we will not change any of the code; we are *only* showing how to convert the
repo to using Maven.

We are also not yet introducing *packages*, that too will be done in a later tutorial.

# What do you need to convert to Maven?

To convert a regular Java project to a Maven project, you really only need to do three things:

* Create the directory structure that Maven expects
* Put the code into that directory structure
* Create a `pom.xml` for the project.

# The directory structure

The directory structure needed by Maven is shown here:

![maven basic directory structure](maven-basic-dir-50.png)

To turn a "flat" project where everything is in one directory into a Maven project, the first
thing we do is create the `src/main/java` directory tree.  We can do this in an IDE such as VSCode by pointing and
clicking, or with this Unix command.  The `mkdir` command makes directories, and the `-p` flag indicates to create
an entire *path* all at once.

* `mkdir -p src/main/java`

We can then move all of the Java files into that directory using a wildcard (i.e. a `*`)

* `mv *.java src/main/java`

We can remove any .class files hanging out in the top level directory; maven will automatically clean those up for us
once we switch to Maven:

* `rm -f *.class`

Finally, we need a `pom.xml` file.  Here's a minimal one.  An explanation of this file, which you are
*strongly encouraged to read*, can be found
here: <https://ucsb-cs156.github.io/topics/maven_hello_world/>.

Seriously, go read that.  I would have included it in the tutorial here, but it seemed redundant to copy/paste,
when you can just go read it.

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>edu.ucsb.cs156</groupId>
    <artifactId>student</artifactId>
    <version>1.0.0</version>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.0</version>
                <configuration>
                    <release>11</release>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>
```

With these changes, we can now use Maven commands to compile and package our code.

* `mvn compile`
* `mvn package`

To run, it's the same as before, except we use `-cp target/student-1.0.0.jar` to point the Java Virtual Machine (jvm) to
load the `.class` files from the indicated `.jar` file instead of from the current directory.

* `java -cp target/student-1.0.0.jar Main Chris 1234567`

Here's what it looks like when we've done those things:

```


```




<div class="github-preview-only">On website: https://ucsb-cs156.github.io/tutorials/student_ex03/</div>
