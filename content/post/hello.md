+++
title = "Blogging with Hugo"
date = 2017-12-24T01:32:22-05:00
draft = false
comments = true
categories = ["Blog", "Tools"] 
description = "" 
tags = ["web", "developpement", "hugo"]

+++

## Blogging with Hugo

Holding a blog does not require any heavy artillery in terms of developpement. Since I am by no means a front end artist, I needed a templating system. Wordpress would have been a good option but then I came accross that article. It made me want to implement a static website to keep my articles on the client-side. No database, no worries! 

There is a bunch of static websites generators out there. My attention got caught on a Go based frameword named Hugo. I opted for the *startbootstrap-clean-blog* from Bootstrap themes adapted to Hugo by humboldtux to lay my articles and didn't changed much to it. Using this microframework allow me to use Markdown to write my posts and automate a lot of otherwise tedious tasks.

### Build your own blog with Hugo

1.	Install Hugo

	- Tarball: Download the appropriate [file](https://github.com/gohugoio/hugo/releases) and tar `-xvzf ~/Downloads/hugo_X.Y_osx-64bit.tgz` More details informations can be found [here](https://gohugo.io/getting-started/installing/).
	- Snap: First install [sdnap](https://docs.snapcraft.io/core/install) with `sudo apt-get install snap` then `snap install hugo`
	- Apt-get: `sudo apt-get install hugo` Since it might not be the latest version, it may cause a problem of template compability. It did to me.

2.	Create a new site with a template:

	- Create the website `hugo new site my-blog`
	- Browse the official [Hugo default themes](https://github.com/gohugoio/hugoThemes) and select your favorite layout.
	- Add the template files and initialize a github repository. Let's say you choose the startbootstrap-clean-blog theme, then you would type this:  
	`cd my-blog && git init && git submodule add https://github.com/humboldtux/startbootstrap-clean-blog.git themes/startbootstrap-clean-blog`

3.	Configure your website using something like `nano config.toml`.

	```
	#baseURL = "/" #local
	baseURL = "https://security-hacks.herokuapp.com"
	title = "Security Hacks"
	canonifyurls = true
	paginate = 10
	theme = "startbootstrap-clean-blog"
	languageCode = "en-us"
	copyright = "Code released under the Apache 2.0 license."	

	[author]
	  name = "Lotana"

	[params]
	  DateForm = "Sun, Dec 24, 2017"
	  Description = "A blog on information security"
	  Author = "Lotana"
	  Ganalytics = "get-your-own"
	  disqusShortname = "get-your-own"
	  postSummariesFrontPage = 3

	[[params.social]]
	  title = "twitter"
	  url = "https://twitter.com/security_hacks"
	[[params.social]]
	  title = "github"
	  url = "https://github.com/security-hacks"
	[[params.social]]
	  title = "rss"
	  url = "https://www.specificfeeds.com/securitydhacks?subParam=followPub"

	[[menu.main]]
	  name = "Home"
	  url = "/"
	  weight = 1
	[[menu.main]]
	  name = "About"
	  url = "/about"
	  weight = 2
	[[menu.main]]
	  name = "Archive"
	  url = "/post"
	  weight = 3
	[[menu.main]]
	  name = "Contact"
	  url = "/contact"
	  weight = 4
    ```


4.	Include some pages and post an article

	- Add pages pages `hugo new about.md && hugo new archive.md && hugo new contact.md` 
	- Add you first blog post `hugo new post/hello.md`. Use [Markdown](https://markdown-it.github.io/) instead of HTML.  
</br>

### Deploy you blog on a live server

1.	Deploy locally
	- If you used the tarball or apt-get `hugo server -D`
	- If you used snap `snap run hugo server -D`
	- Your site should be available locally on *localhost:1313*

2.	Deploy on Heroku
	- Version you work with [Github](https://github.com/humboldtux/humboldtux.github.io-src) on the master branch
	- Access your [Heroku](https://www.heroku.com/) dashboard and deploy the master branch
	- Your site should be publicly available on *my-blog.herokuapp.com*  
</br>