---
topic: "MacOS"
desc: "Setting up an environment to do CS156 work on your own Mac (not ssh'ing into CSIL)"
category_prefix: "MacOS: "
---

This page is our best effort at explaining how to set up an environment for CMPSC 156 for MacOS.

For information on:
* Windows, see:  <https://ucsb-cs156.github.io/topics/windows/> 
* Windows Subsystem for Linux, please see: <https://ucsb-cs156.github.io/topics/windows_wsl/> 

Note that the reference platform for the course remains "CSIL"; we cannot commit to being "tech support" for every conceivable platform.  On your own machine, you *are* your own tech support.  But we'll help as best we can, given the time constraints we are under.
    
# Preliminaries

Installing [MacOS: Homebrew](/topics/macos_homebrew/) is your first step.  `brew` is a package manager for MacOS, and it is needed for the steps that follow.

# Install the JDK

To see whether you already have the JDK installed, do this in a terminal window:

```
169-231-88-206:~ pconrad$ javac -version
javac 1.8.0_31
169-231-88-206:~ pconrad$ 
```
If you see some version of Java 1.11.something... then you are good to go.

If not, download and install Java 11 using either the
* Official Oracle distribution (see below)
* The OpenJDK 11 distribution (see below)

There are three Slack channels that can help:
* Use the `#help-macos` channel to ask questions if you run into problems.
* Use the `#articles-macos` channel to offer tips, tricks, or links to resources that may help other students.
* Use the `#typos` channel if there are things in these instructions that are incorrect and should be updated.

# Installing Java 11 from Oracle on Mac

Oracle has a link for installing Java JDK 11 on Mac on this page: <https://www.oracle.com/java/technologies/javase-jdk11-downloads.html>

# Installing OpenJDK 11 on Mac

This worked for me.  Note that it requires [brew](https://ucsb-cs56.github.io/topics/macos_homewbrew/), a package manager for MacOS.
* <https://installvirtual.com/install-openjdk-11-mac-using-brew/>

Here's the short version--on first install:

```
brew update
brew tap AdoptOpenJDK/openjdk
brew cask install adoptopenjdk11
```

On later upgrades (e.g. from 11.0.6,10 -> 11.0.9.1,1) use:

```
brew update
brew cask upgrade adoptopenjdk11
```


To check if you now have Java 11, open a new Terminal window and do:

```
java -version
```

If it worked, you should see something like this:

```
# java -version
openjdk version "11.0.2" 2019-01-15
OpenJDK Runtime Environment AdoptOpenJDK (build 11.0.2+9)
OpenJDK 64-Bit Server VM AdoptOpenJDK (build 11.0.2+9, mixed mode)
```

# Install Mavem

After installing Java 11, do this to install maven:

```
brew install maven
```

Or if you already have Maven installed:

```
brew upgrade maven
```

And then do:

```
mvn --version
```

To make sure that Maven is using Java 11 and not still using Java 8 or earlier.

# What if Maven reports it is using Java 13

I recently got a new Mac and followed the instructions above.  I ended up with Java 11 as my default java compiled:

```
pconrad@Phillips-MacBook-Pro ~ % javac --version
javac 11.0.6
pconrad@Phillips-MacBook-Pro ~ % 
```

But I was frustrated the Maven was reporting that it was using Java 13:

```
pconrad@Phillips-MacBook-Pro ~ % mvn --version
Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
Maven home: /usr/local/Cellar/maven/3.6.3_1/libexec
Java version: 13.0.2, vendor: N/A, runtim: /usr/local/Cellar/openjdk/13.0.2+8_2/libexec/openjdk.jdk/Contents/Home
Default locale: en_US, platform encoding: UTF-8
OS name: "mac os x", version: "10.15.1", arch: "x86_64", family: "mac"
pconrad@Phillips-MacBook-Pro ~ % 
```

So I went back and looked at the messages during the `brew install maven`, and saw this:

```
pconrad@169-231-117-34 ~ % brew install maven
==> Installing dependencies for maven: openjdk
==> Installing maven dependency: openjdk
==> Downloading https://homebrew.bintray.com/bottles/openjdk-13.0.2+8_2.catalina
==> Downloading from https://akamai.bintray.com/65/65adca036393f528e3830cab8b0aa
######################################################################## 100.0%
==> Pouring openjdk-13.0.2+8_2.catalina.bottle.tar.gz
==> Caveats
For the system Java wrappers to find this JDK, symlink it with
  sudo ln -sfn /usr/local/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk

openjdk is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have openjdk first in your PATH run:
  echo 'export PATH="/usr/local/opt/openjdk/bin:$PATH"' >> ~/.zshrc

For compilers to find openjdk you may need to set:
  export CPPFLAGS="-I/usr/local/opt/openjdk/include"

==> Summary
🍺  /usr/local/Cellar/openjdk/13.0.2+8_2: 631 files, 314.6MB
==> Installing maven
==> Downloading https://www.apache.org/dyn/closer.cgi?path=maven/maven-3/3.6.3/b
==> Downloading from http://apache.spinellicreations.com/maven/maven-3/3.6.3/bin
######################################################################## 100.0%
🍺  /usr/local/Cellar/maven/3.6.3_1: 87 files, 10.7MB, built in 8 seconds
==> Caveats
==> openjdk
For the system Java wrappers to find this JDK, symlink it with
  sudo ln -sfn /usr/local/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk

openjdk is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have openjdk first in your PATH run:
  echo 'export PATH="/usr/local/opt/openjdk/bin:$PATH"' >> ~/.zshrc

For compilers to find openjdk you may need to set:
  export CPPFLAGS="-I/usr/local/opt/openjdk/include"

pconrad@169-231-117-34 ~ %
```

It appears that Maven brings in Java 13 as a dependency.  Not ideal if we are trying to target Java 11.

However, my hope is that if we configure our `pom.xml` files to use Java 11, perhaps this won't be an issue.

I will also see if I can figure out a way to get Maven to actually point to the Java 11 software as its default Java implementation.


# Install Heroku CLI

Follow instructions here: <https://devcenter.heroku.com/articles/heroku-cli>


# Install Node/npm

To install node and npm on Mac, use:

```
brew install node
```

# Install Apache Ant

** NOTE: We are likely not using Apache Ant this quarter, so you probably don't need to install this.  But in case you do, here are the instructions*.

If you need to install Apache Ant for any reason, first check to see if you already have it:

```
169-231-88-206:~ pconrad$ ant -version
Apache Ant(TM) version 1.9.7 compiled on April 9 2016
169-231-88-206:~ pconrad$
```

If instead, you get `command not found`, then install Apache Ant in one of the following ways:

* `brew install ant`
   * This requires Homebrew, which is described here: [/topics/homebrew](/topics/homebrew)
* These instructions: <https://www.mkyong.com/ant/how-to-apache-ant-on-mac-os-x/>
   * A student in W20 reported that these didn't work well, and that `brew install ant` worked better.

# Other Resources

**NOTE: The following article might no longer be relevant, but we'll keep it around for a little while in case it is useful**

This article tells you how to deal with having multiple versions of Java on your Mac, and what to do with the "tarball" file that you might find when you download OpenJDK 11 for Mac, since there are no obvious installation instructions.  Unfortunately, the link to the tarball takes you to a page where the distribution is NO LONGER AVAILABLE.  So this may no longer be relevant.

* <https://dzone.com/articles/installing-openjdk-11-on-macos>

