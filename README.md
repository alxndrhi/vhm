# VirtualHostManager (vhm)

This is a litte script that should help to manage apache's virtual hosts on Mac OS X Systems _(it may also run on other unix based systems with some or none changes)_.
Changes to the existing apache config are as little as possible.

## Install

1. Clone Files: ```git clone https://github.com/alxndrhi/vhm.git ~/.vhm```
2. symlink vhm: ```ln -s ~/.vhm/vhm ~/bin/vhm```
3. Edit ```~/.vhm/vars.cfg```
4. create _sites-available_ folder: ```sudo mkdir -p /etc/apache2/sites-available```
5. create _sites-enabled_ folder: ```sudo mkdir -p /etc/apache2/sites-available```
6. prepare apache conf: ```sudo echo "Include /etc/apache2/sites-enabled/*.conf" >> /etc/apache2/extra/httpd-vhosts.conf```
  * alternativ: copy the ```httpd-vhosts.conf``` file of this repo into ```/etc/apache2/extra``` (never forget to make **backups**)

If you dont want to run ```vhm``` with sudo you should change the permission for ```/etc/apache2/sites-available``` and ```/etc/apache2/sites-enabled```.

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
I am open for suggestions

## Changelog

### 20150503
* **DONE**: _(slightly better check for given parameters)_ Parameter order is not important anymore.
* **DONE**: _(chain actions together: cr -> en)_ You now can create a new Host and Enable it in one command ```vhm -d test.dev --create --enable```
* added the possibility for custom template files. Just put another template file into the ```~/.vhm/``` Folder and use the -t parameter ```--template TEMPLATE_FILE_NAME```
* added parameter that restarts Apache after the changes ( ```-ar``` or ```--apache-restart``` ) it uses ```sudo```
