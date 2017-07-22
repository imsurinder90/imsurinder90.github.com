---
layout: post
title: Setup pgAdmin4 on Ubuntu in Desktop mode
category: posts
---

In this tutorial we will be using Qt-5.5.1 with webkit and assuming you have setup pgAdmin4 in server mode by following tutorial

### Step by step instructions:

* Setup pgAdmin4 first if you have not setup yet.
* Download [Qt-5.5.1][download_link] from Qt website
* cd to pgAdmin4 directory where pgAdmin4 codebase is present and activate virtual environment.

### Qt has dependency of few libraries which has to be installed first.

``` html
sudo apt-get install opengl-dev
sudo apt-get install mesa-common-dev
sudo apt-get install libgl1-mesa-dev
```

### Check python installation directory and set `PYTHONPATH`

``` html
# which python (assuming virtual environment is activated)
output: /home/surinder/virtualenvs/p27/bin/python

# set PYTHONPATH on terminal
export PYTHONPATH=$PYTHONPATH:/home/surinder/virtualenvs/p27/lib/python2.7/site-packages/

# change directory to runtime folder
cd runtime

# compile and make pgAdmin4 binary
/home/surinder/Qt5.5.1/5.5/gcc_64/bin/qmake "DEFINES +=PGADMIN4_USE_WEBKIT"

# run make
make

# Now run pgAdmin4 in Desktop mode
./pgAdmin4
```

### Follow the setps to enable inspector tools:

* create a new file `config_local.py` to override settings defined in `config.py`

* Edit `config_local.py` and write

  ```
  SERVER_MODE=False
  DEBUG=True
```

* open file `web/runtime/BrowserWindow.cpp` and paste below line after `#endif` at line:90

  ```
  QWebSettings::globalSettings()->setAttribute(QWebSettings::DeveloperExtrasEnabled, true);
  ```

* Now run

  ```
  make clean & make & ./pgAdmin4
  ```

That's it. Now enjoy pgAdmin4 in Desktop mode.


---

[jekyll]: https://github.com/mojombo/jekyll
[download_link]: https://download.qt.io/archive/qt/5.5/5.5.1/
[left]: https://github.com/holman/left#readme
[twitter]: https://twitter.com/holman
