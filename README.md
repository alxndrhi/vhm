# VirtualHostManager (vhm)
A script that helps to manage virtual hosts on Mac OS X _(it may also run on other unix based systems with some or no changes)_.

The Idea is to keep the changes on the existing config as little as possible.

## Install

### Homebrew (recommended)
1. Install: ```brew tab alxndrhi/miscbrew && brew install vhm```
2. Tell apache where to find the configuration: ```sudo echo "Include /usr/local/etc/vhm/httpd-vhosts.conf" >> /etc/apache2/extra/httpd-vhosts.conf```
3. Check the vhm Configuration in: ```/usr/local/etc/vhm/vhm.cfg```

### Manual O.o
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

For a full list of parameters see ```vhm --help```

### Template files
You can create your own template files. Just put them in ```/usr/local/etc/vhm/templates```.

**Info**
* After creating a new _VirtualHost_ you have to enable it.
* Remember to restart apache after every change to the configuration.
* If apache don't start just run ```apachectl``` without any parameter to see the error message.
* Delete will remove the VirtualHost config file and the symlink from ```/etc/apache2/sites-enabled``` and ```/etc/apache2/sites-available```. This will **not** remove any of your project files.

## TODO
* custom variables to replace in template file
* try to run apachectl without sudo first and fallback to sudo

## Migration from earlier versions to v0.1.1
Actually it is not that hard to migrate from an earlier clone of this repository, but there are some steps to do. I know, you are pretty hardcore, so this shouldn't be a problem for you.

Just in case, here is a little checklist.
1. remove old vhm Files ```rm -rf ~/.vhm/```
2. remove old vhm script from bin, if in ~/bin: ```rm ~/bin/vhm``` if located in /usr/local/bin: ```rm /usr/local/bin/vhm```
3. Install vhm: ```brew tap alxndrhi/miscbrew && brew install vhm```
4. Copy existing VirtualHosts: ```cp /etc/apache2/sites-available/* /usr/local/etc/vhm/sites-available/```
5. update your local config in: ```~/.vhm.cfg```by comparing it with the new one here: ```/usr/local/etc/vhm/vhm.cfg```or simply delete the old one and update the new one
6. Enable every Site you want to have enabled.
7. remove old directories ```rm -rf /etc/apache2/sites-enabled && rm -rf /etc/apache2/sites-available```
8. update apache to point to the new config location _(step 2 Installation with Homebrew)_
