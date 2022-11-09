---
layout: post
title: "Git Notebook"
author: skylar_lynner
categories: [ git ]
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

## Rename Branch

If others are using: rename before sharing or take steps to synchronize
changes.

```
git branch -m [<old-branch>] <new-branch>
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

## Add Something to a Commit

Add changes to staging directory, then amend commit. If commit is
already shared with a remote repository, you will need to use a
force push to share. Notify others of the change if they have pulled
the commit.

```
git commit --amend
```

## Ignored Files

Ignore a file:

```
git update-index --assume-unchanged "<path/to/file>"
```

Ignore changes in a tracked file:

```
git rm --cached <file/path>
```

Track an ignored file:

```
git update-index --no-assume-unchanged "<path/to/file>"
```
