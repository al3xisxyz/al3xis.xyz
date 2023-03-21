---
title: "Quickguide Git 2023"
date: 2023-03-21T16:00:00Z
tags: [Git, Github, Gitlab, SSH]
featured_image: ""
description: "A simple guide/cheatsheet with all the steps and commands to configure Git and connect with SSH to Github or Gitlab."
ShowToc: true
TocOpen: true
draft: false
---

## Install
- https://git-scm.com/download/linux
- https://docs.github.com/en/get-started/quickstart/set-up-git

```
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git
git --version
```

## Configure
### Configure Git
```
git config --global user.name "Xyz"
git config --global user.email "xxxxx@xxxx.xyz"

# Enable main as the default branch
git config --global init.defaultBranch main

# Enable colours
git config --global color.ui auto

# Check the configuration
git config --list
```

### Generate SSH key
- https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
- https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding
- https://docs.gitlab.com/ee/user/ssh.html#generate-an-ssh-key-pair

```
# Generate SSH key
ssh-keygen -t ed25519 -C "xxxxx@xxxx.xyz"

# Start ssh-agent in the background
eval "$(ssh-agent -s)"

# Add SSH key to ssh-agent (rename key if needed)
ssh-add ~/.ssh/id_ed25519
```

### Add SSH key in Github/Gitlab
- https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account#adding-a-new-ssh-key-to-your-account
- https://docs.gitlab.com/ee/user/ssh.html#add-an-ssh-key-to-your-gitlab-account

```
# Print the public SSH key (rename key if needed)
cat ~/.ssh/id_ed25519.pub

# Or
xclip -sel clip < ~/.ssh/id_ed25519.pub
```

### Verify Github/Gitlab connectivity
- https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection
- https://docs.gitlab.com/ee/user/ssh.html#verify-that-you-can-connect

```
ssh -T git@github.com

# Or (rename domain)
ssh -T git@gitlab.example.com

# Or run in verbose mode
ssh -Tvvv git@gitlab.example.com
```

## Connect to Github/Gitlab Repo
### First initialization
- https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository

```
cd folder/to/myWebsite
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:xxxxx/xxxxx.git
git push -u origin main
```

### Connect to existing Remote
- https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes
- https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories
- https://docs.gitlab.com/ee/gitlab-basics/start-using-git.html#clone-with-ssh

```
git clone git@github.com:xxxxx/xxxxx.git

# Restore Submodules (e.g. themes):
git submodule update --init --recursive

# View the remote repository
git remote -v
git remote show origin
```

### Make Commits
- https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository

```
git status
git add file
git commit -m "message"
git push -u origin main
```

---
If you liked this, consider sending a tip by ko-fi from the button below, and if you want to send me any feedback, you can reach me by [email](mailto:emailme@al3xis.xyz) or on Nostr @al3xis `npub10xxhztawwgtuapdej49q5jgfawu5p0f2j2tzuaxxww2hl546ct3sr7pcjl`.
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/V7V1CFV13)