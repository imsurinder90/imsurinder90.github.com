---
layout: post
title: Configure pgAdmin4 on Apache(with mod_wsgi) on Centos 7
category: pgAdmin4
comments: true
---

### Steps to configure pgAdmin4 using apache with mod_wsgi

```
# Install python27-devel package which is the dependency for pycrypto module
$ sudo yum install python-devel.x86_64

# To get additional packages, we will enable EPEL repository, You can do that easily by typing:
$ sudo yum install epel-release

With EPEL enabled, we can install the components we need by typing:
$ sudo yum install httpd mod_wsgi

# To verify Apache’s presence on your system, you can trigger whereis command
$ sudo whereis httpd

# now configure apache to run with mod_wsgi module
# Take backup of httpd.conf

$ sudo cp /etc/httpd/conf/httpd.conf ~/httpd.conf.backup

# now modify '/etc/httpd/conf/httpd.conf' file and add below line to loadModule section
LoadModule wsgi_module modules/mod_wsgi.so

# restart apache service
$ sudo apachectl restart
```

### Apache service start/stop commands

```
# To start apache httpd server
$ sudo apachectl start
or
$ sudo /sbin/service httpd start

# To stop apache httpd server
$ sudo apachectl stop
or
$ sudo /sbin/service httpd stop

# To get status of apache httpd server
$ systemctl status httpd
or
$ sudo apachectl status

# To enable apache httpd autostart at boot
$ sudo systemctl enable httpd
```

### Modify pgadmin/web/pgAdmin4.wsgi file and replace with below content
```
import os
import sys

activate_this = '/home/surinder/venv/p27/bin/activate_this.py'
execfile(activate_this, dict(__file__=activate_this))

root = os.path.dirname(os.path.realpath(__file__))
python_path = '/home/surinder/venv/p27/lib/python2.7/site-packages'

if sys.path[0] != root:
    sys.path.insert(0, root)
    sys.path.insert(0, python_path)

from pgAdmin4 import app as application
```

### Add apache conf file for pgAdmin4
Create a new file `pgadmin4.conf` inside `/etc/httpd/conf.d/` directory with file contents

```
<virtualhost *:80>
    WSGIDaemonProcess pgadmin user=surinder group=surinder threads=5 home=/home/surinder/dev/pgadmin4/web
    WSGIScriptAlias /pgadmin /home/surinder/dev/pgadmin4/web/pgAdmin4.wsgi
    <directory /home/surinder/dev/pgadmin4/web>
        WSGIProcessGroup pgadmin
        WSGIApplicationGroup %{GLOBAL}
        WSGIScriptReloading On
        Require all granted
    </directory>
</virtualhost>
```

**where:**

  - **user=surinder** - system user name, the ownership of _/home/surinder/dev/pgadmin4_ directory
  - **directory** - the storage location of pgAdmin4 root
  - **WSGIScriptAlias pgadmin/** - the url path after *http://localhost/{pgadmin/}*, where pgAdmin4 will load
  it can be any subpath like, 'pgadmin/pgadmin/' and access like *http://localhost/pgadmin/pgadmin/*
  - **WSGIScriptAlias _/home/surinder/dev/pgadmin4/web/pgAdmin4.wsgi_** - path to pgAdmin4 wsgi file where
  pgAdmin4 virtualenv is activated first when loaded and python path and app path is added to environment.

Change the ownership of user directory:
`$ chmod 755 /home/surinder/`

Restart apache service, run `sudo apachectl restart`

**Note:** The app might display internal server error because `SELinux` blocks apache http requests, so disable it:

``` html
$ sudo grep httpd /var/log/audit/audit.log | audit2allow -M mypol
$ sudo semodule -i mypol.pp
```


### Create virtual environment

```
# First install pip
$ wget https://bootstrap.pypa.io/get-pip.py
$ python get-pip.py

# Install virtualenv
$ sudo pip install virtualenv

# create a directory where you want to store venv environments
$ mkdir /home/surinder/venv/
$ mkdir /home/surinder/venv/py27

# go to py27 directory where virtualenv will be created
$ cd /home/surinder/venv/py27

# create virtualenv for python2.7
$ virtualenv py27

# activate virtualenv
$ source bin/activate
```

### Download pgAdmin4 from HEAD and configure/setup

```
# clone pgAdmin4 from git repository
$ git clone https://git.postgresql.org/git/pgadmin4.git/

# go to pgAdmin4 root directory
$ cd /home/surinder/dev/pgadmin4

# install python dependencies
$ pip install -r requirements.txt

# run setup.py to create username/password, database, and session storage paths.
$ python setup.py
```

### Now install NodeJS and npm

```
# enable EPL repository to get packages for nodejs, npm
$ sudo yum install epel-release (epel-release, 7-10)

# Let's install latest version of node:
go to https://nodejs.org/en/download/package-manager/#enterprise-linux-and-fedora

# Download latest version of NodeJS(v8)
$ curl --silent --location https://rpm.nodesource.com/setup_8.x | sudo bash -

# now install NodeJS
$ sudo yum -y install nodejs

# To check installation was successful, run
$ node --version
v6.10.3

# Install NPM to install Yarn
$ sudo yum install npm
```

### Install Yarn

```
# Install Yarn via RPM package repository
$ sudo wget https://dl.yarnpkg.com/rpm/yarn.repo -O /etc/yum.repos.d/yarn.repo

# run on terminal to install yarn
$ sudo yum install yarn

# to check if yarn is installed correctly
$ yarn --version
  0.27.5-1

# now install pgAdmin4 vendor libraries (such as jquery, backbone etc) via yarn
# go to /home/surinder/dev/pgadmin4/web

# now install all libraries listed in packages.json
$ yarn install

# Generate bundle of entry point libraries
$ yarn run bundle
```

**Note:** If you got an error while building packages

> ./node_modules/acitree/image/load-node.gif
> Module build failed: Error: /home/surinder/dev/pgadmin4/web/node_modules/gifsicle/vendor/gifsicle: /home/surinder/dev/pgadmin4/web/node_modules/gifsicle/vendor/gifsicle: cannot execute binary file

then force run yarn install to resolve this:
`$ yarn install --force`

or try install package which fails, for example:

```
# pgquant package failed while running yarn install
$ npm install pngquant

# Now run yarn install and yarn run bundle
$ yarn install
$ yarn run bundle
```

Restart apache service, run `sudo apachectl restart` to run pgAdmin4 server and
open url `http://localhost/pgadmin` to browse pgAdmin4.

Enjoy!
