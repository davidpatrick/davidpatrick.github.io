---
layout: post
title:  "Starting a Blog with Jekyll"
date:   2014-09-15 14:34:25
categories: jekyll poole ruby
tags: featured
image: 'http://i.imgur.com/gVHPdME.png'
---

When searching where to host our team’s blog we wanted to stay close to the community that we were trying to give back to. [Github Pages](http://pages.github.com/) immediately stood out and with the cost of $0 it’s perfect.  Github Pages allows us to keep using the same tools we use everyday in Development for Blogging.

## Where to Start?
The first thing you will want to do is choose a static site generator.  To make it easy for you I’ve read through quite a bit material and the top 2 imo are:

* jekyll (ruby)
* cabin (javascript)

Both have their advantages but since I need some material for the next Ruby Meetup we are going to start this blog with using Jekyll.  

## Getting Started

[Github Pages](https://pages.github.com/) is straight forward and easy to follow.

[Jekyll](http://jekyllrb.com/)  is even easier to install
 ```gem install jekyll```

There are a ton of resources and tools from here to get you started with Jekyll.  One of the most common is [Octopress](http://octopress.org/).  But I like starting from something even more basic.  That’s where I found [Poole](https://github.com/poole/poole). 

Even more so let’s start from one of its themes [Hyde](https://github.com/poole/hyde). Download the [source code](https://github.com/poole/hyde/archive/master.zip) and extract it into our new project.

Let’s take a look at the file structure.  You will see some files/folders with underscores.  Every thing without an underscore will get copied into to the _site folder on build.

If you open up /_layouts/post.html  you will see handlebars used for injecting content.  This is using the [Liquid Markup Language](http://liquidmarkup.org/). 

### Configuring Poole
There are few things we will need to do configure Poole
  
  * First, unelss you are using a custom domain is to remove the CNAME file, otherwise edit it with your domain.

  * Second, let’s set customize the _config.yml to fit our blog.

  * Third, remove the default blog posts under the _posts folder and write your our first post.

That’s it! Now run ```jekyll build``` Commit and push!

You can add [Disqus Comments](https://help.disqus.com/customer/portal/articles/472138-jekyll-installation-instructions) and customize it a ton of different ways. Good luck