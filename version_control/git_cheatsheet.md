# Git Cheat Sheet

This is a cheat sheet summary of some of the main git commands

## Basics

> git status (Using git status checks the current state of the branch)
>
> git log (Provide a historical log of all the commits on the current branch)
>
> git checkout your-branch (Switches branches)
>
> git checkout -b your-branch (Creates a branch from your current branch then git checkout to it)
>
> git branch (Displays local branches and highlights the current branch)
>
> git branch --all (Displays all branches and highlights the current branch)
>
> git branch your-branch (Creates a branch from your current branch)
>
> git branch -D your-branch (DANGEROUS! Deletes a specified branch)
>
> git clean -d -f -x (DANGEROUS! Cleans up the local branch of clutter that aren't included in the remote branch)

## Iterative Steps

> "git add ." (Stage all currently untracked files)
>
> git commit (Commits the currently staged files)

## Getting The Latest

> git fetch (Synchronises the remote cached branches (origin/your-branch) with the latest on remote (origin your-branch))
>
> git fetch --prune (Allows git fetch to remove remote branches that have been deleted from remote)
>
> git rebase origin/trunk (Rebase the current branch onto the base branch)
>
> git rebase --onto your-branch origin/trunk (Rebase the specified branch onto the base branch)
>
> git rebase --continue (Continues the rebase process)
>
> git pull --rebase origin trunk (Updates the your branch by placing commits onto a base branch)

## Updating Trunk

> git push (Pushes local changes to the remote branch)
>
> git push origin your-branch (Pushes local changes to a specified remote branch)
>
> git push --force (DANGEROUS! Replaces whatever was on the remote branch with whatever was on the local branch)

## Disaster Recovery

> git reset --hard (DANGEROUS! Resets to current branch HEAD)
>
> git rebase --abort (Aborts the rebase process)
