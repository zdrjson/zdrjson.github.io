---
layout: post
title: "Configuring a Godaddy domain name with github pages"
date: 2016-06-26 21:41:39 +0800
comments: true
categories: 
---

##配置顶级域名 xxx.com
	1.	Set up my user page arsturges.github.io
	2.	Commit a file called CNAME with one line: andrewsturges.com
	3.	Go to GoDaddy site to manage my URL
	4.	Add an "A (Host)" record with "host" = @ and "Points to" = 192.30.252.153
	5.	Add a "CNAME (Alias)" record with "host" = www and "Points to" = arsturges.github.io
	6.	Wait for changes to propogate.
	
##Reference
* [Andrew's blog](http://andrewsturges.com/blog/jekyll/tutorial/2014/11/06/github-and-godaddy.html)
* [使用 Octopress+GitHub Pages 搭建个人博客](http://blog.leichunfeng.com/blog/2014/11/11/use-octopress-plus-github-pages-to-setup-a-personal-blog/)
* [从DNS到github pages自定义域名 -- 漫谈域名那些事](http://winterttr.me/2015/10/23/from-dns-to-github-custom-domain/)
* [象写程序一样写博客：搭建基于github的博客](http://blog.devtang.com/2012/02/10/setup-blog-based-on-github/)

