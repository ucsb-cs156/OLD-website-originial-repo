---
topic: "eslint"
desc: "Linting (checking for style and frequent errors) in ECMAScript (i.e. JavaScript)"
---

The utility `eslint` is used in many of our projects to do *linting* of our JavaScript/ECMAScript code.

# Configuring Exceptions

Sometimes there are individual style rules that `eslint` enforces that you might have a specific reason to
want to ignore.

As an example, in Storybook code, there is a convention that results in this warning from `eslint`:

```
/Users/pconrad/github/HappyCows/dsrk/frontend/src/stories/components/Profile/RoleBadge.stories.js
  6:1  warning  Assign object to a variable before exporting as module default  import/no-anonymous-default-export

/Users/pconrad/github/HappyCows/dsrk/frontend/src/stories/layouts/BasicLayout/BasicLayout.stories.js
  6:1  warning  Assign object to a variable before exporting as module default  import/no-anonymous-default-export

```

The string `import/no-anonymous-default-export` is a label that identifies this particular issue.  What we want to do
is suppress these warnings, but only under the directory tree `src/stories`.

To do this, we can modify the file `.eslintrc.json` in the `javascript` directory.

The process is documented here: <https://eslint.org/docs/user-guide/configuring/>

Note that because we are using Create-React-App, there are some subtle issues that arise,
as explained here: <https://create-react-app.dev/docs/setting-up-your-editor/#extending-or-replacing-the-default-eslint-config>.  What it boils down to is that you need this line in your configuration so that your customizations extend the ones already being done under the hood
for `react-app`, rather than replacing them, resulting in strange issues.

```
  "extends": ["react-app"],
```

