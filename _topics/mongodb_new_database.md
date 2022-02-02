---
topic: "MongoDB: New Database"
desc: "Setting up a new database on cloud.mongodb.com"
category_prefix	: "MongoDB: "
indent: true
---

This article will show the process of setting up a MongoDB Datbase, which holds MongoDB Collections.

First, some basic terminology:

* What we call a "table" in an SQL database is called a "collection" in a MongoDB database.
* What we call a "row" in a table in called a "document" in an MongoDB database.

But, unlike a row that has specific fields (columns), 
a document in a MongoDB database is essentially a JSON object stored in the cloud; 
thus it can have arbitrarily deep nested structure.


Also, note the following hierarchy that is used on <https://cloud.mongodb.com>.  Each level in the hierachy can have
multiple items at the next level down, i.e. an organization can have many projects, a project can have many databases,
a database can have many collections, and a collection can have many documents.

* Organization (e.g. `ucsb-cs156-w22`)
  - Project (e.g. `demo-mongodb-project-01`)
    - Database (e.g. `database01`)
      - Collection (e.g. `reddit_posts`)
        - Document (e.g. the JSON representation of a specific reddit post, e.g. )
 
 
      
Once you have navigated to an organization and have created a new project, you'll see this screen where it is possible to create your first database.


<img alt="Create Database" src="https://user-images.githubusercontent.com/1119017/152082399-445e96ae-f6dc-412d-8ed4-3bafe26612c2.png" width="800" />


The next choice you need to make is what kind of deployment.  Clearly, we are going to choose the *FREE* option for this course, but
if you are building something for your own use, and are prepared to pay for it, you might make a different choice.


<img alt="Deployment options, choose FREE" src="https://user-images.githubusercontent.com/1119017/152082540-5caa8846-fb98-491b-a45c-dadeaa5ce7d6.png" width="800" />

The next choice you will make is which cloud provider to use, as well as various other options.  I suggest taking the defaults.
(It could be argued that there might be some marginal benefit to using `us-west-2` instead of `us-east-1`, just because
of geographical proximity to California, and if you have a reason to prefer Google Cloud or Microsoft Azure over Amazon AWS, feel free.)

After taking the defaults (or configuring to your hearts content), click the green "Create Cluster" button.

<img alt="Create Cluster" src="https://user-images.githubusercontent.com/1119017/152082831-3cef6f74-42bf-4bfd-b89b-035960fa7175.png" width="800" />




<img alt="" src="" width="800" />
<img alt="" src="" width="800" />
<img alt="" src="" width="800" />
<img alt="" src="" width="800" />
