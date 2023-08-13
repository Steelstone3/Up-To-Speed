# Git Configuration

## Introduction

Git on the command line off "git config" which allows you to edit user and global git configuration files. Git will prioritise local repository then global user then system wide git configurations

## File Locations

## Local Repository

In the location of your development repository

Windows: C:\dev\sources\your_repo
Unix: ~/dev/sources/your_repo

## Global User

User wide git configuration for all repositories

Windows: C:\Users\<username>\.gitconfig
Unix: ~/.gitconfig

## System Wide

System wide git configuration for all user's git repositories you will need admin permissions to change this

Windows: C:\Program Files\Git\etc\gitconfig
Unix: /etc/gitconfig

## Setting Up Git Global

> git config --global pull.rebase true
> 
> git config --global user.email "<your@email.com>"
> 
> git config --global user.name "your name"

## Setting Up Git Local

> git remote set-url origin https://your-origin-https-link.git
> 
> git config credential.helper 'cache --timeout 7200'
> 
> git config --global push.autoSetupRemote true
> 
> git config --global rebase.autoStash true

## Checking Git Config

> git config -l
