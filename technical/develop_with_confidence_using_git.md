# Develop With Confidence Using Git

## Using Command Line Git

Command line git is a very efficient tool even over graphical frontend. It has a number of key advantages

- Consistent
- Fast
- Simple
- Accurate
- Precise

This is to say command line git can execute commands as described above.

Command line git also comes with some disadvantages.

- Initial learning curve
- Dangerous commands have no warnings

Certain commands are dangerous to use and will lose "commit history" it is important to "RTFM" as this guide hopes to de-mystify git.

Git commands with --hard, --force usually come with risk associated with it.

Some commands to be aware of:

> git push --force

Will overwrite commit history regardless of whether the branch is up to date.

> git push --force-with-lease

Will overwrite commit history but will check the remote branch is up to date.

> git reset --hard

Will loose any current changes not committed.

## Developers Are *Indecisive*

As a developer how many times have you come across a situation of uncertainty with which direction to take a feature on a codebase.

I myself can name numerous examples.

Sometimes this indecision can be thought through and a solution reached.

Maybe the blocker came from unclear direction or requirements that can be discussed.

However sometimes the situation of indecision comes from a technical implementation.

I would make the case that git eliminates the technical indecision.

## Code Without *Indecision*

How can we then code without indecision as it pertains to git?

Git is a form of version control. I like to conceptualise version control as a checkpoint system in video games.

If we think to that for a moment. Lets imagine a branch with committed work that up to this point has a degree of certainty in design decisions made. Lets call this branch "design-happy".

Lets suppose a few design directions present themselves. How can we tackle the uncertainty?

Say there are two design paths that you could go down "design-path-a" and "design-path-b".

### Decision Branching

One such method is to use branching.

Start by branching from "design-happy" to "design-path-a"

> git checkout design-happy
>
> git branch design-path-a
>
> git checkout design-path-a

Start working down this path. If it works out merge it back into the original branch "design-happy".

> git add --all
>
> git --message "a commit message"

Otherwise checkout to "design-happy" and then create the branch "design-path-b"

> git checkout design-happy
>
> git branch design-path-b
>
> git checkout design-path-b

If "design-path-b" works out to be a worse path than "design-path-a" then the option to merge "design-path-a" is still available.

This is the main advantage with this approach.

### Stash and Start Again

For smaller design decisions the following may make for a better approach.

Remain on "design-happy" and continue to work on a commits worth of work.

If the design is not heading in a direction that is desirable then stash the current work.

> git stash save "design not happy"

If when redoing the work you were happier with the original the work can be retrieved using the following.

> git stash list
>
> git stash pop stash@{1}

## Implementing Code Changes Within A Team

As a version control git deals with the changes to a codebase.

Sometimes however, changes don't automatically integrate. This occurs where two or more developers work in the same area of code and the changes will need to be integrated.

### Avoidance

The best strategy for avoiding merge conflicts in a team is clear communication in the area of work. This can be achieved by daily stand up ceremonies and pair programming.

Regular rebasing with the branch to be merged with using

> git pull --rebase develop-branch

This will ensure the divergent changes are reduced if any occur.

### Merge Conflicts

Some point inevitably merge conflict will occur so lets discuss strategy.

First things first a cheap and easy backup by creating a new branch

> git branch branch-name-rebase
>
> git checkout branch-name-rebase

Next is to pull in the changes from the main development branch

> git pull --rebase origin develop

Fix the first merge conflict using a merge conflict tool

> git rebase --continue

If part of the process of fixing merge conflict goes wrong then use

> git rebase --abort

If however the entire merge is complete and something has gone irrecoverably wrong **BEFORE** "git push --force-with-lease" use

> git reset origin/branch-name

If however you did push by accident the use the original branch to restore from

> git checkout branch-name
>
> git branch branch-name-rebase-2
>
> git checkout branch-name-rebase-2
>
> git pull --rebase origin develop
>
> git rebase --continue

Hence why the first step is important

## Efficiency With Git Usage

### Configuration

Making git an efficient tool to work with is important. One of the ways to go about this is to create a git configuration:

#### Example Global Configuration

Git configurations come in two parts local to the repository and global. For now we'll just focus on the global configuration.

To access the global configuration use the following command:

> git config --global --edit

An editor will then pop up. Use the following as an example:

> [push]
>
> autoSetupRemote = true
>
> [pull]
>
> rebase = true
>
> [credential]
>
> helper = store
>
> helper = cache --timeout 60
>
> [rebase]
>
> autoStash = true
>
> [user]
>
> email =
>
> name =
>
> [core]
>
> editor = hx

The example lays out some important configurations.

> pull.rebase = true

This configuration makes it so that git pull by default uses rebase. This keeps the commit history linear.

> user.email = "<Company@Company.co.uk>"
>
> user.name = "Skippy"

Sets up a git username and email

> core.editor = hx

Sets up the text editor you wish to use with git

> credential.helper = store
>
> credential.helper = "cache --timeout=3600"

Determine whether to store access credentials permanently or with a set timeout

#### Example Local Configuration

To access the local configuration use the following command:

> git config --edit

Local configurations can contain overrides to the global configuration such as:

> pull.rebase = false

However usually they revolve around storing and managing information linked to the specific repository

For example:

> [remote "origin"]
>
> url = <https://github.com/Steelstone3/Up-To-Speed.git>
>
> tch = +refs/heads/\*:refs/remotes/origin/\*
>
> [branch "main"]
>
> remote = origin
>
> merge = refs/heads/main
>
> [branch "blog"]
>
> remote = origin
>
> merge = refs/heads/blog

The most important parts about the local configuration is that the remote "origin" is setup correctly

> +refs/heads/\*:refs/remotes/origin/\*

For most repositories ensuring fetch is setup as so ensures you'll fetch all remote branches. There will be times when this isn't so such as during a shallow clone where you may need to set it correctly when you unshallow the repository.

> url = the-remote-repository

This setting is used to ensure that your remote repository is setup correctly. You may need to change this if you move to using SSH or move remote repository location entirely.

> branch "blog"

The settings surrounding a branch are also important you can have more than one remote repository set ([remote "origin"] [remote "origin-2"]). Ensure this matches the desired destination and the merge option matches the local branch name.

the branch names match the merge option.

#### Configuration Commands

The configuration can be set up using git commands. For example:

> git config --global core.editor "hx"

### Aliases

Aliases are a powerful way of using common git commands. They shorten the time taken to execute specific commands.

#### Example Usage

Something like this:

> git add --all
>
> git commit --message "reasonable commit message"
>
> git pull --rebase origin develop
>
> git push

Could become something like:

> git a
>
> git c
>
> git pl
>
> git pu

#### Checking Current Aliases

To see anything currently aliased:

> git config -l | grep alias
>
> git config --get-regexp ^alias

#### Example Configuration

In the git configuration file add the following appended to bottom of the file:

> [alias]
>
> ce = config --edit
>
> ceg = config --global --edit
>
> clf = clean -d -f -x
>
> co = checkout
>
> br = branch
>
> a = add --all
>
> c = commit --message \"update\"
>
> st = status
>
> d = diff
>
> pu = push
>
> pf = push --force-with-lease
>
> pl = pull --rebase
>
> l = log --pretty=oneline
>
> ll = log
>
> f = fetch --prune
>
> ri = rebase --interactive
>
> rc = rebase --continue
>
> ra = rebase --abort

#### Aliasing Commands

Alias can also be added using commands such as

> git config --global alias.co checkout
>
> git config --global alias.br 'branch --all'

Say something was aliased in the configuration that you want to remove

Find the alias then run this command

> git config --global --unset alias.the_alias_in_question

This is a typical alias configuration. There are no standards per say when it comes to git aliases.
