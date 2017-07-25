# My personal blog

This blog is using [Left](https://github.com/holman/left/fork) theme based on [Jekyll](https://github.com/mojombo/jekyll).

## Setup

Contributions are Welcome!

- [Fork this repository](https://github.com/imsurinder90/imsurinder90.github.com.git)
- Clone it: `git clone https://github.com/imsurinder90/imsurinder90.github.com.git`
- Install ruby things: `bundle install` (if this doesn't work, look into [installing Bundler](http://bundler.io))
- Start it up: `script/server`

You should have a server up and running locally at <http://localhost:4000>.

## Steps to change post content:

Project layout:

````
├── _config.yml
├── _includes
│   ├── head.html
│   └── sidebar.html
├── _layouts
│   ├── layout.html
│   └── post.html
├── _posts
│   ├── 2017-07-22-pgAdmin4?.markdown
│   ├── 2017-07-22-setup_pgAdmin4_in_desktop_mode.markdown
│   └── 2017-07-22-setup_pgAdmin4_in_server_mode.markdown
├── _site
│   ├── 404.html
│   ├── CNAME
│   ├── Gemfile
│   ├── Gemfile.lock
│   ├── LICENSE
│   ├── README.md
│   ├── about.html
│   ├── apple-touch-icon.png
│   ├── atom.xml
│   ├── css
│   │   ├── base.css
│   │   ├── mobile.css
│   │   └── pygments.css
│   ├── favicon.ico
│   ├── images
│   │   ├── hr.png
│   │   └── profile_pic.png
│   ├── index.html
│   ├── js
│   │   └── application.js
│   ├── posts
│   │   ├── pgAdmin4.html
│   │   ├── setup_pgAdmin4_in_desktop_mode.html
│   │   └── setup_pgAdmin4_in_server_mode.html
│   ├── script
│   │   └── server
│   └── sitemap.xml
├── about.html
├── apple-touch-icon.png
├── atom.xml
├── css
│   ├── base.scss
│   ├── mobile.scss
│   └── pygments.css
├── favicon.ico
├── images
│   ├── hr.png
│   └── profile_pic.png
├── index.html
├── js
│   └── application.js
└── script
    └── server
````

1. Open post you want to change in `_posts/` directory with your favourite editor.

2. Save and close file after making changes in files.

3. Set Remote Url to repository Url.

  <pre>git remote set-url origin https://github.com/imsurinder90/imsurinder90.github.com.git</pre>

4. Stash the changes you made:

  <pre>git add filename1 filename2</pre>

4. Commit and push the changes.

  <pre>git commit -m "Add description of changes"</pre>

4. `git push`

## Licensing

[MIT](http://www.opensource.org/licenses/mit-license.php) License

© 2017 Surinder Kumar (imsurinder90@gmail.com)
