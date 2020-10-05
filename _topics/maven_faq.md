---
topic: "Maven: FAQ"
desc: "Frequently Asked Questions"
indent: true
---

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
