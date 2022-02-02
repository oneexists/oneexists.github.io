# How to Create an Optimized Git Workflow

1. Create a branch to start working from. Start work and make commits locally. Make commit messages along the way with any relevant information. These don't need to be neat and tidy, but do need to communicate anything relevant that may need to be referenced later if issues arise.

```
git checkout -b feature-branch
git commit -m "starting progress"
git commit -m "added some functionality to the UI, something is broken in ClassA"
git commit -m "UI is functional, ClassA has been fixed"
```

2. If something is implemented and you have reached a good stopping point, take some time to reset the branch. Reset branch to either a specific commit where you've left off or to the point where you started your work on the branch.

```
git reset origin/main
git reset < SHA-VALUE >
```

What this will do, is collect all the changes made in those commits in between and bring them back into the working directory. From here, the commits can be rewritten to better describe the addition of each piece and provide the intended implementation with the changes appropriately grouped in an easy to follow sequence.

3. If there is more to be done, commits can revert back to in-progress style and be cleaned up again by resetting to the most recent finished commit through reference to its SHA value.

Some additional features that can be used is to use the "patch" option to stage the changes of part of a file. This can help in creating atomic commits when revising a bigger set of changes in a single file.

```
git add --patch
```
or
```
git add -p
```

Another feature that can be implemented to assist in stepping through these commits while testing the functionality is to use the "stash" feature.

```
git stash
git stash pop
```

If there is a quick change that you find you want to make to the most recent commit, there is also the option to amend. This is helpful when it is available, but is only an option for editing the most recent commit. The process is similar to any other commit, you would add the changes and then issue a commit, but this time with the "amend" option instead of a message.

```
git add
git commit --amend
```

4. When the feature is implemented and work is ready to be shared, all that will need to be done is to finish cleaning up the last set of commits, pushing to the remote repository (if working with others), and creating a pull request.
