---
topic: "Legacy Code: Projects"
desc: "A list of legacy code projects associated with this course"
category_prefix: "Legacy Code: "
indent: true
apps: 
  - org: ucsb-cs156-w21
    repo: demo-spring-react-minimal
    heroku-prod: demo-spring-react-minimal
    heroku-qa: demo-spring-react-minimal-qa
    purpose: Minimal Starter Code for new apps
  - org: ucsb-cs156-w21
    repo: demo-spring-react-todo-app
    heroku-prod: demo-spring-react-todo-app
    heroku-qa: demo-spring-react-todo-app-qa
    purpose: Todo manager  
---

This page provides a list of some of the legacy code repos associated with this course.  This is not necessarily a complete list; we provide links to the ones that 
have active development.

| Repo | Prod Deployment | Prod Heroku | QA Deployment | QA Heroku | Purpose |
|------|-----------------|-------------|---------------|-----------|----------|
{% for app in page.apps %}| [{{app.repo}}](https://github.com/{{app.org}}/{{app.repo}}){:target="_blank"} | [{{app.heroku-prod}}](https://{{app.heroku-prod}}.herokuapp.com){:target="_blank"} | [Prod Heroku](https://dashboard.heroku.com/apps/{{app.heroku-prod}}){:target="_blank"} | [{{app.heroku-qa}}](https://{{app.heroku-qa}}.herokuapp.com){:target="_blank"} | [QA Heroku](https://dashboard.heroku.com/apps/{{app.heroku-qa}}){:target="_blank"} | {{app.purpose}} |
{% endfor %}{:.table .table-sm .table-striped .table-bordered}



