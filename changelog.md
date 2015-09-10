# Changelog

## 20150910 (Release v0.2.0)
* Added list view of Domains including status
* You now can set use_suo in config to -1 if you dont want apachectl to be run as sudo
* Added some fancy colors

## 20150606 (Release v0.1.0)
* Updated Installation Instruction - created Homebrew Tab _(yeah I know, I changed the folder structure for this)_
* Updated Paths in files - now you have less to do after brewing this :)
* Fixed Variable Names and cleaned it up a bit

## 20150507
* DONE: vars.cfg as config file in ~/ so you dont overwrite it with every pull. If not set the one from ~/.vhm should be read instead
* DONE: --info to print / cat vhost file to a given domain
* added: --status to print status of given domain (enabled, disabled, not created)

## 20150503
* DONE: (slightly better check for given parameters) Parameter order is not important anymore.
* DONE: (chain actions together: cr -> en) You now can create a new Host and Enable it in one command vhm -d test.dev --create --enable
* added: the possibility for custom template files. Just put another template file into the ~/.vhm/ Folder and use the -t parameter --template TEMPLATE_FILE_NAME
* added: parameter that restarts Apache after the changes ( -ar or --apache-restart ) it uses sudo
