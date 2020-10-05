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

To avoid having to type that every time you work on CSIL, you can add that line to your Shell startup files.   That file might be, for example, `.bashrc`

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
