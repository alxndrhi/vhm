# Changelog

## 20150507 _(tagged as v0.1)_
* DONE: vars.cfg as config file in ~/ so you dont overwrite it with every pull. If not set the one from ~/.vhm should be read instead
* DONE: --info to print / cat vhost file to a given domain
* added: --status to print status of given domain (enabled, disabled, not created)

## 20150503
* DONE: (slightly better check for given parameters) Parameter order is not important anymore.
* DONE: (chain actions together: cr -> en) You now can create a new Host and Enable it in one command vhm -d test.dev --create --enable
* added: the possibility for custom template files. Just put another template file into the ~/.vhm/ Folder and use the -t parameter --template TEMPLATE_FILE_NAME
* added: parameter that restarts Apache after the changes ( -ar or --apache-restart ) it uses sudo
