---
title: Git Basic Usage
subsection: git
order: 2
---

# Basic Git Usage


## Cloning Git Repository
Open up a terminal in a directory where the repository would be cloned. Execute the following command (with additional parameters if needed to accommodate custom-named SSH keypair files) to clone the fork repository.

```
git clone https://src.fedoraproject.org/rpms/hello.git
```

Navigate into the cloned repository and feel free to pick an IDE and code editor of your choice to start working on the code.

## What is git-branch ?

A Git branch is a version of the repository that diverges from the main working project. It is a feature available in most modern version control systems. A Git project can have more than one branch.


## Listing Branches

Listing a branch in Git is simple.


Show local branch(es)
```
git branch
```

Result:

```
* master
foo-branch
foo-branch-2
```

Show All branch(es) including local branches

```
git branch -a
```
Result:

```
  master
  foo-branch
  foo-branch-2
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
  remotes/origin/foo-branch
  remotes/origin/foo-branch-2
  remotes/origin/foo-branch-3

```

## Creating Branches

Let’s go through a simple example of branching workflow that you might use in the real world.Once create new branch it will give us current branch we have in our repository.Give it a name appropriately. For instance, a branch consisting of work you doing it.



Create branch
```
git branch branch-foo
```

Switch to new branch

```
git checkout branch-foo
```

Create and switch to new branch (shorthand)

```
git checkout -b branch-foo
```

#### Useful Tip
* Be sure to NOT work on the primary branch of the repository, which is `master` in this case. Keep the primary branch aside as a reference branch to create new branches out of and fallback to in case of scrapping. For example If you work on something like "foo-feature" you should name your branch  `foo-feature`.

```
git checkout -b foo-feature
```

## Git Status

After on the working on the code, execute the following command to know about the changes made with additions, removals and modifications made in the tracked and untracked files.

```
git status
```

## Git Add

Stage the changes of similar kind by executing the following command to prepare them to be committed. Please note that multiple changed files can be staged for single commit, but it is strongly recommended to keep dissimilar changes as separate commits.

```
git add <file-that-was-changed>
```

Stage all changes at once

```
git add .
```

## Git Commit

Commit the staged changes to the checked out branch of your locally. The commit message should be representative of the changes made  in the said commit and preferably be under 50 chars.

```
git commit -sm "<appropriate-commit-message>"
```

## Git Push

In order to reflect the locally made changes to your remote fork, the changes must be pushed. If there is no upstream branch available for the currently checked out local branch - which is generally the case when new branches are created locally, push can be made by executing the following command.

```
git push --set-upstream origin <branch-name-according-to-what-would-be worked-on>
```

Once an upstream branch is available for the currently checked out local branch - which is generally the case after the above command has been executed, push can be made by executing the following command.

```
git push origin <branch-name-according-to-what-would-be-worked-on>
```

## Git Pull

There are cases you want to view some changes wich are already in your fork (e.g. modified using Github WebUI). We're using variables holding your remote and branch names:

If you already have branch in your computer your can just pull via "git pull"

```
# Pulls curent branch commits from remote
$ git pull 
```

If you don't have remote branch in your computer then you can fetch the changes from your fork:

```
$ git fetch remote-branch
```

And then checkout the branch:

```
$ git checkout -b new-branch-name -t $remote/$branch 
```

## Git Rebases

To update the `foo/` directory, switch to that directory, make sure you are on your development branch and rebase on the latest stuff:

```
$ cd foo
$ git checkout my-devel-branch
$ git fetch origin
$ git rebase origin/master
```

If conflicts occured, you need to resolve them, and continue with rebase.

```
$ nano file/that/has/conflict.md
# properly adjusted / edited to show correct foo-content
$ git add file/that/has/conflict.md
$ git rebase --continue
``` 