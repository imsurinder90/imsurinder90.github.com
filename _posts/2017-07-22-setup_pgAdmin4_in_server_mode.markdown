---
layout: post
title: Setup pgAdmin4 on Ubuntu in Server mode
category: pgAdmin4
comments: true
---

### Steps by step instructions:

``` html
# Run on terminal to upgrade package repository
sudo apt-get upgrade

# Install python dependencies
sudo apt-get install python-pip python-dev build-essential

# Upgrade pip to lastest version
sudo pip install --upgrade pip
```

### Steps to install virtual environment:

It is always recommended to use virtual environment to manage multiple version of python for pgAdmin4,
becuase pgAdmin4 supports various variants of Python

### Install following packages:

``` html
sudo pip install virtualenv virtualenvwrapper

# backup .bashrc file first
cp ~/.bashrc ~/.bashrc-org

printf '\n%s\n%s\n%s' '# virtualenv' 'export WORKON_HOME=~/virtualenvs' 'source /usr/local/bin/virtualenvwrapper.sh' >> ~/.bashrc

# Activate Virtual environment
source ~/.bashrc # reload .bashrc

mkdir -p $WORKON_HOME

mkvirtualenv pgAdmin4_27 (pgAdmin4 with python 2.7)
```

Tips: you can activate virtualenv by running command `workon pgAdmin4_27`

### Install latest version of Git

``` html
sudo apt-get update --fix-missing

sudo apt-get install git
```

### Install NodeJS and Yarn

``` html
sudo apt-get update

sudo apt-get install nodejs

# install npm(node package manager)
sudo apt-get install npm

# install Yarn package manager globally(-g)
npm install -g yarn
```
Now we have installed all prerequisites for pgAdmin4.

### Pull latest pgAdmin4 codebase from master branch

``` html
create a directory named "~/Documents/pgAdmin4" and cd to it.

git pull https://git.postgresql.org/git/pgadmin4.git/ ./

# Activate virtual env if not activated
workon pgAdmin_27

# install all python dependency to pgAdmin4
pip install -r requirements.txt

# install all dependent packages to pgAdmin4
cd web and run `yarn install`

# Run pgAdmin4 server and browse to 'http://127.0.0.1:5050'
python pgAdmin4.py
```

Thats it. Now you have setup pgAdmin4.

---