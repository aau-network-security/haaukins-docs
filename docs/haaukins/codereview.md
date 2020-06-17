---
layout: default
title: Code Review
parent: Haaukins
nav_order: 5
---

# Code Review Checklist

All committed code should satisfy following requirements to be accepted: 
-  Even admins of repository absolutely should not commit anything directly to
master without any review.
- Before begin any development on a feature or bug, make sure that there is
not another branch which contains same feature developmen or bug fixes. If
there is, then merge conflicts will be appeared when merging branch into
targeted branch.
- Branches should be created feature or bug based and should have descriptive
names, for instance of there is a memory leak bug then name of the branch,
which will contain the solution to it, should be [ hotfix/fix-memory-leak-#000 ] or [ issue-
#212 ]
- Codes should be committed in formatted format (etc. using GOIMPORTS )
- Important parts should be commented
- There should be a naming convention (function names and variable names
should follow defined pattern such as getName(private) or GetName (public)
- Commit messages should be as much as shorter and meaningful.


