---
layout: post
title: "Git Tips and Tricks"
author: skylar_lynner
categories: [ git ]
featured: true
---

## Can I add files from another branch?
Sometimes it is easier to move to a new branch to resolve
a problem than it is to try to fix the current one. To
do this without losing work, it is helpful to be able to
retrieve the changes you've made without having to copy
and paste by hand between the two. Thankfully, Git has
two options to help.

With the help of redirection, the file output can be
copied to the new location by using the git show command
and specifying the commit by the beginning of SHA value.

```
git show commit_id:path/to/file > path/to/file
```
Another option that can be done completely within git
and provides a better solution for bigger files is to
restore the file. This option can also be used for a
directory and provides the 'overlay' option to keep
current files while adding the new changes.

```
git restore --source=other-branch path/to/file
git restore --source=other-branch --overlay path/to/file
```

## I made a commit to the wrong branch
It is easy to start working and forget to create a new
branch for the work, then find that you've saved your
new changes into the main branch. A quick and easy fix
is to create a new branch with the changes and reset
the other branch to where it was before.

```
git checkout -b new-feature
git checkout main
git reset --hard <SHA-value>
```

If the changes have already been accidentally shared with
the remote repository, the newly reset branch can be
force-pushed to match the locally reset branch.

```
git push -f
```

Resets in a branch can create complexity when merging
branches, so it is important to let others on the team
know if they may have brought these changes into their
local repository to minimize possible conflicts between
branches.


Some additional features that can be used is to use the
"patch" option to stage the changes of part of a file. This
can help in creating atomic commits when revising a bigger
set of changes in a single file.


## I missed something in my last commit
If there is a quick change that to make to the most recent
commit, there is also the option to amend. This is helpful
when it is available, but is only an option for editing the
most recent commit. The process is similar to any other
commit, but with the amend option rather than a commit message.

```
git add
git commit --amend
```

## How do I test my commit without losing other work?
To assist in stepping through changes, especially when
testing functionality at specific points, the stash feature
provides a convenient way to temporarily store changes that
haven't been committed.

```
git stash
git stash pop
```

By default, any untracked files will not be included, but
this is quick to fix by simply using the option to include
them.

```
git stash -u
```
