# How to Create an Optimized Git Workflow

## Step 1
Create a branch to start working from. Start work and make
commits locally. Make commit messages along the way with any
relevant information. These don't need to be neat and tidy,
but it is helpful to leave any relevant information in case
these commits will be revisited when troubleshooting.

```
git checkout -b feature-branch
git commit -m "starting progress"
git commit -m "added some functionality to the UI, something is broken in ClassA"
git commit -m "UI is functional, ClassA has been fixed"
```

## Step 2
When a good stopping point is reached, it can be useful
to take a minute to clean up the branch. If there are 
new changes from the main branch to implement, now is the time. 
If there are any notes you want to take from your commits, either 
create a copy of the branch to reference or take some quick notes. 
First, the branch will be reset, then the new changes will be merged, 
finally the changes in the branch will be re-committed. 

```
git reset < SHA-VALUE >
git merge < SHA-VALUE >
```

First, check the log and find the first commit on the branch, 
reset to this location. All changes will be moved from the 
commits into the working directory. Then, merge any changes 
to be added by using the reference to the commit that is to be 
added. At this point, all changes will be added and all work 
that has been done on the branch is in the working directory. 
From here, the changes in the working directory can be 
reconstructed into atomic commits, creating a log of commits 
that are easier to follow and groups changes appropriately 
in an easy to follow sequence.

## Step 3
If there is more to be done, commits can revert back to
in-progress style. If there isn't more to add at the base 
of the branch, these commits can be quickly restructured 
by working from the most recent "finished" commit when 
choosing a commit to reset to.

## Step 4
When the feature is implemented and work is ready to be 
shared, all that will need to be done is to finish any 
organizing of commits and creating a pull request to 
merge the feature branch with its new added functionality. 

## Additional Options when Building the Commit Log
Some additional features that can be used is to use the
"patch" option to stage the changes of part of a file. This
can help in creating atomic commits when revising a bigger
set of changes in a single file.

```
git add --patch
```
or
```
git add -p
```

Another feature that can be implemented to assist in stepping
through these commits while testing the functionality is to
use the "stash" feature.

```
git stash
git stash pop
```

If there is a quick change that you find you want to make to
the most recent commit, there is also the option to amend.
This is helpful when it is available, but is only an option
for editing the most recent commit. The process is similar to
any other commit, you would add the changes and then issue a
commit, but this time with the "amend" option instead of a
message.

```
git add
git commit --amend
```

## Read Further

[Git Organized: A Better Git Flow](https://dev.to/render/git-organized-a-better-git-flow-56go)
