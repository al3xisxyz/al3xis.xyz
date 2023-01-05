---
title: "Quickguide - Hugo | Git | Netlify setup"
date: 2021-02-16T11:50:27+01:00
tags: [Hugo, Git, Netlify]
featured_image: ""
description: "This is a simple guide/cheatsheet with all the steps and commands to take you from nothing to a FREE published website with Hugo, GitHub and Netlify!"
ShowToc: true
TocOpen: true
draft: false
---

This guide assumes that you have already bought a domain for your website (I recommend [Porkbun](https://porkbun.com/products/domains) if you want to buy one now). The domain cost is the only cost needed in this guide. To create, host and publish your website is completely **FREE**!

---

## Hugo installation

There are many ways to install Hugo in all major operating systems, described under the [Hugo installation documentation](https://gohugo.io/getting-started/installing)

To install Hugo on some of the popular Linux distributions:
```
Debian/Ubuntu based:
snap install hugo

Arch based:
pacman -S hugo

Fedora/Red Hat based:
dnf install hugo
```

Verify the installation and check the version:
```
hugo version
```

### New Hugo site

Now, navigate to the folder where you want Hugo to create your website's folder. For example in `webdev/sites`
```
hugo new site myWebsite
```

This will create a new folder for your website with the hugo structure in it `webdev/sites/myWebsite`

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

[First-Time Git Setup Documentation](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)

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

Now [create a new GitHub repository](https://github.com/new) where we will store our Hugo files, for example with a name `myWebsite`. Then we will have an SSH link for the GitHub repository such as `git@github.com:myname/myWebsite.git` which we will use later to connect in our local Git environment.

### Create an SSH key and insert it in GitHub

In order to connect to your GitHub account from your local machine without having to give a username and password everytime then you can setup an SSH key.

In the terminal check if you already have an SSH key:
```
ls ~/.ssh/id_rsa.pub
```

If you get a message `No such file or directory` then create an SSH key by using the email you used to create an account on GitHub:
```
ssh-keygen -C myname@email.com
```
During the key generation process it will prompt you for a location to save the generated key and ask for a password, but you can just press `Enter` to skip both.

Now we can print/see the newly made public SSH key in the terminal with:
```
cat ~/.ssh/id_rsa.pub
```
Copy the output in order to insert it in GitHub by going to your profile image on the top right corner and then `Settings -> SSH and GPG keys -> New SSH key`. Add a title of your choice and paste the key in the field below.

[Test the SSH connection with GitHub](https://docs.github.com/en/github/authenticating-to-github/testing-your-ssh-connection) by entering in your terminal:
```
ssh -T git@github.com
```

If everything is configured correctly you should see:
> Hi *myname*! You've successfully authenticated, but GitHub does not provide shell access.

### Connect Git with GitHub

Now we can start working on our Hugo website and push the local files to the GitHub repository.

Start Git in the folder with the Hugo files ([check the Git documentation for details](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository)). First navigate in the folder `webdev/sites/myWebsite` and then initialize Git, add all files (don't forget the dot `.`), commit the files, choose the branch, connect to the GitHub repository we created earlier and finally push the files up to GitHub:
```
cd webdev/sites/myWebsite
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:myname/myWebsite.git
git push -u origin main
```

Next time we want to connect to an existing repository with our files on GitHub we can just clone the repository locally to start working on the latest version of the files:
```
git clone git@github.com:myname/myWebsite.git
```

---

## Install Visual Studio Code

Now all the configuration is done and we are ready to start editing our Hugo site! The most popular code editor software is [Visual Studio Code](https://code.visualstudio.com/). Just install it, navigate to your folder structure and start editing the files. Then you can [manage the Git commands straight in Visual Studio Code](https://code.visualstudio.com/docs/editor/versioncontrol).

---

## Connect your GitHub repository to Netlify

The [Hugo documentation about Netlify](https://gohugo.io/hosting-and-deployment/hosting-on-netlify) is quite nice to follow. 

First [make an account on Netlify](https://app.netlify.com/) and connect it to your GitHub account.

Next we can create a `netlify.toml` file in our Hugo folder. Go to [Configure Hugo Version in Netlify](https://gohugo.io/hosting-and-deployment/hosting-on-netlify#configure-hugo-version-in-netlify) and copy all the contents into your file. You can change the version number if you want in the file. Save it and push it to your GitHub account.

Now from Netlify we can continue and create a `New site from Git`. Choose your new repository when asked and in the last step enter `Hugo` in the field command and `public` for directory.

Our website will deploy now with Netlify. We get a url from Netlify to check our website in the form of `something.netlify.app`. To connect your own domain with Netlify follow [Netlify's instructions on custom domains](https://docs.netlify.com/domains-https/custom-domains/). The instructions will take you to change the nameservers in your domain provider (for example in Porkbun) to specific nameservers from Netlify. This change should take an hour to be register from your domain provider and then another hour from Netlify. So in total 2 hours minimum from the time you change nameservers to Netlify's in your domain provider until you see your website through your domain url. In the meantime you can edit your website and push the changes to GitHub and use Netlify's own url to see your page take shape.

***Done!***

Of course there are plenty more settings in Netlify but the basics are done and you have a working site for **free!** One cool thing I do in Netlify is to have a `dev.mywebsite.com` that takes my Hugo files from a secondary branch `dev` on GitHub and deploy a website with ongoing changes to the `dev.mywebsite.com`. This is perfect in order to work on a draft version of the website and see the work take shape without affecting the actual website where people might be visiting. If you are interested in that check [Netlify's documentation on branch deploys](https://docs.netlify.com/site-deploys/overview/#branch-deploy-controls).

---
If you liked this, consider sending a tip by ko-fi from the button below, and if you want to send me any feedback, you can reach me by [email](mailto:emailme@al3xis.xyz).
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/V7V1CFV13)