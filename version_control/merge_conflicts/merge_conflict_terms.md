# Merge Conflict Terms

## Understanding Conflict Resolution Terms

It depends on the type of operation (merge or rebase) leading to that conflict.
When you are trying to resolve conflicts in Git, you are typically dealing with two sets of changes:

### Changes from your Current Branch

Often the branch you are currently working on or have checked out. In your explanation, this is described as "what you have" or "the destination of the merge".

### Changes from the Incoming Branch

The branch you are trying to merge into your current branch (during a merge) or the branch you are attempting to apply on top of another branch (during a rebase). This is "what you merge" or "the source of the merge".

### VSCode Accept Incoming changes

That will discard the conflicting changes from your current branch ("what you have") and keep the changes from the incoming branch ("what you merge").

### VSCode Accept current changes

That will keep the conflicting changes from your current branch ("what you have") and discard the changes from the incoming branch ("what you merge").

## Summary Of Merge Conflict Terms

It is important to understand that during a rebase, the roles of "current branch" and "incoming branch" are essentially reversed. In a rebase, your current branch is being applied on top of the incoming branch. So, when faced with conflicts:

### "Current changes"

During a rebase will refer to the branch onto which you are rebasing (usually the base branch).

### "Incoming changes"

During a rebase will refer to the branch that you are trying to rebase (the changes you are attempting to apply on top of another branch).
