---
topic: "Maven: FAQ"
desc: "Frequently Asked Questions and misc tips/troubleshooting"
indent: true
---


# `The JAVA_HOME environment variable is not defined correctly`...

If you are working on CSIL and get this error
```
The JAVA_HOME environment variable is not defined correctly
This environment variable is needed to run this program
NB: JAVA_HOME should point to a JDK not a JRE
```
Then here's the fix:

```
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk
```

Type that once before you use mvn commands

To avoid having to type that every time you work on CSIL, you can add that line to your Shell startup files.   That file might be, for example, `.bashrc` by running the following:

```bash
echo 'JAVA_HOME=/usr/lib/jvm/java-11-openjdk' >> ~/.bashrc
```

You can verify that this worked properly by doing the following:

```bash
source ~/.bashrc
$JAVA_HOME/bin/javac -version
```

You should see `javac 11.0.8` as the output. 

Disconnect and reconnect to double check that it still works; if it still does, then you've solved the problem.

# `Error: A JNI error has occurred, please check your installation and try again`

This error usually indicates a mismatch between the Java versions being used. For example, you may have compiled with Java 11 but are using an older version of the JRE. First make sure your `JAVA_HOME` variable is set to JAVA 11 (following the instructions in the first part of this post if necessary), then make sure your `PATH` environment variable is updated to make sure the JRE for Java 11 is being used: 

```
export PATH=$JAVA_HOME/bin:$PATH
```
To make this change permanent, add it to your `.bashrc`:
```
echo 'PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

# What the heck: `[WARNING] Using platform encoding (UTF-8 actually)`

Here's what to do:

```xml
 <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
```

While you are at it, you might also include the version of Java you need:

```xml
   <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>
```

# Making `mvn clean` remove app specific files


If you want `*.log` from the `logs` directory (or any other custom fileset or directory) to be deleted when you do `mvn clean`, here is how you can accomplish that: just "configure the `maven-clean-plugin`" in your pom.xml (as explained [here](https://maven.apache.org/plugins/maven-clean-plugin/examples/delete_additional_files.html)).  Be sure this goes in the `build` plugsin (not the `reporting` plugins, for example.)

```xml
   <!-- also remove logs on maven clean -->
      <plugin>
        <artifactId>maven-clean-plugin</artifactId>
        <version>3.1.0</version>
        <configuration>
          <filesets>
            <fileset>
              <directory>logs</directory>
              <includes>
                <include>**/*.log</include>
              </includes>
            </fileset>
          </filesets>
        </configuration>
      </plugin>
```
