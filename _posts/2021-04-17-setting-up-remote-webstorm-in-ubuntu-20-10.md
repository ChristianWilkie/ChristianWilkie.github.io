---
published: false
---
# Setting up Remote Webstorm in Ubuntu 20.10 

## Pre-reqs
First install Webstorm on your server (apt/whatever). I went with the snap:

`sudo snap install webstorm --classic`

Make sure you have a jdk installed, ex:

`sudo apt install openjdk-15-jdk`

(note: you can search for the latest with "apt search openjdk.*-jdk"

## Connecting

Connect to your remote Ubuntu server using the "-X" ssh flag:

`ssh -X hp.lan`

Success!

![Webstorm Over SSH]({{site.baseurl}}/_posts/webstorm.png)


## Troubleshooting

### Server Side: 
-You can try running "xeyes" to narrow down the problem to your X11Forwarding or the app itself
-Make sure /etc/ssh/sshd_config has "X11Forwarding yes"
-Make sure you see something when you do "echo $DISPLAY" from your active ssh session
-Mak

### Client Side:
-Make sure you connect with the -X flag (or set X11 forwarding as default w/ "ForwardX11 yes" in ~/.ssh/config)

## References:
- https://unix.stackexchange.com/questions/12755/how-to-forward-x-over-ssh-to-run-graphics-applications-remotely
- https://snapcraft.io/webstorm
