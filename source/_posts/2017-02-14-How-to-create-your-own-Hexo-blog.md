---
title: How to create your own Hexo blog
date: 2017-02-14 01:08:43
tags: [Hexo, Blog, Javascript]
thumbnail: /images/banners/hexo.jpg
banner: /images/banners/hexo.jpg
categories: [Javascript, Tutorials]
---
So why would you want to use [Hexo](https://hexo.io/) to create your blog when there are other more popular solutions out there?
Well for me there are a few important reasons.

<!-- more -->

1. It is written with JavaScript, one of the most popular programming languages today. This also makes it really easy to modify or add new features
2. Its really fast, simple and powerful. With only a few commands you can quickly create and deploy new posts
3. Posts are written in [Markdown](http://daringfireball.net/projects/markdown/). And anyone who has used [Github](https://github.com) should be familiar with it
4. It doesn't require a database and can be hosted anywhere. Hexo generates static files that can be hosted on Github, FTP server or even Amazon S3 in just a few seconds

If that convinces you to use Hexo for your blog, just follow the steps bellow and you will have it up and running in just a few minutes.

## Requirements

Two basic requirements are [Node.js](https://nodejs.org/) and [Git](https://git-scm.com/). If your computer already has these, congratulations you can skip this part and go straight to installation.


### Install Git

##### Linux (Ubuntu, Debian)

``` bash
$ sudo apt-get install git-core
```

##### Linux (Fedora, Red Hat, CentOS)

``` bash
$ sudo yum install git-core
```

##### Mac ([Homebrew](http://mxcl.github.com/homebrew/))

``` bash
$ sudo brew install git
```

##### Mac ([MacPorts](http://www.macports.org/) )

``` bash
$ sudo port install git +svn +doc +bash_completion +gitweb
```

##### Windows 

 Download & install [git](https://git-scm.com/download/win).

 

 ### Install Node.js

 ##### Linux (Ubuntu, Debian)

``` bash
$ sudo apt-get install nodejs
$ sudo apt-get install npm
```

##### Linux (Fedora, Red Hat, CentOS)

``` bash
$ sudo yum install nodejs
$ sudo yum install npm
```

##### Mac ([Homebrew](http://mxcl.github.com/homebrew/))

``` bash
$ sudo brew install node
$ sudo brew install npm
```

##### Mac ([MacPorts](http://www.macports.org/) )

``` bash
$ sudo port install nodejs
$ sudo port install npm
```

##### Windows 

 Download & install [node](https://nodejs.org/en/download/).
 

 ## Install Hexo

 ``` bash
$ sudo npm install -g hexo
```

That will install Hexo globally so you can use it anywhere.
So now create a new folder somewhere on your system. I named my "my-hexo-blog" but you can name it anyway you like.

 ``` bash
$ mkdir my-hexo-blog
```

After that use Hexo to generate files for your blog.

 ``` bash
$ hexo init my-hexo-blog
$ cd my-hexo-blog
```

When that finishes you will get something like this:

{% asset_img img/hexo-folder.png Hexo folder structure %}

Most important files are `_config.yml` which is your hexo configuration file where you can change the blog name and similar options. And `package.json` which is contains information for npm including the plugin list.

## Run locally

To be able to modify the theme and write posts you need to be able to run the blog locally. You do that run the next command.

 ``` bash
$ hexo server -d
```

Now open a browser of your choice and open `http://localhost:4000/`. You will finally be able to see your blog in all of its glory.

Now you can edit configuration files, install a theme, install plugins, write a new posts and deploy your blog.
