---
title: Managing your $HOME with git without symlinks
categories: git, linux
---

## Overview

Based off the thread found at [https://news.ycombinator.com/item?id=11071754](https://news.ycombinator.com/item?id=11071754)

This relatively simple setup allows you to manage your dot files with just git and without having to resort to symlinks or some other hackery.

## New Setup

1. Create your git working directory
  ~~~
git init --bare ${HOME}/.config/dotfiles
  ~~~
1. Add an alias to git which will only be used for working with your dot files
  ~~~
alias dotgit='/usr/bin/git --git-dir=${HOME}/.config/dotfiles/ --work-tree=${HOME}'
  ~~~
1. Ignore your .git directory to avoid headaches
  ~~~
echo "${HOME}/.config/dotfiles" > ${HOME}/.gitignore
  ~~~
1. Ignore untracked files by default, this will make 'dotgit status' a lot less noisy
  ~~~
dotgit config --local status.showUntrackedFiles no
  ~~~
1. Link your repo to a remote repository for easy backups
  ~~~
dotgit remote add origin <GIT_URI>
  ~~~

## Importing an existing repository onto a new system

1. Add the alias to git which will only be used for working with your dot files
  ~~~
alias dotgit='/usr/bin/git --git-dir=${HOME}/.config/dotfiles/ --work-tree=${HOME}'
  ~~~
1. Ignore your .git directory to avoid headaches
  ~~~
echo "${HOME}/.config/dotfiles" > ${HOME}/.gitignore
  ~~~
1. Clone the repository
  ~~~
git clone --bare <GIT_URI> ${HOME}/.config/dotfiles
  ~~~
1. Check out the code
  ~~~
dotgit checkout
  ~~~
  WARNING: This might throw the following error if some of the files to checkout already exist:
  ~~~
error: The following untracked working tree files would be overwritten by checkout:
  .bashrc
Please move or remove them before you can switch branches.
Aborting
  ~~~
  You'll need to delete the mentioned files and retry the check out.
1. Ignore untracked files by default, this will make 'dotgit status' a lot less noisy
  ~~~
dotgit config --local status.showUntrackedFiles no
  ~~~

## Usage

Once the setup is completed you can interact with it like you would any git repository.

~~~
dotgit add .bashrc
dotgit commit -m 'adding .bashrc'
dotgit push
~~~
