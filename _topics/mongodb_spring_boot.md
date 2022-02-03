---
topic: "MongoDB: Spring Boot"
desc: "Accessing a MongoDB collection from Spring Boot"
category_prefix	: "MongoDB: "
indent: true
---

This article assumes that you have worked through the steps in [MongoDB: New Database](https://ucsb-cs156.github.io/topics/mongodb_new_database/) to 
set up a MongoDB deployment on the site <https://cloud.mongodb.com>, with:

* a cluster than can accessed from `0.0.0.0/0`, i.e. from any IP address
* a username and password with read/write access
* a database called `database` and a collection called `posts`

From that starting point, we'll explain:

* How to set up a Java class that represents a single `Document` in the  collection
* How to set up a Java class that represents the entire collection
* How to use those classes in backend controller methods to do CRUD operations on the collection.


# Setting up the `pom.xml`

To work with MongoDB, we should add the following dependency to our `pom.xml`.  Check the URL in the comment for the latest version; at this writing
that is `2.6.3` but it may be later by the time you are reading this.

```xml
   <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-data-mongodb -->
   <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-mongodb</artifactId>
   </dependency>
```

If using the the `spring-boot-starter-parent` as many of our projects are, i.e. the code below, then it is not necessary to specify a version; that will 
be determined by the version in the `<parent>` element:

```xml
    <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-parent -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.6.3</version>
        <relativePath /> <!-- lookup parent from repository -->
    </parent>
```

Otherwise consult the URL in the comment to determine the latest version to use.

# Setting up a Document class

A MongoDB document is a representation of a JSON object.  As such, it can be nested arbitrarily deep.

The same is true when setting up a Java object to represent a MongoDB document. 

Suppose we have a simple JSON object, such as the following JSON object representing a student with a name and a perm:

```json
{
   "first_name" : "Chris",
   "last_name" : "Gaucho",
   "perm" : 1234567
}
```

In this case, it is straightforward to make a class `Student.java` that represents objects of this type:

```

```
