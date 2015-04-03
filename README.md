# VirtualHostManager (vhm)

This is a litte shell script that should help to manage virtual apache hosts on Mac OS X Systems.
Changes to the existing apache config are as little as possible.

## Install

1. Clone Files: ```git clone https://github.com/alxndrhi/vhm.git ~/.vhm```
2. symlink vhm: ```ln -s ~/.vhm/vhm ~/bin/vhm```
3. Edit ```~/.vhm/vars.cfg``` so it fits your settings
4. create _sites-available_ folder: ```sudo mkdir -p /etc/apache2/sites-available```
5. create _sites-enabled_ folder: ```sudo mkdir -p /etc/apache2/sites-available```
6. prepare apache conf: ```sudo echo "Include /etc/apache2/sites-enabled/*.conf" >> /etc/apache2/extra/httpd-vhosts.conf```
  * alternativ: copy the ```httpd-vhosts.conf``` file of this repo into ```/etc/apache2/extra``` (never forget to make **backups**)

If you dont want to run ```vhm``` with sudo you should change the permission to ```/etc/apache2/sites-available``` and ```/etc/apache2/sites-enabled```.

## Using vhm

To create a Host, you have to go into the Root Folder of the new Host and run vhm with Parameter cr (or create) followed by the development hostname:

- create: ```vhm cr test.dev```
- enable: ```vhm en test.dev```
- disable: ```vhm dis test.dev```
- delete: ```vhm del test.dev```

Delete will remove the VirtualHost config file and the symlink from ```/etc/apache2/sites-enabled``` and ```/etc/apache2/sites-available```. 
This will **not** remove any of your Project files.

**Info**

After creating a new _VirtualHost_ you have to enable it. Remember to restart apache after every change to the configuration.

## TODO:
* better check for given parameters
* chain actions toghether: cr -> en _(?)_
