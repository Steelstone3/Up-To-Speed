# Efficiency With Git Usage

## Configuration

Making git an efficient tool to work with is important. One of the ways to go about this is to create a git configuration:

### Example Global Configuration

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
> \# helper = cache --timeout 60
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

### Example Local Configuration

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

### Configuration Commands

The configuration can be set up using git commands. For example:

> git config --global core.editor "hx"

## Aliases

Aliases are a powerful way of using common git commands. They shorten the time taken to execute specific commands.

### Example Usage

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

### Checking Current Aliases

To see anything currently aliased:

> git config -l | grep alias
>
> git config --get-regexp ^alias

### Example Configuration

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

### Aliasing Commands

Alias can also be added using commands such as

> git config --global alias.co checkout
>
> git config --global alias.br 'branch --all'

Say something was aliased in the configuration that you want to remove

Find the alias then run this command

> git config --global --unset alias.the_alias_in_question

This is a typical alias configuration. There are no standards per say when it comes to git aliases.
