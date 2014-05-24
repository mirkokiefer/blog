---
layout: post
title: "Switching from WordPress to Octopress"
date: 2013-01-19 20:40
comments: true
categories: 
---
I didn't update my blog for more than a year now!
Its not that there wasn't anything to write about - a lot has happened in the meantime.

Whenever I'm working on my notebook I keep a text editor open to keep notes about ideas or to log what I've just done. I love [markdown](http://daringfireball.net/projects/markdown/) and use that for formatting.
<!-- more -->
A lot of these notes could have become blog posts. But having to login into wordpress everytime and use their editor to reformat my posts was just too much overhead for my taste.  
Luckily I discovered [github's jekyll](http://jekyllrb.com/), which is a static site generator they use on their own site. It allows you to write your content in markdown and generate a full website with a single command.  
[Octopress](http://octopress.org/) is a small framework to simplify jekyll blogging that comes with great features readily configured:

- syntax highlighting
- Disqus comments
- third-party integration (Twitter, Google+, github, ...)
- an easy to modify default theme
- various deployment methods (github pages, rsync, ...)

As transforming my notes to blog posts should now take much less time you will see more posts coming here soon :)

I spent some time modifying the octopress classic theme to become simpler and less distracting. You can use my theme following the instructions here:

- [Setup octopress theme classic-light](https://github.com/mirkokiefer/octopress-theme-classic-light).

As I alreay have a small virtual server running nginx I just use rsync to deploy.

Relevant links:

- [Octopress setup](http://octopress.org/docs/setup/)
- [Octopress rsync deployment](http://octopress.org/docs/deploying/rsync/)
- [Migrating WordPress](https://github.com/mojombo/jekyll/wiki/blog-migrations)