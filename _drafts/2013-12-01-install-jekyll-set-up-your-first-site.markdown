---
layout: post
title:  "Install Jekyll and Set Up Your First Site in OS X Mavericks"
date:   2013-12-01 08:33:29
categories: jekyll
---

Installing Jekyll in OS X hasn't always been as easy as it is today. OS X Mavericks includes some improvements that make it much easier to install, and that means you can get all of the benefits of a static HTML blog with a lower time investment.

That's what we at Statiq like to call a win-win.

Now, open up Terminal and let's dive in.

##Install Xcode

Don't worry. We're not coding an iOS app. We just need some of the tools that Apple installs when Xcode is installed on your Mac. So, hit the App Store and download Xcode. [Click here to go straight to it][1].

[1]:https://itunes.apple.com/us/app/xcode/id497799835

##Download the Xcode Command Line tools

Two options here. 

First option: Open up Xcode, Preferences, Downloads and choose Command Line tools.

Second option: Fire up terminal and type:

	sudo xcode-select --install

##Install Jekyll

Jekyll used to require a bunch more prep work, installing other prerequisites. But now it's just one simple command:

	sudo gem install jekyll

There you have it. Jekyll is ready to go.

##Get your first site ready to go

It took me awhile to get used to how Jekyll works. Basically, you type a command that takes a folder of plain text content and a defined theme, and the engine runs through and combines your content and the design into your static HTML.

So let's create your content folder.

	mkdir ~/sites

This will create a 'sites' folder in your Home directory. A lot of people like this folder to be inside of their Dropbox folder. If that's you, run this command instead:

	mkdir ~/Dropbox/sites

That will create the 'sites' folder in your Dropbox root directory.

One more command:

	jekyll new ~/sites/site-name

Name your site whatever you want (probably not 'site-name').

##Test your Jekyll install

	cd ~/sites/site-name

	jekyll serve --watch

This will create a temporary host to test your site on your local machine. You can make changes in your folder and Jekyll will automatically update your site to reflect your new content. 

Let's make sure it worked. Open your browser to [http://0.0.0.0:4000/][2] to find your Hello World site with sample content and the default theme.

[2]: http://0.0.0.0:4000/