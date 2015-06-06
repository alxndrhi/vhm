# VirtualHostManager (vhm)

This is a litte script that should help to manage apache's virtual hosts on Mac OS X Systems _(it may also run on other unix based systems with some or none changes)_.
Changes to the existing apache config are as little as possible.


## Install

### Using Homebrew (recommended)
1. Tab the location: ```brew tab alxndrhi/miscbrew```
2. install Formula: ```brew install vhm```
3. Tell apache where to find the configuration: ```sudo echo "Include /usr/local/etc/vhm/httpd-vhosts.conf >> /etc/apache2/extra/httpd-vhosts.conf```
4. Check the vhm Configuration in: ```/usr/local/etc/vhm/vhm.cfg```

### Manual Installation
1. create _sites-available_ folder: ```sudo mkdir -p /usr/local/etc/vhm/sites-available```
2. create _sites-enabled_ folder: ```sudo mkdir -p /usr/local/etc/vhm/sites-available```
3. Clone Files: ```git clone https://github.com/alxndrhi/vhm.git WHEREEVER-YOU-WANT-TO-PUT-THE-FILES```
4. symlink vhm: ```ln -s WHEREEVER-YOU-WANT-TO-PUT-THE-FILES/vhm /usr/local/bin/vhm```
5. Set config: ```cp WHEREEVER-YOU-WANT-TO-PUT-THE-FILES/vhm.cfg /usr/local/etc/vhm/.vhm.cfg``` _(don't forget to edit you config)_
6. Tell apache where to find the configuration: ```sudo echo "Include /usr/local/etc/vhm/httpd-vhosts.conf >> /etc/apache2/extra/httpd-vhosts.conf```

## Using vhm

To create a Host, you have to go into the Root Folder of the new Host and run vhm.

### examples

Ok, lets say we want to create the development domain _testing.dev_ with the DocumentRoot in ~/Sites/testing.dev/,
and as we are already here, we also want to enable it and restart apache.

```
mkdir -p ~/Sites/testing.dev
cd ~/Sites/testing.dev
vhm --domain testing.dev --create --enable --apache-restart
```

You can also use your custom template file or an alternativ template file by using the --template parameter.

```
mkdir -p ~/Sites/testing.dev
cd ~/Sites/testing.dev
vhm --domain testing.dev --create --enable --template MyTemplateFileName.conf --apache-restart
```

To delete, disable or enable an existing VirtualHost you dont have to ```cd``` into the DocumentRoot. Just use the --domain parameter:

```
vhm --domain testing.dev --enable
vhm --domain testing.dev --disable
vhm --domain testing.dev --delete
```

For a full list of parameters see ```vhm --help```

### Template files
You can create additional template files. Just copy the VirtualHost.conf file in ```~/.vhm``` and make your changes.

**Info**

* After creating a new _VirtualHost_ you have to enable it. Remember to restart apache after every change to the configuration. Both can be done in one command now with the parameters: ```--enable --apache-restart```.
* Delete will remove the VirtualHost config file and the symlink from ```/etc/apache2/sites-enabled``` and ```/etc/apache2/sites-available```. This will **not** remove any of your Project files.

## TODO

I am always open for suggestions
