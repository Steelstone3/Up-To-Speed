# Disaster Recovery Plan

If you are clever about it this can all be done on one branch but requires more advanced git knowledge.

You want to **keep the remote of "origin/your branch" with the merge conflicts** until you are completely satisfied. This will act as your disaster recovery.

## Rebasing Onto Trunk

For the local "your branch" you'll want to rebase onto the latest changes in "trunk"

It is a good idea to squash your changes in "your branch" which will mean less changes to rebase.

> git branch
>
> git checkout your-branch
>
> git pull --rebase origin develop

Or

> git fetch
>
> git branch
>
> git checkout your-branch
>
> git rebase origin/develop

Or

> git fetch
>
> git rebase --onto your-branch origin/develop

Note that there can be many ways to accomplish the same thing with git.

## Resolving The Conflicts Disaster Recovery

Start to resolve the conflicts.

In the case you are happy with the resolved merge conflicts use

> git rebase --continue

In the case something went wrong mid rebase use

> git rebase --abort

In the case you complete the rebase and start to test the build to find a problem you may want to use

> git reset --hard origin/your-branch

When you are completely happy and haved tested the build then and only then use

> git push

## Using Branches

This same process applies if you branched off "your branch" with "your branch merge conflicts" except for some small differences

In the case you complete the rebase and start to test the build to find a problem you may want to use

> git branch
>
> git checkout your-branch
>
> git checkout -b your-branch-merge-conflicts-attempt-2
>
> git branch

Or

> git branch
>
> git checkout your-branch
>
> git branch your-branch-merge-conflicts-attempt-2
>
> git checkout your-branch-merge-conflicts-attempt-2
>
> git branch

Both do the same thing creating a new branch from "your branch"

When you are completely happy and haved tested the build then and only then use

You'll have been working on and solved the merge conflicts on "your branch merge conflicts" you now need to push to "your branch"

> git push origin your-branch
