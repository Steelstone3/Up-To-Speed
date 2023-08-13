# Git Usage

Git is a very powerful version control with many features. There can also be a few ways to do the same things at times.

This article can act as a guide through the maze that can sometimes be git.

## Basics

### git status

Using git status checks the current state of the branch.

### git log

Provide a historical log of all the commits on the current branch

### git checkout your-branch

Switches you from one the current branch to the target branch. For example you are on "apples" branch and you want to change to "your-branch" you'd run

> git checkout your-branch

#### git checkout -b your-branch

Creates a branch from your current branch then checks out to it

The same as

> git checkout trunk
>
> git branch your-branch
>
> git checkout your-branch

Example

> git checkout trunk
>
> git checkout -b your-branch

In both cases would create "your branch" from trunk

### git branch

Provides a list of the local branches in alphabetical order with the one currently being worked on highlighted.

For example

> branch-name
>
> some-other-branch
>
> **the-one-you-are-working-on**
>
> your-branch

#### git branch --all

All branches option will show all the branches related to the current repository's project.

For example

> branch-name
>
> some-other-branch
>
> **the-one-you-are-working-on**
>
> your-branch
>
> origin/your-branch
>
> origin/main

#### git branch your-branch

Creates a branch from your current branch.

Example

> git checkout trunk
>
> git branch your-branch

Creates a branch called your-branch from trunk

#### git branch -d your-branch

DANGEROUS! Deletes a specified branch

Example

> git branch -d your-branch

Deletes your-branch

> git branch -D your-branch

Deletes your-branch with force meaning that whether you had changes on there or not it is gone permanently

### git clean

DANGEROUS! Cleans up the local branch of clutter that aren't included in the remote branch. Can loose work in progress from doing this so be careful.

Example

> git clean -d -f -x

Will remove the following from the project repository

-d recurse into directories to remove those
-f force to allow it to delete files and directories
-x remove untracked files

I use this after "git checkout develop" personally and not much else

## Iterative Steps

### "git add ."

Stage all currently untracked files

Example

> git status
>
> git add .

Adds all the files that are currently untracked on the current branch "your branch"

### git commit

Commits the currently staged files

Example

> git status
>
> git add .
>
> git commit -m "Added a controller to the flux capacitor class"

Creates a commit with the message "Added a controller to the flux capacitor class"

## Getting The Latest

### git fetch

Synchronises the remote cached branches (origin/your-branch) with the latest on remote (origin your-branch). This command will have no impact on local branches (your-branch).

For example

If a new branch has been made it will add it to the remote branches list.

> new branch created origin/your-branch

It will synchronise branches with the latest so the likes of origin/develop will now be up to date with the latest changes.

> updated branch origin/develop

#### git fetch --prune

Allows git fetch to remove remote branches that have been deleted from remote and can be set as a configuration option to do this automatically on "normal" git fetch.

For example

In the remote repository (bitbucket) the branch "your branch" is deleted

> git fetch --prune
>
> removed branch origin/your-branch

### git rebase origin/trunk

Updates "your branch" by placing the commits on top of the "target branch".

Can cause merge conflicts. In such a case run "git rebase --abort" branch off "your branch" to "your branch merge conflicts" then proceed from there.

Example

> git fetch
>
> git rebase origin/trunk

Will rebase the current branch you're on onto the cached remote "trunk" latest

#### git rebase --onto your-branch origin/trunk

Rebase can be used to rebase a branch you're not currently on by using the --onto option

Example

> git fetch
>
> git rebase --onto your-branch origin/trunk

Will rebase "your branch" onto cached remote "trunk" latest

#### git rebase --continue

Continue with the next step of the rebase

### git pull --rebase origin trunk

> git pull --rebase origin trunk

Performs the equivalent of

> git fetch
>
> git rebase origin/trunk

In one step. Rebasing on git pull can be set as a default in your git config.

## Updating Trunk

### git push

Pushes your local changes to the remote branch

You can also specify a location to push the changes to.

> git push origin your-branch

Useful in cases when you are working on a branch with a different name such as "your branch merge conflicts"

#### git push --force

DANGEROUS! Only use git push with force on a feature branch NEVER trunk. Replaces whatever was on the remote branch with whatever was on the local branch.

## Disaster Recovery

### git reset --hard

DANGEROUS! Resets changes to the latest commit on your branch with force. Any untracked changes will be lost

Example

Can be used as disaster recovery from merge conflicts like so...

(on "your branch" with merge conflicts when trying to merge to "trunk")

> git push // The working version with merge conflicts
>
> git pull --rebase origin develop
>
> git rebase --continue // Compiled but in testing found feature didn't work as intended and the merge conflict is the cause
>
> git reset --hard origin/your-branch // The working version with merge conflicts

### git rebase --abort

Resets the branch to pre-rebase attempt when mid-rebase.

Example

> git push // The working version with merge conflicts
>
> git pull --rebase origin develop
>
> git rebase --continue // Happy with the resolved merge conflicts so far
>
> git rebase --abort // Something went wrong during one of the merge conflicts

In the example on the second part of the merge conflict resolution something went wrong so the developer used "git rebase --abort" to put the branch back to a pre-rebase state.

Ask for help with merge conflicts if you get stuck.
