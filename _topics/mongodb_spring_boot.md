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

# Adjusting our collections

If you followed the  [MongoDB: New Database](https://ucsb-cs156.github.io/topics/mongodb_new_database/)  to set up your database, you
have:
* a database named `database`
* in that database, a collection named `posts`

To see that, here are the navigation steps you need:
* Select your organization:

  ![image](https://user-images.githubusercontent.com/1119017/152418744-43db11db-8d17-43ca-ad1d-a4feda301e73.png)

* Select your project:

  ![image](https://user-images.githubusercontent.com/1119017/152418808-cc834de9-d9ae-4cc7-8292-2875cbf802c7.png)
  
* When you see the cluster where your project is deployed, you can either click the `Browse Collections` button:

  ![image](https://user-images.githubusercontent.com/1119017/152418932-ee46623d-179b-4095-913a-5e62ce528552.png)

  Or you can click into the cluster, and then select the Collections tab:
  
  ![image](https://user-images.githubusercontent.com/1119017/152419023-81067c84-08ac-49e4-af44-0ef78efb46e3.png)

When you get there, you see this:

![image](https://user-images.githubusercontent.com/1119017/152419327-0d354c2f-68e2-4792-ad44-c39c5efa1a52.png)

# Renaming a collection

The first thing we will try to do is rename `posts` to `reddit_posts`.

Note that as far as I can tell, at the current time, there is no way to rename a collection in the web user interface.

Fortunately, since our collection is empty, we can just drop it and recreate it.  

To drop the collection posts, hover over `posts` and you'll see a trash can icon pop up:

![image](https://user-images.githubusercontent.com/1119017/152419662-632e4ca0-6b5b-4294-bef7-e9947b1ffe64.png)


Then, click the trash can and a confirmation modal appears. Type in `posts` and click `Drop`

![image](https://user-images.githubusercontent.com/1119017/152419763-ef4a07a5-20c1-4c4e-bd8d-1dc8195686ab.png)

That returns us to a state of having no collections, which looks like this:

![image](https://user-images.githubusercontent.com/1119017/152419854-6840051e-c57c-4d39-b4e2-1b5b2095a7e8.png)

From here, we'll click `Add your own data` and create two collections: `reddit_posts` and `students`. The user interface
here is a bit tricky, so I'll walk you through it.  First click `Add my own data` which gets us here, where you can fill in `database` and `reddit_posts`

![image](https://user-images.githubusercontent.com/1119017/152420104-e0d5bf9f-453c-494b-bd10-cba019e2b96f.png)

That results in this:

![image](https://user-images.githubusercontent.com/1119017/152420205-571cb9ce-01e8-493b-90c0-cc465628a5b3.png)


Then, to create the second collection (or additional ones after that), hover over the name `database`, and you'll see a plus sign pop up.  Click that to 
add the second collection.

![image](https://user-images.githubusercontent.com/1119017/152420224-7dd408c0-ef0f-421a-bc19-4c4a7f31e532.png)

Enter `students` as the name of the second collection:

![image](https://user-images.githubusercontent.com/1119017/152420283-cab197bd-d759-4b9a-9b3b-b07d796f49e3.png)

Now we have a database named `database` and two collections: `reddit_posts` and `students`.  We are ready to start doing Java coding.


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

In this case, it is straightforward to make a class `Student.java` that represents objects of this type. But our first step will be to create a directory under `src/main/java/` that is a sibling of our `controllers`, `services`, `entities`, etc. called `documents`, like this:


| Before | After |
|-|-|
| ![image](https://user-images.githubusercontent.com/1119017/152420561-712a7d15-a367-4622-90eb-ad33c8acd8e0.png) | ![image](https://user-images.githubusercontent.com/1119017/152420645-96628f71-45b2-4f3d-b029-57c715f3846e.png) |
{:.table .table-sm .table-bordered}





