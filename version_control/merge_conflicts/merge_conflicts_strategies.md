# Merge Conflicts Strategies

## Git Strategies

There are a number of git strategies that makes resolving merge conflicts less painful.

### Avoidance

The ultimate strategy is to try to avoid merge conflicts all together.

#### Make The Commit Surface Area Small

When developing code only make and commit essential changes. In cases where there are things you would "like to do" make a new branch from "trunk" and do them there.

Reducing the surface area reduces the chance another developer will be working in the same area and thus reduce the chance of a merge conflict.

#### Make Small Iterative Changes

This is all about not keeping a long running branch. The longer the branch runs the more changes are made on "trunk" relative to "your branch".

The larger the changes between "your branch" and "trunk" the harder it will be to work out what needs to go in when resolving the merge conflict and the likelhood of merge conflicts arising.

In addition it is easy for the pull request reviewer to review a "part 1, 2, 3" type pull request than one large feature with many changes.

For a general rule of thumb break down the "big feature" aim for a "sub feature" and try to merge that into "trunk" keeping the branch running for around no more than a week.

### Looks Like Its Merge Conflict Time

#### Teamwork Makes The Dream Work

Sometimes as a developer you know that yourself and another developer (or team of) will be working in an area and causing merge conflicts.

In such cases make and push to a "staging branch" and resolve the merge conflicts as a team for this branch. The staging branch can be merged into "trunk" regularly and then continued to be worked on.

This strategy uses the philsophy of a "problem shared is a problem halved" in the sense that both developers will know what changes are important to them and when the conflicts arise will better be able to communicate what is essential and where it needs to go.

#### Branches Are Cheap

When you get a merge conflict create a new branch from "your branch" call it something like "your branch merge conflicts" then fix the merge conflicts on this branch. Then push "your branch merge conflicts" onto "your branch".

In this way if anything goes wrong during the process of fixing merge conflicts on "your branch merge conflicts" you have a master copy to "disaster recovery" from. Simply make a new branch from "your branch" called something like "your branch merge conflicts attempt 2" and try again.
