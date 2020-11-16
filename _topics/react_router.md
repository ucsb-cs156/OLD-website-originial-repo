---
topic: "React: Router"
desc: "Using React Router in a spring/react app"
category_prefix: "React: "
indent: true
---

We show how to use React Router along with Spring in this demo repo:
* <https://github.com/ucsb-cs156-f20/demo-spring-react-minimal>

In our projects, we typically put the React Router code into a file called `App.js`, which represents the 
"main" file for the user interface of the application.

Here is an excerpt of that code.  
```javascript
return (
    <div className="App">
      <AppNavbar />
      <Container className="flex-grow-1 mt-5">
        <Switch>
          <Route path="/" exact component={Home} />
          <PrivateRoute path="/profile" component={Profile} />
          <AuthorizedRoute path="/admin" component={Admin} authorizedRoles={["admin"]}/>
          <Route path="/about" component={About} />
        </Switch>
      </Container>
      <AppFooter />
    </div>
  );
```

As you can see, there are three types of routes shown:

* `<Route ... />`
* `<PrivateRoute ... />`
* `<AuthorizedRoute ... />`

TODO: Add a discussion of when to use each of these, and for what purpose.
