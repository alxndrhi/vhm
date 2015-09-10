# VirtualHostManager (vhm)
A script that helps to manage virtual hosts on Mac OS X _(it may also run on other unix based systems with some or no changes)_.

The Idea is to keep the changes on the existing config as little as possible.

## Install

### Homebrew (recommended)
1. Install: ```brew tap alxndrhi/miscbrew && brew install vhm```
2. Tell apache where to find the configuration: ```sudo echo "Include /usr/local/etc/vhm/httpd-vhosts.conf" >> /etc/apache2/extra/httpd-vhosts.conf```
3. Check the vhm Configuration in: ```/usr/local/etc/vhm/vhm.cfg```

### Manual
1. create _sites-available_ folder: ```mkdir -p /usr/local/etc/vhm/sites-available```
2. create _sites-enabled_ folder: ```mkdir -p /usr/local/etc/vhm/sites-enabled```
3. create _templates_ folder: ```mkdir -p /usr/local/etc/vhm/templates```
4. Download Release from [releases page](https://github.com/alxndrhi/vhm/releases) untar / unzip it
5. symlink vhm: ```ln -s WHEREVER-YOU-PUT-THE-FILES/vhm /usr/local/bin/vhm```
6. copy config: ```cp WHEREVER-YOU-PUT-THE-FILES/vhm.cfg /usr/local/etc/vhm/vhm.cfg``` _(don't forget to edit the config)_
7. copy template ```cp WHEREVER-YOU-PUT-THE-FILES/VirtualHost.conf /usr/local/etc/vhm/templates/```
7. copy apache config file ```cp WHEREVER-YOU-PUT-THE-FILES/httpd-vhosts.conf /usr/local/etc/vhm/```
8. Tell apache where to find the configuration: ```sudo echo "Include /usr/local/etc/vhm/httpd-vhosts.conf >> /etc/apache2/extra/httpd-vhosts.conf```

## Using vhm
To create a host, you have to go into the root folder of the new host and run ```vhm -d domain-name cr```.

### examples
Ok, lets say we want to create the development domain _testing.dev_ with the "DocumentRoot" in ~/Sites/testing.dev/,
and as we are already here, we also want to enable it and restart apache.

```
mkdir -p ~/Sites/testing.dev
cd ~/Sites/testing.dev
vhm -d testing.dev cr en --apache-restart
```

You can use your custom template file or an alternative template file by using the --template parameter.

```
mkdir -p ~/Sites/testing.dev
cd ~/Sites/testing.dev
vhm -d testing.dev cr en --template MyTemplateFileName.conf --apache-restart
```

To delete, disable or enable an existing VirtualHost you dont have to ```cd``` into the "DocumentRoot". Just use the --domain parameter:

```
vhm -d testing.dev --enable
vhm -d testing.dev --disable
vhm -d testing.dev --delete
```
See a list of Domains including Status:

```
vhm -l
```

For a full list of parameters see ```vhm --help```

### Template files
You can create your own template files. Just put them in ```/usr/local/etc/vhm/templates```.

**Info**
* After creating a new _VirtualHost_ you have to enable it.
* Remember to restart apache after every change to the configuration.
* If apache don't start just run ```apachectl``` without any parameter to see the error message.
* Delete will remove the VirtualHost config file and the symlink from ```/etc/apache2/sites-enabled``` and ```/etc/apache2/sites-available```. This will **not** remove any of your project files.
