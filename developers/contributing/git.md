---
layout: page
title: Git Layout
---

Most of the LOCKSS Program's Git repositories use a simplified Git Flow layout.

Stable releases are recorded on the `master` branch with tag names beginning with `version-`.

Settled contributions are recorded on the `develop` branch, which should build successfully at all times (or as close as feasible to it).

In-progress development takes place off of the `develop` branch on feature branches with names beginning with `feature-`.

Stable releases are prepared on release branches with names beginning with `release-`. These branches stem from the `develop` branch, and are eventually merged into the `master` branch and marked with tag names beginning with `version-`.

Hotfix releases are prepared on hotfix branches with names beginning with `hotfix-`. These branches stem from the `master` branch, and are eventually merged into the `master` and `develop` branches.

Some Git Flow models include other types of branches, like bugfix branches, but we do not use them.

## See Also

*   [*A Successful Git Branching Model*](https://nvie.com/posts/a-successful-git-branching-model/) by Vincent Driessen
*   [*Git Flow Cheat Sheet*](https://danielkummer.github.io/git-flow-cheatsheet/) by Daniel Kummer
*   [*Gitflow Workflow*](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) by Atlassian
