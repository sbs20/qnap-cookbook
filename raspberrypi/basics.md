# Basics
This outlines various common tasks which all rely on your having terminal
access to your pi. If you don't have that then go and download PuTTY or
something similar and then come back. If you've just got your Pi out of
the box and vaguely know about linux then start here.

## Inital login
Default username and password for raspbian are:

    username: pi
    password: raspberry

## Change pi user
Reference: https://serverfault.com/a/653514

Create a new temp account with sudo rights:

    sudo adduser temp
    sudo adduser temp sudo

Log out from your current account and back in with the temp account.

Rename your username and directory:

    sudo usermod -l new-username -m -d /home/new-username old-username

Rename your username default's group:

    sudo groupmod -n new-username old-username

Log out from temp account and log back into your account with new-username.

Remove temp account:

    sudo userdel -r temp



## Filesystem
### Expand filesystem
You can do [this](http://raspberrypi.stackexchange.com/a/501) or take the
easy option and ...
```
sudo raspi-config
```

### Disk usage
```
sudo du -h --max-depth=1
df -h
```

## Reboot
    sudo reboot

## Network
### Network interfaces
    ifconfig

### IP addresses
    ip addr show eth0

### Bindings
    # All
    netstat -ltunp
    
    # Just for port 631
    netstat -ltunp | grep 631

## Timezone
```
sudo dpkg-reconfigure tzdata
```

## Package management
```
sudo apt-get update
apt-cache pkgnames | grep mono
dpkg-query -l
sudo apt-get upgrade
apt-cache search packagename
```
    
### Get rid of packages
Unless you need these they're just using up space

```
sudo apt-get remove --purge libreoffice*
sudo apt-get remove --purge wolfram-engine
sudo apt-get remove --purge oracle-java8-jdk oracle-java7-jdk openjdk*
sudo apt-get autoremove
```

Also this: https://blog.samat.org/2015/02/05/slimming-an-existing-raspbian-install/

### Reinstall raspi-config
Then: https://github.com/snubbegbg/install_raspi-config

## What version of linux am I running?
Try:
```
uname -a
```

## Working with a USB3.0 hub
There is information here: https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=53832 and
here https://github.com/raspberrypi/firmware/issues/64

Try doing an update
```
sudo rpi-update
```
But if that doesn't work then edit /boot/cmdline.txt and downgrade USB to 1.1. It is a space
delimited set of value pairs
```
sudo nano /boot/cmdline.txt
```
And add the following to it:
```
dwc_otg.speed=1
```
