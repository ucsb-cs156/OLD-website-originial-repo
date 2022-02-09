---
topic: "Spring Boot: Database"
desc: "Setting up a new SQL database table"
category_prefix: "Spring Boot: "
indent: true
---

To set up a new SQL database table in Spring Boot, you need to add two files:

* An `@Entity` class.  Each instance of this class represents one row in the database, and the fields in this class are the columns in the database
* A `@Repository` interface, which is the abstraction that represents the actual database table as a whole.  
 
The `@Repository` file is an interface rather than a class, because Spring Boot will *automatically create a class, and an instance of the class for you*.  
It writes most of the code that you need, without you having to do anything other than specify any custom queries you might perform beyond the default
ones.


# The `@Repository` class

The basic repository class is quite simple. If our `@Entity` class is `Thing`, then the `@Repository` class, at a minimum, looks like this:

```java
@Repository
public interface ThingRepository extends CrudRepository<Thing, Long> {
}
```

Note that in the Spring Data Documentation, this takes this form, where `T` is the type of our entity, and `ID` is the type of our
primary key; in this course, we are always using `Long` as the primary key type unless there is a reason to do otherwise:

```
public interface CrudRepository<T, ID extends Serializable> extends Repository<T, ID> {
}
```

With this basic declaration, you get a lot of query types through inheritance.  

The full list can be found at the [JavaDoc page for CrudRepository](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html)

Here are a few of the more important ones; here I've gone ahead and substituted `Long` for `ID`, but I've kept `T` for the entity type:



