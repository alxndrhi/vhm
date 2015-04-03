# **V**irtual**H**ost**Manager** (vhm)

This is a litte shell script that sould help to manage several virtual Apache Hosts on Mac OS X Systems.
Changes to the existing Mac OS Apache Server are as little as possible.

In addition to this script I installed dnsmasq and used resolver to only resolv \*.dev Domains with it.

## Install

1. Clone Files: ```git clone https://github.com/alxndrhi/vhm.git ~/.vhm```
2. symlink vhm: ```ln -s ~/.vhm/vhm ~/bin/vhm```
3. Edit ```~/.vhm/vars.cfg``` so it fits your settings
4. create sites-available folder: ```sudo mkdir -p /etc/apache2/sites-available```
5. create sites-enabled folder: ```sudo mkdir -p /etc/apache2/sites-available```
6. prepare apache conf: ```sudo echo "Include /etc/apache2/sites-enabled/*.conf" >> /etc/apache2/extra/httpd-vhosts.conf```
  * alternativ: copy the ```httpd-vhosts.conf``` file of this repo into ```/etc/apache2/extra``` (never forget to make **backups**)

If you dont want to run vhm with sudo you have should change access permission to ```/etc/apache2/sites-available``` and ```/etc/apache2/sites-enabled```.

## Using vhm

### create
To create a Host, you have to go into the Root Folder of the new Host and run vhm with Parameter cr (or create) followed by the development hostname:

```vhm cr test.dev```

### enable

```vhm en test.dev```

### disable

```vhm dis test.dev```

### remove
This will remove the VirtualHost File and the symlink from ```/etc/apache2/sites-enabled``` and ```/etc/apache2/sites-available```. 
It will **not** remove any of your Project files.

```vhm del test.dev```

## TODO:
* better check for given parameters