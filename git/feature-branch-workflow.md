# How to Create an Optimized Git Workflow

Git can be difficult to manage initially, but using its structure to build a
workflow can provide benefits in managing overall insight and structure into
your development approaches. Learning Git is often deferred until after some
comfort in at least one language, but it can be a very useful tool for anyone
looking to ease some of the frustration in learning the tools necessary for
writing a new project.

Similar to a [Kanban board](https://www.atlassian.com/agile/kanban/boards),
the stages of your workflow will work in three parts:
* Writing
* Staging
* Revising


### Step 1: Writing
Set out with an intention of what you plan on writing. This is best done with
attention to making incremental, progressive implementation.

With one feature in mind, create a new branch and start writing. The goal is
to know what you want to write before writing, this can work well with using
Test Driven Development strategies to ensure that there is direction and
clarity with what will be written. Another strategy is to create a structure
of comments for each step that will be written and using it as a guide.

Periodically step back and review the changes you've made. For each step in
writing you make, review the changes and create commits along the way that
reflect the incremental changes made while building up the new feature.
Describe the step that was done in the commit messages along the way, these
commits can be excessively incremental, think of them as a working timeline of
what was written that can be stepped through one change at a time.

### Step 2: Staging

Once some of the groundwork is built in the branch, it may make sense to clean
some of the commits along the way. If a few pieces of a change were written
into multiple commits, it can be helpful to rewrite some of these commits to
group some of the smaller changes together. This can also be useful if a few
changes work together to implement some functionality.

One option for staging these commits is to reset and rewrite them into
cohesive, atomic commits that are ready to share with others. This can be a
good point to look over changes made and consider some refactoring to increase
readability.

The branch can be reset to a previous commit, which will shift all changes
into the working directory. These changes can be staged into commits that
describe the steps taken to build the functionality. Once changes are recorded
into a new commit structure, either return to adding functionality to the
feature or proceed with final revising. This can also bring an opportunity to
merge changes from the main branch of the project if they haven't previously
been added.

### Step 3: Revising
Some additional features that can be used is to use the "patch" option to stage
the changes of part of a file. This can help in creating atomic commits when
revising a bigger set of changes in a single file.

```
git add --patch
```
or
```
git add -p
```

Another feature that can be implemented to assist in stepping through these
commits while testing the functionality is to use the "stash" feature.

```
git stash
git stash pop
```

If there is a quick change that to make to the most recent commit, there is
also the option to amend. This is helpful when it is available, but is only an
option for editing the most recent commit. The process is similar to any other
commit, but with the amend option rather than a commit message.

```
git add
git commit --amend
```

When the branch's functionality is written and revised into cohesive commits,
the branch can be reviewed by others by using a pull request. The time taken
to revise the workflow to build the commit history this way allows for code
that communicates what it intends to do and a commit history that provides a
descriptive log of changes.


## Read Further

[Git Organized: A Better Git Flow](https://dev.to/render/git-organized-a-better-git-flow-56go)
