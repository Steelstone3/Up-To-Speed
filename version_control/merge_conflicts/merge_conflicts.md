# Merge Conflicts

## Discovery

When developing within a team "main", "develop", "master" known as the trunk branch has changes going into it all the time from developers.

Rebasing "your branch" onto "trunk" (remote main/ master/ develop) often goes smoothly. Most of the changes will go in automatically (where no rival implementation exists).

If however, two developers happened to have worked in the same file on the same lines merge conflicts occur. Commonly this can happen when adding "using" statements at the top of the file to bring in dependencies or other classes. In rarer cases this can happen within methods which requires more caution.

Without rebasing "your branch" when you push the branch and make a pull request to "merge into trunk" you'll sometimes see the message of "merge conflicts" this means an automatic merge from "your branch" into "trunk" isn't possible until the "merge conflicts" are resolved.

## Getting Started

Firstly create a branch to resolve the conflicts on

> git branch
>
> git checkout -b "your-branch-merge-conflicts"

This will leave you with a "backup" branch in "your branch" that won't be touched during this process that we can use for "disaster recover" whilst resolving merge conflicts

Next squash the commits on "your branch merge conflicts" as this makes rebasing easier

After that rebase "your branch merge conflicts" onto "trunk"

> git pull --rebase origin develop

See [merge_conflicts_distaster_recovery_plan.md](./merge_conflicts_distaster_recover_plan.md) for more information on disaster recovery.

## Graphical Tools

To resolve merge conflicts developers often use graphical conflict resolution tools.

There are many tools that you can use for this.

See [VS2022 Merge Editor](<https://learn.microsoft.com/en-us/visualstudio/version-control/git-resolve-conflicts?view=vs-2022>) for a guide to using the inbuilt conflict editor in your IDE.
