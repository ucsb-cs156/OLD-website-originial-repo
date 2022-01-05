---
topic: "Maven: Plugins"
desc: "Plugins extend Maven functionality"
indent: true
category_prefix: "Maven: "
---

In a Maven `pom.xml` file, there is a `<plugins>` section, which, unsurprisingly, contains one or more `<plugin>` elements:

```
<plugins>
  <plugin>
  ...
  </plugin>
  
  
  <plugin>
  ...
  </plugin>

</plugins>
```

Plugins extend the functionality of Maven.  Here are a few common ones that you may see in CS156, and what each of them does.

# maven-compiler-plugin/

The main purpose of this is to specify the version of Java that we'll be using to compile our code.  For example, this sets the version to Java 17:

```
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.0</version>
        <configuration>
          <release>17</release>
        </configuration>
      </plugin>
```


Learn More: <https://maven.apache.org/plugins/maven-compiler-plugin/

