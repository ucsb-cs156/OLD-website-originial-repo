---
topic: "Legacy Code: Projects"
desc: "A list of legacy code projects associated with this course"
category_prefix: "Legacy Code: "
indent: true
apps: 
  - org: ucsb-cs156-w21
    repo: demo-spring-react-todo-app
    heroku-prod: demo-spring-react-todo-app
    heroku-qa: demo-spring-react-todo-app-qa
    purpose: Todo manager
---

This page provides a list of some of the legacy code repos associated with this course.  This is not necessarily a complete list; we provide links to the ones that 
have active development.

| Repo | Production Deployment | QA Deployment | Purpose |
|------|-----------------------|---------------|---------|
{% for app in page.apps %}
| [{{app.repo}}](https://github.com/{{app.org}}/{{app.repo}}) | [{{app.heroku-prod}}](https://{{app.heroku-prod}}.herokuapp.com) | [{{app.heroku-qa}}](https://{{app.heroku-qa}}.herokuapp.com) | {{app.purpose}} |
{% endfor %}


