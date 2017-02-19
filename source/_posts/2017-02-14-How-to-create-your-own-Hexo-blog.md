---
title: How to create and deploy your own Hexo blog
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

Now its time to run the blog locally. You do that by running the next command.

 ``` bash
$ hexo server -d
```

Now open a browser of your choice and go to `http://localhost:4000/`. You will finally be able to see your blog in all of its glory.

Now you can edit configuration files, install plugins, install a theme, write a new posts and deploy your blog.

## Configuration

Main configuration file is `_config.yml`. Its written in [YAML](http://www.yaml.org/). You can open and edit it with any text editor.
Some important options you should set first are `title`, `author` and `url` of the blog.
One other option I prefer setting in the start is `new_post_name`. I set it to something like `:year-:month-:day-:title.md`. It defines the format of the title for the post files. Makes later organization much easier.

## Plugins

You can browse all the available plugins by going to official [Hexo plugins page](https://hexo.io/plugins/). There are about 183 available at the time of writing this post. They have various functions and give some useful features. One you should definitely look in to is [hexo-admin](https://github.com/jaredly/hexo-admin). Its one of the most popular ones and it gives you an admin interface for your blog. One more you could find useful is [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git) which enables you to deploy your blog directly to Github.
You can install plugins by adding them to the `dependencies` section of the `package.json` and following some extra instruction on the plugins Github page.
After that run `npm install` to download them and you are set to go. 


## Theme

You can browse all the available themes by going to official [Hexo themes page](https://hexo.io/themes/). There are quite a few now.
After you find a theme you like, find its Github page with the instructions how to install it. Some require just a clone of the repo, while some require some extra plugins or configuration.
After you install the theme you can modify it by editing its `_config.yml`, template and CSS files. Templates are written with [EJS](http://www.embeddedjs.com/) so they are easy to modify.
For example my blog uses modified [Icarus Theme](https://github.com/ppoffice/hexo-theme-icarus).

## Writing posts

To start writing posts you need to create one. You do that by running the next command:

``` bash
$ hexo new post <title>
```

After that find the post file in the `./source/_posts` folder and edit it as you wish with your favorite text or [Markdown](http://daringfireball.net/projects/markdown/) editor.

## Deployment 

After you are finished with configuring your blog, and writing the posts you will probably want to deploy it somewhere so other people can find it and read it. No point in having a blog otherwise.
There are a few methods available to you. Most popular seems to be to deploy it to Github. I personally deployed my to an AWS EC2 instance because I already had one for my [CV](https://cv.predovan.com) site.


### Github

For deploying to Github you need to use the [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git) plugin. Just install the plugin and follow the instructions on its Github page. Than add this to your `_config.yml` file and fill the required information. 

``` yaml
deploy:
  type: git
  repo: https://github.com/username/your-blog-url.github.io
```

Than run:

``` bash
$ hexo deploy
```

It will automatically build your static files and deploy them to a repo of your choice. But beware it does so with the -f flag so it automatically override all the files in that repo.
After that go to settings for that repo and enable `GitHub Pages`.

And that is it. Your blog will be avaliable on `http://<your-github-username>.github.io/`.


### AWS EC2

For deploying on AWS EC2 I used [hexo-deployer-shell](https://github.com/HakurouKen/hexo-deployer-shell) plugin. That is just a simple plugin that enables you to use any shell scripts for deployment. So I simply used `scp` command to transfer all the files to the server. You also need to add allow the use of port `22` in your EC2s Security Group.
So my `_config.yml` looks something like this:

``` yaml
deploy:
  type: shell
  command: scp -ri <path-to-private-key-file> public/* <server-user>@<server-ip>:/var/www/html/blog
```
And after that you run:

``` bash
$ hexo generate && hexo deploy
```
And your static files will be generated and deployed to your server.

## Conclusion

And that is it. Now you have your own private blog that you can easily and quickly modify and add to.
Hope you have enjoyed this post and that you have fun with your new blog. If you have any questions, feel free to ask them below in the comments or use any of the other contacts in the profile.
