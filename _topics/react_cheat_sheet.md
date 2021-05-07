---
topic: "React: Cheat Sheet"
desc: "Helpful tips for working with frontend code in CS156"
category_prefix: "React: "
indent: true
---

This page is not intended to be a full React tutorial, but a brief overview of some of the 
most important things you need to have at your finger tips when working with React code.


# Six Terminal Windows

While this may seem extreme, I suggest having six terminal windows, each with specific roles to play.

| Num | Name | Directory | Purpose |
|-----|------|-----------|---------|
| 1 | Main | root of repo | Running git commands, and running `code .` to open VS Code |
| 2 | Backend | root of repo | Run backend with `mvn spring-boot:run` |
| 3 | Backend tests | root of repo | Run backend tests with `mvn test` <br /> or Test coverage with `mvn test jacoco:report` |
| 4 | Frontend | `javascript` | Run frontend with `npm start` |
| 5 | Frontend Tests | `javascript` | Run front end unit tests `npm test`<br /> jest coverage with `npm run coverage`, <br />Stryker coverage with `npx stryker run`, <br /> or eslint with `npx eslint --fix src` |
| 6 | Storybook | `javascript` | Run storybook with `npm run storybook` |
{:.table .table-sm .table-striped .table-bordered}

We'll refer to these windows throughout the rest of this cheat sheet.
