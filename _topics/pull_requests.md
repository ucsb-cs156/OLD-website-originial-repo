---
topic: "Pull Requests"
desc: "aka PRs; a checklist for doing them properly"
---

# Pull Requests

# A Checklist

1. PR Title:
   - Is it escriptive enough that someone familiar with the project can understand it at first glance?
   - Is it short enough to be readable at a glance? (For example, don't try to put the entire "As an X I can Y so that Z" story into the title field.)
2. Linked to an Issue?
   - You can link to an issue with certain magic words such as `Closes #15`, `Fixes #27`
   - But if you don't phrase it just right, the link doesn't happen.
   - In that case, use the manual feature for linking to an issue (see below)
3. Linked Issue is in the "In Review" column on team's Kanban board.
4. PR is tagged with the Team's tag, like this one:
   ![tagged PR](tagged-PR.png)
5. Test cases all pass.
   - If you have difficulty with this one, ask for help from a team member first.
   - Then ask for help on the Slack help channel associated with the project, e.g. `#proj-ucsb-courses-search`, `#proj-ucsb-cs-las`, `#proj-mapache-search` on the slack.
   - Then ask for help during staff office hours or during lecture/discussion work time.
6. You have requested (and gotten) a code review from a fellow team members.
7. You have requested (and gotten) a code review from a member of staff (i.e. an LA, TA, or the instructor)
   - Please consult the page with team assignments (e.g. for W21 that's here: ) to see which LA and TA are assigned to your team. 
   - Request those members of staff first; however anyone on staff can review your PR.
8. Address all concerns brought up in the code review. This doesn't mean that you have to do exactly as the code reviewer says, but it does mean
   that you can't just ignore what they suggest.  Acceptable ways of resolving a code review concern include:
   - Doing what the code reviewer asks
   - Presenting a good case why you are not going to do that (e.g. "that's a good point, but let's do that in a different issue", or "I see the situation differently; here's my point of view; let's discuss.")
9. Address any merge conflicts that exist between your feature branch and the then current `main` branch.  You may need to "rebase" your branch on main.
   - Merge conflicts with `package-lock.json` are a special case covered here: <https://ucsb-cs156.github.io/topics/spring_react_package_lock_json_merge_conflicts/>
   - If you have other merge conflicts that you don't know how to resolve, ask for help.
   

# Linking a PR to an issue

 You can link to an issue automatically with certain magic words such as `Closes #15`, `Fixes #27`.
 
 But if that doesn't work, here's how to do it manually:
 
 ![Animated Gif that shows how to link a PR to an issue](link-PR.gif)
 
 
 # Doing a Code Review
 
Many companies use "branch protection" rules in GitHub for their `main` branch (or `master` branch, if using the older convention).

Rules may include the number of code reviews that must be done.  In our case, we are requiring two code reviews, one from the team, and one from a member of staff.

For these code reviews to "count", i.e. to make the PR mergable, the code review needs to be done *with the right set of mouse clicks* in GitHub. (It isn't enough, for exmaple, to just put a "comment" `LGTM` ("Looks Good To Me"); that comment has to be done *as an approving code review*. 

Here's what that looks like. 

![Approving Code Review](LGTM-Code-Review.gif)


