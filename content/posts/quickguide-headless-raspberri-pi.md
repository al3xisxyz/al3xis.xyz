---
title: "Quickguide - Headless Raspberri Pi setup"
date: 2022-04-17T23:06:05+02:00
tags: [Raspberry Pi]
featured_image: ""
description: "This is a quick setup cheat sheet to start a headless Raspberry Pi."
ShowToc: true
TocOpen: true
draft: false
---

This guide is to make the initial steps from formating the microSD card to having ssh access to a headless Raspberry Pi.

---

## Headless Raspberry Pi

### Fresh Installation
- Install the [rpi-imager](https://github.com/raspberrypi/rpi-imager).
- Choose the `Raspberry Pi OS Lite (64-bit)`
- Select the microSD card and `Write`

### Prepare the microSD card
Before the first boot the microSD card needs a user account and the SSH connection enabled.

#### User account
Add a `userconf.txt` file in the boot folder. In the file include: `username:password` (your username, followed by a colon, followed by the encrypted password)

To generate the encrypted password:

```
echo 'mypassword' | openssl passwd -6 -stdin
```

#### Enable SSH
Add an empty `ssh` file in the boot folder
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)

#### Boot and SSH into the Raspberry Pi
Insert the microSD card and boot the Raspberry Pi with an ethernet cable connected.

Connect with ssh:
```
ssh username@192.168.x.x
```

---
### Adjustments after first boot

#### Change default ssh port

```
sudo nano /etc/ssh/sshd_config
```
Uncomment the #22 and change it to the desired port (i.e. 2234)

#### Restart SSH 
```
sudo systemctl restart ssh
```
Exit & connect with ssh again:
```
exit
ssh username@192.168.x.x -p 2234
```

---
### Install Firewall UFW

```
sudo apt install ufw
```
#### Allow a port
```
sudo ufw allow 2234
```
#### Deny a port
```
sudo ufw deny 22
```
#### Limit a port
```
sudo ufw limit ssh/tcp
```
#### Start UFW
```
sudo ufw enable
```
#### Firewall status
```
sudo ufw status
```
#### Enable logs
```
sudo ufw logging on
```
The logs are stored under `/var/log/ufw.log`