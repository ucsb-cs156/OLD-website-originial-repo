---
topic: "React: Spring Boot"
desc: "Combining a React Front End with a Spring Boot Backend"
category_prefix: "React: "
indent: true
---

# Examples, Tutorials, Resources

## <https://blogg.kantega.no/webapp-with-create-react-app-and-spring-boot/>

Note that the instructions for configuring the proxy are out of date.  When you get to the step for adding a `proxy` entry in the `package.json`, if you follow the instructions as given, you'll get this error:
 
```
When specified, "proxy" in package.json must be a string.
```
To address this, follow the instructions at [this Stack Overflow answer](https://stackoverflow.com/questions/52605997/when-specified-proxy-in-package-json-must-be-a-string)
    
Summary:
* Inside `frontend`, type this to install `http-proxy-middleware` as a dependency.
  ```
  npm install http-proxy-middleware --save
  ```
* Create a file `frontend/src/setupProxy.js` with these contents:
  ```javascript
  const proxy = require('http-proxy-middleware');

  module.exports = function(app) {
    app.use(proxy('/api', { target: 'http://localhost:8080/' }));
  };
  ```
    
Repos: 
* Original: <https://github.com/kantega/react-and-spring>
* Modified by P. Conrad so that it works on Heroku and with current versions of React and Spring Boot: <https://github.com/pconrad/cs156-try-spring-react-01>  

## <https://spring.io/guides/tutorials/react-and-spring-data-rest/>

This tutorial is a good guide for setting up REST endpoints automatically for CRUD operations for an entity/repository for Spring Data.

For React, this tutorial uses the plugin <https://github.com/eirslett/frontend-maven-plugin>

One thing that can be bewildering is that while the main tutorial here suggests that all you have to do is put this in your `pom.xml` and you are off and running, in reality, you have to do a bit more than that.

```
<plugin>
	<groupId>com.github.eirslett</groupId>
	<artifactId>frontend-maven-plugin</artifactId>
</plugin>
```

That's a good start.  But it is helpful to consult these additional sources of information about the `frontend-maven-plugin`:
* <https://huongdanjava.com/manage-node-js-dependencies-with-frontend-maven-plugin.html>
* <https://auth0.com/blog/integrating-node-dot-js-build-tools-with-maven/>
* <https://dev.to/tzehe/dev-recipes-integrate-react-frontend-in-a-java-corporate-environment-2e43>
* <https://frakton.com/utilizing-maven-front-end-plugin-for-angular-spring-boot/> (Though this uses Angular, ignore that, and focus on how the `frontend-maven-plugin` is configured.

In order to get the `npm` stuff to install, you have to do `mvn install`.   I have not yet found a way to get Maven to do the bits and pieces of this plugin independently.

A few other notesa
* If you follow the tutorial, there are a few files you need from the [repo containing the finished code](https://github.com/spring-guides/tut-react-and-spring-data-rest) that are not spelled out in the tutorial.  These include at least the following:
  * `src/main/js/client.js`
  * Everything under `src/main/js/api`
* In `webpack.config.js`, instead of setting:
  ```
   filename: './src/main/resources/static/built/bundle.js'

  ```
  
  You can set the output directory for webpack to be under `target`.  
  
  ```
   filename: './target/classes/static/built/bundle.js'
  ```
  
  Some advantages:
  * You don't want generated files cluttering up your `src` directory.   
  * To avoid cluttering up your diffs, you'd have to put `./src/main/resources/static/build/` in your `.gitignore`, but if you put this under `target`, is it automatically in your `.gitignore`
  * A `mvn clean` automatically gets rid of the generated files so you can do a clean build.


## Others


* <https://hackernoon.com/package-your-react-app-with-spring-boot-a-how-to-guide-cdfm329w>
* <https://developer.okta.com/blog/2018/07/19/simple-crud-react-and-spring-boot>
* <https://medium.com/@mukundmadhav/build-and-deploy-react-app-with-spring-boot-and-mysql-6f888eb0c600>
  * Focused on *not* implementing on Heroku, but on doing everything from scratch.
  * Has a lot of low-level MySQL details that may not be relevant for CS156
  * But, also has a few useful tips on the use of `frontend-maven-plugin` and copying files with the Ant plugin 
* <https://blog.indrek.io/articles/serving-react-apps-from-spring-boot/>
  * Works with Gradle, so not currently relevant to CS156 (unless/until we pivot from Maven to Gradle)
