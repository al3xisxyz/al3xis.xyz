---
title: "Quickguide - Hugo | Git | Netlify setup"
date: 2021-02-16T11:50:27+01:00
tags: [Hugo, Git, Netlify]
featured_image: ""
description: "This is a simple guide/cheatsheet with all the steps and commands to take you from nothing to a FREE published website with Hugo, GitHub and Netlify!"
draft: false
---

This guide assumes that you have already bought a domain for your website (I recommend [Porkbun](https://porkbun.com/products/domains) if you want to buy one now). The domain cost is the only cost needed in this guide. To create, host and publish your website is completely **FREE**!

---

## Hugo installation

There are many ways to install Hugo described under the [Hugo installation documentation](https://gohugo.io/getting-started/installing)

My preferred method to install Hugo is on Linux with snaps:
```
snap install hugo
```

Verify the installation and check the version:
```
hugo version
```

### New Hugo site

Now, navigate to the folder where you want Hugo to create your website's folder. For example in `/webdev/sites`
```
hugo new site mywebsite
```

This will create a new folder for your website with the hugo structure in it `/webdev/sites/mywebsite`

### Add a Hugo theme

[Find a Hugo theme](https://themes.gohugo.io) you like and add it to your themes folder. I chose here the [PaperMod theme](https://themes.gohugo.io/hugo-papermod/) ([PaperMod installation documentation](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation))

```
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod --depth=1
git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
```

Update the theme when needed with:

```
git submodule update --remote --merge
```

---

## Start Git and connect with GitHub

### Git installation

This will assume an operating system based on Ubuntu linux. For other operating systems check the [Git download page](https://git-scm.com/downloads)

First, let's check if Git is already installed and what version it is:
```
git --version
```

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

And now we can set Git to initialize by default with the branch `main` and thus align with GitHub as mentioned earlier:
```
git config --global init.defaultBranch main
```

We can also enable colors in Git with:
```
git config --global color.ui auto
```

Lastly, verify that your name and email is properly added in the new configuration:
```
git config --get user.name
git config --get user.email
```

### Create a GitHub account

Create a [GitHub account](https://github.com/join) if you don't have an account yet. Gitlab, Bitbucket and others should work too but might need some different settings comparing to GitHub.

Now [create a new GitHub repository](https://github.com/new) where we will store our Hugo files, for example with a name `myWebsite`. Then we will have a link for the GitHub repository such as `https://github.com/al3xisxyz/myWebsite` which we will use later to connect in our local Git environment.

### Create an SSH key and insert it in GitHub

In order to connect to your GitHub account from your local machine without having to give a username and password everytime then you can setup an SSH key.

I the terminal check if you already have an SSH key:
```
ls ~/.ssh/id_rsa.pub
```

If you get a message `No such file or directory` then create an SSH key by using the email you used to create an account on GitHub:
```
ssh-keygen -C myname@email.com
```
During the key generation process it will prompt you for a location to save the generated key and ask for a password, but you can just press `Enter` to skip both.

Now we can print the newly made public SSH key in the terminal with:
```
cat ~/.ssh/id_rsa.pub
```
And copy the output in order to insert it in GitHub by going to your profile image on the top right corner and then `Settings -> SSH and GPG keys -> New SSH key`. Add a title of your choice and paste the key in the field below.

[Test the SSH connection with GitHub](https://docs.github.com/en/github/authenticating-to-github/testing-your-ssh-connection) by entering in your terminal:
```
ssh -T git@github.com
```

If everything is configured correctly you should see:
> Hi *myname*! You've successfully authenticated, but GitHub does not provide shell access.

### Connect Git with GitHub

Now we can start working on our Hugo website and push the local files to the GitHub repository.

Create a new repository on the command line and push it to GitHub:
```
echo "# myRepository" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:al3xisxyz/myRepository.git
git push -u origin main
```

Create a new repository on GitHub and clone it locally so you can start developing it:
```
git clone git@github.com:al3xisxyz/myRepository.git
```


---

## Install Visual Studio Code

Now all the configuration is done and we are ready to start editing our Hugo site! The most popular code editor software is [Visual Studio Code](https://code.visualstudio.com/). Just install it, navigate to your folder structure and start editing the files.