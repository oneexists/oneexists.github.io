---
layout: post
title: "Git Notebook"
author: skylar_lynner
---

## Git Aliases

```
git config --global alias.st "status"
git config --global alias.co "checkout"
git config --global alias.ci "commit"
git config --global alias.br "branch"
git config --global alias.df "diff"
git config --global alias.dfs "staged"
git config --global alias.logg "log --graph --decorate --oneline --all"
```

## Move Commits to a New Branch

```
git checkout -b new-branch
git push -u origin new-branch
git checkout main
git reset --hard <SHA>
git push -f origin main
```

## Clone a Remote Branch

```
git checkout -b new-branch
git pull -u origin new-branch
```

## See Last Commit

Last commit with file line diff summary:

```
git show --stat
```

Last commit without file change:

```
git log -1
```

One line with file diff summary:

```
git show --oneline --stat
```

## Push Only up to Specific Commit

```
git push <remote-name> <commit-SHA>:<branch-name>
```
