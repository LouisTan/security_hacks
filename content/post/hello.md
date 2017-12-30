+++
title = "My First Blog Post"
date = 2017-12-24T01:32:22-05:00
draft = true
comments = true
categories = ["Blog", "Tools"] 
description = "" 
tags = ["hello", "world", "hugo"]

+++

## The blog

For most of my posts I will assume that you are using a Linux distribution. I recommand Linux Mint, others will prefer Ubuntu. I don't suggest using Kali Linux as it may not be appropriate for day-to-day use. If you want to get your hands dirty with a specialized OS, use Parrot Security or wait for my post on Kali Linux Persistence (Encrypted) USB Bootable OS.

---

Holding a blog does not require any heavy artillery in terms of developpement. Since I am by no means a front end artist, I needed a templating system. Wordpress would have been a good option but then I came accross that article. It made me want to implement a static website to keep my articles on the client-side. No database, no worries! 

There is a bunch of static websites generators out there. My attention got caught on a Go based frameword named __[Hugo](https://gohugo.io/)__. I opted for the sober __[startbootstrap-clean-blog](https://github.com/eBlackrockDigitalffstartbootstrap-clean-blog)__ from Twitter Bootstrap adapted to Hugo by __[humboldtux](https://github.com/humboldtux/humboldtux.github.io-src)__ to lay my articles and didn't changed much to it. Using this microframework permits me to use Markdown to write my posts and automate a lot of otherwise tedious tasks.

---

### Build your own blog with Hugo

1.	Get Hugo
	- Tarball:
	- snap:
	- apt-get: I don't recommand using apt-get since you won't necessarly get the last version and you won't be able to utilize some templates.

2.	Get a template
	- Hugo default templates
	- a Github repo

3.	Configure your blog
	- config.toml

4.	Include some pages
	- #
	- #

5.	Post some articles
	- #
	- #

### Deploy you blog on a live server

1.	**Deploy locally**
	- If you used the tarball or apt-get:
	- If you used snap:

2.	**Deploy on Heroku**
	- Version you work with Github
	- Deploy on Heroku