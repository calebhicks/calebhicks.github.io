---
layout: post
title:  "Getting Started With Way Away"
date:   2013-12-03 07:10:29
categories: jekyll
tags: one two three
---

![My helpful logo example](/images/hammock-way-away.jpg)

Welcome to Way Away, a beautiful, simple blog theme by Statiq. First, a special thanks to all of our Lifetime Members, who helped in getting Statiq off of the ground.

##What is Statiq?
Our mission at Statiq is to help you build beautiful, ridiculously fast websites. We make static HTML blogging engines more accessible by providing tools and themes to take advantage of them.

We are just like you. We run our own sites. We set up sites for other people. We want those sites to be fast, rock solid, and easy to update. Sure, we could dive into the HTML, but our clients won't.

Static site engines can run sites of all shapes and sizes - from a small family blog to some of the largest corporations in the world.

## What is Way Away?

Way Away is our second theme. It is a beautifully simple take on blogging that puts the focus where it should be - on your words.

This is version 1.0, and we recognize that it is not perfect. We want to hear your feedback so we can continue to improve it by adding features.

It is currently built for use with Jekyll, with a Pelican version coming soon.

Let's get started:

## Installing Jekyll

If you haven't yet installed Jekyll, here's a quick walkthrough to get set up:

[Install Jekyll and Set Up Your First Site][3]

Now run the Jekyll command in the directory for the Way Away theme.

	jekyll serve --watch

And open up the site in your browser.

[3]: /2013/install-jekyll-set-up-your-first-site/

## Using Way Away

Open up the _config.yml file in the root directory of the theme. This is where you get to set up your basic options, including:

* Site name
* Site description
* Author name
* Contact e-mail
* Logo
* URL
* Permalink settings
* Mailchimp subscriptions
* Custom site search
* Social media accounts
* Navigation links
* Google Analytics
* Disqus comments

The --watch flag on the Jekyll command will regenerate your site when you modify or add any file in the folder, with the exception of the _config.yml file. So we need to run the command again.

	jekyll serve --watch

Way Away should be up and running with your options!

## Customizing Way Away

While our themes are designed to be usable out of the box, feel free to change **anything** about them. Dive into the CSS or template files, change them up, make the design yours!

## Writing Posts

Put new posts into the _posts folder in the root directory of the theme folder. They need to have the date info preceding the post name (ex. 2013-12-3-hello-world.markdown) to get processed by Jekyll. Use the Front Matter options provided in the '2000-1-1-default' post to get started.

## Creating Pages

You can create a new page by putting a markdown or HTML file in the root directory of the theme folder. You can use YML Front Matter (the info at the top of the blog posts) to customize the info. Choose the 'page' option for your layout. This will create a new page at the URL you selected.

## Feedback

We love your feedback! Please [e-mail us][4] your comments, questions, and feature requests!

[4]: mailto:hello@statiq.io
