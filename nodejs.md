## Install and upgrade


### Install nodejs
* On Windows
* On Linux
* On Mac

### Install modules
* [how to install nodejs package from github directly](http://stackoverflow.com/questions/17509669/how-to-install-nodejs-package-from-github-directly)

```
npm install git+https://git@github.com/visionmedia/express.git
npm install git+ssh://git@github.com/visionmedia/express.git
# configed ssh 
npm install git+ssh://configName:visionmedia/express.git
```
* [installing-a-local-module-using-npm](https://stackoverflow.com/questions/8088795/installing-a-local-module-using-npm)
```
npm install path
```
or [link](https://docs.npmjs.com/cli/link)

### Update nodejs or npm
* Mac/Linux/Window(with poweshell)
```bash
# Clean cache, usually it is not necessary
$ sudo npm cache clean -f
# n is tool for manage nodejs/npm versions
$ sudo npm install -g n 
$ sudo n stable 

```
* On Windows
  * [how-do-i-update-node-and-npm-on-windows](http://stackoverflow.com/questions/18412129/how-do-i-update-node-and-npm-on-windows)


### Issues
* [How to fix 'fs: re-evaluating native module sources is not supported' - graceful-fs](http://stackoverflow.com/questions/37346512/how-to-fix-fs-re-evaluating-native-module-sources-is-not-supported-graceful)
