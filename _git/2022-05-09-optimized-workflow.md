---
layout: post
title: "How to Incorporate Git into an Optimized Workflow"
author: skylar_lynner
---

Git is known for its ability to provide version control, but it can also
be used as a tool to aide in building a focused workflow. With a simple
writing process, it is easy to add functionality to a project
incrementally that allows for easy review of work and provides focus on
the tasks that need to be accomplished.

The stages of the workflow will work in three parts:
* Writing
* Staging
* Revising

### Step 1: Writing
Similar to writing a paper in school, it will be important to start with
an idea of what needs to be written. Taking the time to initially analyze
the steps needed to accomplish the task will assist in simplifying the
overall process. Some initial practices that can start to build this stage
can include sketching initial class and sequence diagrams for those who
are familiar or it can be as simple as opening a text file and creating
a list of the incremental tasks needed to accomplish the goal.

With an idea of the tasks needed to accomplish the goal, the goal is to
know what needs to be written before starting to write. This practice can
be paired well with Test Driven Development strategies by writing the test
for the functionality first. For each step in writing, review the changes
made and stage them into commits. Create descriptive commit messages that
can serve as a working timeline of what was written that can be stepped
through one change at a time. These commits need not be final, as they can
be squashed or even rewritten entirely.

While Git is usually seen just for its ability in version control, it can
provide a useful debugging tool for those who tend to get lost in writing.
If there is a question about what's been written and what might be
missing, all changes can be viewed using the diff functionality. This
brings attention to new changes and can help identify areas where
something may have been missed.

### Step 2: Staging
Once some functionality has been added to the project, it might make sense
to start revising and cleaning up commits. This can be a good time to
review all changes, identify commits that can be grouped together if there
are smaller similar changes made across multiple areas or to group changes
that work together to implement some part of the functionality.

One option for staging these commits is to reset and rewrite them into
cohesive, atomic commits that are ready to share with others. This can be
a useful opportunity to review what changes have been made and consider
possible refactoring to increase readability. Once the changes are
added into the new commit structure, functionality is implemented, and
the new testing validates what has been written, either the next step in
writing can be added by revisiting the writing stage or the branch can be
prepared to share with others in the next step.

### Step 3: Revising
If there are additional changes to incorporate from the main branch of the
project, this can be done by rebasing the branch or by simply merging the
changes if there's significant enough change. After ensuring that the
branch is updated, a pull request can be made. The resulting pull request
will now have changes that are easy to review and with the additional
attention to updating changes from main, ideally there will be minimal, if
any, merge conflicts to resolve.

The time taken to revise the workflow into cohesive commits allows for
code that communicates what it intends to do and a commit history that
compliments the changes by providing a clear description of through the
log of commit messages.

## Read Further

[Git Organized: A Better Git Flow](https://dev.to/render/git-organized-a-better-git-flow-56go)
