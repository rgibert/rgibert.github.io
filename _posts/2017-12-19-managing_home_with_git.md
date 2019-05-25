---
title: Managing your $HOME with git without symlinks
modified: 2017-12-29 14:02
tags: [linux]
layout: post
---

Based off the thread found at [https://news.ycombinator.com/item?id=11071754](https://news.ycombinator.com/item?id=11071754)

### Overview

This relatively simple setup allows you to manage your dot files with just git and without having to resort to symlinks or some other hackery.

### New setup

1. Create your git working directory
  {% highlight bash %}
  $ git init --bare ${HOME}/.config/dotfiles
  {% endhighlight %}
1. Add an alias to git which will only be used for working with your dot files
  {% highlight bash %}
  alias dotgit='/usr/bin/git --git-dir=${HOME}/.config/dotfiles/ --work-tree=${HOME}'
  {% endhighlight %}
1. Ignore your .git directory to avoid headaches
  {% highlight bash %}
  echo "${HOME}/.config/dotfiles" > ${HOME}/.gitignore
  {% endhighlight %}
1. Ignore untracked files by default, this will make 'dotgit status' a lot less noisy
  {% highlight bash %}
  dotgit config --local status.showUntrackedFiles no
  {% endhighlight %}
1. Link your repo to a remote repository for easy backups
  {% highlight bash %}
  dotgit remote add origin <GIT_URI>
  {% endhighlight %}

### Importing an existing repository onto a new system

1. Add the alias to git which will only be used for working with your dot files
  {% highlight bash %}
  alias dotgit='/usr/bin/git --git-dir=${HOME}/.config/dotfiles/ --work-tree=${HOME}'
  {% endhighlight %}
1. Ignore your .git directory to avoid headaches
  {% highlight bash %}
  echo "${HOME}/.config/dotfiles" > ${HOME}/.gitignore
  {% endhighlight %}
1. Clone the repository
  {% highlight bash %}
  git clone --bare <GIT_URI> ${HOME}/.config/dotfiles
  {% endhighlight %}
1. Check out the code
  {% highlight bash %}
  dotgit checkout
  {% endhighlight %}
  WARNING: This might throw the following error if some of the files to checkout already exist:
  {% highlight bash %}
    error: The following untracked working tree files would be overwritten by checkout:
      .bashrc
    Please move or remove them before you can switch branches.
    Aborting
  {% endhighlight %}
  You'll need to delete the mentioned files and retry the check out.
1. Ignore untracked files by default, this will make 'dotgit status' a lot less noisy
  {% highlight bash %}
  dotgit config --local status.showUntrackedFiles no
  {% endhighlight %}

### Usage

Once the setup is completed you can interact with it like you would any git repository.

{% highlight bash %}
$ dotgit add .bashrc
$ dotgit commit -m 'adding .bashrc'
$ dotgit push
{% endhighlight %}
