---
layout: post
title: Setting up Remote Webstorm in Ubuntu 20.10
date: 2021-04-17 22:55 +0000
---

## Pre-reqs
First install Webstorm on your server (apt/whatever). I went with the snap:

`sudo snap install webstorm --classic`

Make sure you have a jdk installed, ex:

`sudo apt install openjdk-15-jdk`

(note: you can search for the latest with `apt search openjdk.*-jdk`)

## Connecting

Connect to your remote Ubuntu server using the "-X" ssh flag:

`ssh -X hp.lan`

Success (hopefully)!

![Webstorm Over SSH](/assets/posts/2021/04/17/webstorm.png "Webstorm over SSH")

## Troubleshooting

### Server Side:
- You can try running "xeyes" to narrow down the problem to your X11Forwarding or the app itself
- Make sure /etc/ssh/sshd_config has "X11Forwarding yes"
- Make sure you see something when you do "echo $DISPLAY" from your active ssh session

### Client Side:
- Make sure you connect with the -X flag (or set X11 forwarding as default w/ "ForwardX11 yes" in ~/.ssh/config)

## References:
- [https://unix.stackexchange.com/questions/12755/how-to-forward-x-over-ssh-to-run-graphics-applications-remotely](https://unix.stackexchange.com/questions/12755/how-to-forward-x-over-ssh-to-run-graphics-applications-remotely)
- [https://snapcraft.io/webstorm](https://snapcraft.io/webstorm)