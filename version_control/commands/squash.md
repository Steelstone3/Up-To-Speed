# Squash

## Introduction

Git squash is a tricky command to use on the command line. This article will provide a tutorial on how it is used

## Git History

Before you can squash you'll need to find the commit that you want to squash up to. To find this use...

> git log --oneline

This will produce a list of commits for example

> 70e44f2 Update main
>
> 3ceec9e Update controller
>
>c7ce01b create view

So on

## Using Squash

Squash effectively rebases commits onto commits. Therefore we will use the following command to start a squash...

> git rebase -i HEAD~10

Lets break this command down

### -i

This command option runs rebase in "interactive mode". Interactive mode will bring up a text editor. 

Each commit in "interactive mode" will have "pick" next to it. 

In order to squash change all "pick" apart from the top commit to "squash" or "s". Use find and replace for this. 

"reword" or "r" will let you rename a commit. You should do this for the first one (optional).

### HEAD~n

How many commits back from and including the first commit you want to squash.

> 70e44f2 Update main
>
> 3ceec9e Update controller
>
>c7ce01b create view

HEAD~3 in this case would squash all the commits

HEAD~2 in this case would squash Update controller into Update main
