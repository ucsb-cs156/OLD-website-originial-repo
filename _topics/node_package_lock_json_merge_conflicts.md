---
topic: "Node: package-lock.json merge conflicts"
desc: "Installing and working with Node, npm, nvm on Linux"
indent: true
category_prefix: "Node: "
---

A merge conflict in package-lock.json is a special case.  It looks like this:

<img width="950" alt="image" src="https://user-images.githubusercontent.com/1119017/154364907-01b9e567-72ab-4745-88c4-0958045c2f92.png">


Here's how you go about resolving it.

1.  Checkout the branch in question.  For example, in this case the branch is: `rh-subjects_menu_page`

    <img width="813" alt="image" src="https://user-images.githubusercontent.com/1119017/154365102-900baf48-b20e-4a90-a961-1e3d24d67566.png">
    
    ```
    pconrad@169-231-112-36 team03-w22-7pm-2 % git checkout rh-subjects_menu_page
    Branch 'rh-subjects_menu_page' set up to track remote branch 'rh-subjects_menu_page' from 'origin'.
    Switched to a new branch 'rh-subjects_menu_page'
    pconrad@169-231-112-36 team03-w22-7pm-2 % 
    ```
    
 2. Make sure the branch is up-to-date with what's on github by pulling from the branch:

    ```
    git pull origin rh-subjects_menu_page
    ```

3.  Next, type the command to rebase your branch on origin main, like this:

    ```
    git pull --rebase origin main
    ```
    
    Heres what that would look like. Note that the `git` command line is telling us the same thing that GitHub did, namely that we have
    a merge conflict in `package.lock.json`
    
    ```
    pconrad@169-231-112-36 team03-w22-7pm-2 % git pull --rebase origin main
    From github.com:ucsb-cs156-w22/team03-w22-7pm-2
     * branch            main       -> FETCH_HEAD
    First, rewinding head to replay your work on top of it...
    Applying: created menu and pages
    Using index info to reconstruct a base tree...
    M	frontend/package-lock.json
    .git/rebase-apply/patch:35850: trailing whitespace.

    warning: 1 line adds whitespace errors.
    Falling back to patching base and 3-way merge...
    Auto-merging frontend/package-lock.json
    CONFLICT (content): Merge conflict in frontend/package-lock.json
    error: Failed to merge in the changes.
    Patch failed at 0001 created menu and pages
    hint: Use 'git am --show-current-patch' to see the failed patch
    Resolve all conflicts manually, mark them as resolved with
    "git add/rm <conflicted_files>", then run "git rebase --continue".
    You can instead skip this commit: run "git rebase --skip".
    To abort and get back to the state before "git rebase", run "git rebase --abort".
    pconrad@169-231-112-36 team03-w22-7pm-2 % 
    ```
    
