---
topic: "Codecov: Troubleshooting"
desc: "Solutions to problems that commonly arise with Codecov"
category_prefix: "Codecov: "
indent: true
---

# I cannot find my upload token

Try navigating to <https://codecov.io/gh/organization-name/repo-name>

For example: <https://codecov.io/gh/ucsb-cs156-f20/jspa01-cgaucho>

If you get a 404, then there are a few things you may need to try:

1. Try logging in with your GitHub account.

2. If that still doesn't work, you may need to "Add Private Scope".  See instructions below.


# Adding Private Scope

When you log in to codecov.io with your GitHub account, you are using OAuth.   Codecov.io is
an "OAuth Application" that you authorize to access your GitHub repositories.

When you authorize any OAuth appllication, there is a concept of "scope".  For example, when
you login to an application using Facebook, you are asked whether you want to give Facebook
permission to access your account.  Along with that, the application will list the specific
things that Facebook can, or cannot do with this access. For example, can the application
* see your friends?
* post to your timeline?
* etc.

These fine-grained permissions are called *scopes*.

When you authorize Codecov through GitHub, there are "scopes" that you approve.
But  "access to private repos" might not get added by default.  So you may have to go
back and fix that.  Here's how.


To "Add Private Scope" means to add additional permissions to the "OAuth Application".

Here's how you do it.  

* Navigate to <https://codecov.io/gh/your-github-id-here>, e.g. <https://codecov.io/gh/cgaucho>

Then, if your account is *not* authorized for private repos, you see a button like the one
in the image below. Click that button.

![add private scope](codecov-add-private-scope-50.png)

Then, you should be able to bring up your private repos on Codecov by navigating to links such as this one
(substituting in the right values for the `org-name` and `repo-name`.

* <https://codecov.io/gh/organization-name/repo-name>

