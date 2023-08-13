# Git Aliases

## Introduction

Welcome to the true power of git on the command line. I strongly recommend you get used to the standard commands before proceeding with the following instructions for setting up git aliases.

## Setup Part 1

Add the following to you git configuration. This will appear under the "[alias]" key

> git config --global alias.co checkout
>
>git config --global alias.br branch
>
>git config --global alias.c commit
>
>git config --global alias.a add
>
>git config --global alias.st status

These config changes are fairly safe and are good for practicing the flow and power that aliases provide. Remember though some git commands can be dangerous such as git clean and git reset I would recommend not to alias these

## Setup Part 2

Once you've gotten used to the aliases in part 1 you can add some further aliases

> git config --global alias.pu push
>
> git config --global alias.pl pull

## Forgetting Aliases

Don't panic you can always find your aliases again with

> git config -l

and then look for "alias". If you run this into a grep tool (not sure if this is possible on windows)

> git config -l | grep "alias"
