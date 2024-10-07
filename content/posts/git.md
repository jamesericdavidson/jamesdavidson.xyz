---
date: 2024-10-06
description: "It's like Git for Dummies..."
draft: true
image: "/image/git.svg"
showTableOfContents: true
slug: "learn-git-from-the-terminal"
tags: [ "git", "tutorial", "linux" ]
title: "Learn Git: From the Terminal"
type: "post"
---

![Orange Git logo](/images/git.svg)

## Introduction

Instead of learning multiple Git interfaces (with UX that can differ *greatly* from mainline Git), I think you should learn the command line utility instead.

Don't go running yet! Here's how easy it is:

## Concepts

- `HEAD`

    The latest commit is equal to `HEAD~1` or `HEAD^`.

- `.gitignore`

    Git subcommands (e.g. `add`, `rm`) will ignore patterns listed in this file.

## Commands

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

### commit

Commit changes.

UNIX options can be grouped, e.g. `git commit -p -v` can be expressed as `git commit -pv`.

```sh
# Commit staged changes, then set the commit message using GIT_EDITOR
git commit

# Set the commit message inline
git commit -m 'chore: init'

# Automatically stage modified and deleted files
git commit -a

# Use the patch interface to selectively stage file hunks
git commit -p

# Show the git diff underneath the commit message
git commit -v

# Amend commit contents, and the HEAD commit message
git commit --amend

# Amend the commit contents only
git commit --amend --no-edit
```

### push

Update remote branches. Changes must be [committed](#commit) first.

```sh
# Push the checked out branch
git push

# Push an arbitrary branch
git push my-pet-branch

# Added the remote as origin, but not tracking the branch upstream yet?
git push -u origin $(git branch --show-current)

# Push all tags
git push --tags
```

### pull

Fetch remote branches and tags.

```sh
# Fetch changes from origin's remote tracking branch
git pull

# Fetch changes from another remote tracking branch
git pull my-repository

# Fetch remote tags
git pull -t
```

### tag

Create, delete and list tags.

```sh
# List tags
git tag

# Create a tag at HEAD
git tag v0.1.0

# Create a tag at commit-id
git tag v0.1.0 $commit-id

# Delete tag
git tag -d $tag-name
```

### rm

Remove files from the index.

```sh
# Remove file
git rm path/to/file

# Recursively remove files from a directory
git rm -r path/to/directory

# Force remove file
git rm -f
```

### submodule

Add, remove and list submodules.

```sh
# List all submodules
git submodule

# Add a submodule
git submodule add $repository path/to/submodule

# Initialise all submodules
git submodule init

# Unregister a submodule
# Can be paired with git rm -r path/to/submodule to remove the submodule from
# .gitmodules
git submodule deinit path/to/submodule

# Update all submodules recursively from remote, and initialise any
# unregistered submodules
git submodule update --init --remote --recursive
```

### add

```sh
# Stage file contents or modifications
git add path/to/file

# Recursively stage directory contents
git add path/to/directory

# Use the patch interface to selectively stage file hunks
git add -p
```

### remote

```sh
# List remotes by name
git remote

# List remote URLs
git remote -v
```

### rebase

Rebase the git history.

Useful for amending commits older than the latest commit.

```sh
# Interactively rebase the current branch using GIT_EDITOR
git rebase -i

# Rebase the last n commits (best used for untracked branches)
git rebase -i HEAD~n

# Rebase branch-name
git rebase -i my-branch
```

### show

Display the diff of the latest commit.

```sh
# Show long commit-id, commit author, and commit message
git show

# Show short commit-id; don't show commit author, or commit message
git show --oneline
```

### log

Display history for the current branch.

```sh
# Show long commit-id, commit author, and commit message
git log

# Show git diff
git log -p

# Show short commit-id and commit message; don't show commit author
git log --oneline
```

### merge

```sh
git merge
git merge --squash
```

### mv

```sh
#
git mv
```

### diff

```sh
#
git diff

#
git diff --cached
```

### clone

```sh
git clone
git clone --recurse-submodules
```

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

Git has great documentation; I suggest following the [Pro Git Book](https://git-scm.com/book/en/v2), in addition to the `man` pages, and `tldr`.

Moreover, it's worth defining your Git strategy...

<!-- Conventional commits, feature branches, atomic commits, versioning... -->
