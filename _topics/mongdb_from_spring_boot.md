---
topic: "MongoDB: From Java"
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


