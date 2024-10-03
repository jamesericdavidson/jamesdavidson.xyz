---
# image: ""
date: 2024-10-03
description: "It's like Git for Dummies..."
draft: true
showTableOfContents: true
slug: "learn-git-from-the-terminal"
tags: [ "git", "version control", "linux" ]
title: "Learn Git: From the Terminal"
type: "post"
---

## Introduction

Instead of learning multiple Git interfaces (with UX that can differ *greatly* from mainline Git), I think you should learn the command line utility instead.

Don't go running yet! Here's how easy it is:

## Common Git commands

### checkout

Move between branches, or create new branches.

```sh
# Checkout the existing main branch
git checkout main

# Create the dev branch
git checkout -b dev

# Checkout the last used branch (in this case, main)
git checkout -
```

### branch

View local and remote branches, rename branches, and delete branches.

```sh
# View branches
git branch
# Display the latest commit hash and commit message next to each branch
git branch -v

# Rename a branch
git branch -M main

# Delete a branch
git branch -D dev
```

## Putting it all together

### cherry-pick

Committed to the wrong branch? Copy your commit into a new branch, then remove the commit from the original branch.

```sh
# Assuming your commit is at the HEAD, and the branch hasn't been pushed
commit-id=$(git rev-parse HEAD)
git checkout my-new-branch
git cherry-pick $commit-id
git checkout my-original-branch

# This will checkout any changes in the working directory, and remove any
# untracked files
git reset --soft HEAD && git restore --staged . && git checkout . \
    && git clean -f
```

## Further Reading

Git has great documentation; I suggest following the [Pro Git Book](https://git-scm.com/book/en/v2), in addition to terminal tools such as:

```sh
man git-submodule
# Use man -K to find the Git man pages you need
man -K git

# Install a tldr implementation (such as tealdeer), and access a handy
# reference of Git commands
tldr git-checkout

# Cheat is similar to tldr, but is typically less useful for most programs
cheat git
```
