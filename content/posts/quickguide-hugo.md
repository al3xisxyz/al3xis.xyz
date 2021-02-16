---
title: "Quickguide - Hugo, Git, Netlify setup"
date: 2021-02-16T11:50:27+01:00
tags: [Hugo, Git, Netlify]
featured_image: ""
description: "This is guide/cheatsheet with all the steps and commands to install Hugo, Git and deploy with Netlify."
draft: false
---

# Quickguide - Hugo first setup

This is a simple guide for a first time Hugo setup with all the steps and necessary resources to take you from nothing to a published website!

***

## Hugo installation

There are many ways to install Hugo described under [Hugo installation documentation](https://gohugo.io/getting-started/installing)

My preferred method to install Hugo is with snaps:

`snap install hugo`

Verify the installation and check the version:

`hugo version`

***

## New Hugo site

Navigate to the folder where you want Hugo to create your site's folder. For example in `/webdev/sites`

`hugo new site mywebsite`

This will create a new folder with the hugo structure in it `/webdev/sites/mywebsite`

***

## Add a Hugo theme

[Find a Hugo theme](https://themes.gohugo.io) you like and add it to your themes folder. I chose here the [PaperMod theme](https://themes.gohugo.io/hugo-papermod/) ([PaperMod installation documentation](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation))

`git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod --depth=1`

`git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)`

Update the theme when needed with:

`git submodule update --remote --merge`

***

## Start Git and connect with GitHub

### Git installation

This will assume an operating system based on Ubuntu linux. For other operating systems check the [Git download page](https://git-scm.com/downloads)

First, let's check if Git is already installed and what version it is:

`git --version`

[Git version 2.28](https://github.blog/2020-07-27-highlights-from-git-2-28/) brought many updates including the possibility to change the default branch to something different than just `master`. This is important in order to align with the [GitHub's change in default branch name](https://github.com/github/renaming) from `master` to `main`. 

So, if you don't have Git or you have a version older than 2.28 then install the latest version of Git:

```
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git
```

### Git configuration

Set your name and email in Git:
```
git config --global user.name "My Name"
git config --global user.email "myname@email.com"
```

And now we can set Git to initialize by default with the branch `main` and thus align with GitHub as mentioned earlier.
`git config --global init.defaultBranch main`

We can also enable colors in Git with:
`git config --global color.ui auto`

Verify new configuration:
```
git config --get user.name
git config --get user.email
```

### Connect Git with GitHub

First create a GitHub account.

### Create first repository and push to GitHub

Create a new repository on the command line:
```
echo "# anthista.se" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:al3xisxyz/anthista.se.git
git push -u origin main
```

Push an existing repository from the command line:
```
git remote add origin git@github.com:al3xisxyz/myRepository.git
git branch -M main
git push -u origin main
```
