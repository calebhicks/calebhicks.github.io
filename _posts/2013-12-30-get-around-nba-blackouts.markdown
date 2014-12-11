---
layout: post
title:  "Get Around NBA Blackouts by Running Your Own VPN"
date:   2013-12-30 09:22:29
categories: 
tags: walkthrough sports
---

## League Pass and Blackouts

You love watching games live, but you hate paying for cable. Seems like the only reason to pay for cable anymore is for live sports. [NBA League Pass Broadband][1] seems like it'd be the perfect solution. $129 to stream every game of your five favorite teams to your Apple TV, iPad, Roku, whatever.

It's perfect. Except for **[stupid blackouts][2]**. If you live anywhere that shows Jazz games on cable, they'll block you from watching the games live on League Pass Broadband.

Since getting married, I've never paid for cable. But I didn't want to miss Jazz games. After messing around with streaming sites of ill-repute (and many ads, and super low quality streams), I had to figure out a way to get League Pass to work.

## The Solution

The trick is to make the NBA League Pass servers *think* that you're outside of Utah. You can use a service like a VPN or proxy server to do that. Basically, a VPN sends all of your traffic to a server, and then that server sends your internet requests for you, receives responses, and then sends those responses back to you.

Sort of confusing. Here's a picture of what happens with blackouts:

![NBA Blackout Blocks Your Request][3]

## What the VPN Does

And what the VPN does:

![VPN disguises your location to the NBA servers][4]

[Zoom][5]

## So how do I get a VPN?

There are a few VPN services you can pay a couple bucks a month for. But they typically limit how much you can stream through them. I wouldn't recommend them.

You can run your own, which is what I do, using a cloud server like Digital Ocean. I'm including instructions on how to set this up below. But it's not for the faint of heart. If you've never heard the words Ubuntu, shell, or terminal before, this is probably going to be too hard. You're welcome to try though!

[E-mail me][6], shoot me $30 bucks on Paypal or Venmo, and I'll send you a username and password that you can use to access *my* VPN. For what it's worth, I don't make a bunch off of that $30. Just covers bandwidth for 80%2B HD games of basketball.

## The Hard Way

Ok. Here's the meat and potatoes. You're going to be setting up your own Linux server, PPTP for tunneling, and setting up a personal VPN account through your own server.

## Sign Up for Digital Ocean

Step one. Go to DigitalOcean.com and Sign Up for a new account. Once your new account is set up, log in to your Admin Panel.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Sign up for Digital Ocean][7]

[Zoom][8]

## DigitalOcean Control Panel

Step two. You should see a giant blue Create Droplet button in the top-right corner. Go ahead and click it.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Create a new droplet][9]

## Choose Your Server Options

Step three. Choose your server options. First, enter a Hostname (this can be almost whatever you want, but I recommend a joke about Ty Corbin or Locke). Choose the cheapest option. That little machine is more than adequate to stream some games to you.

This next decision is important. Digital Ocean currently offers servers in New York, San Francisco, and Amsterdam. You will be subject to blackout rules for whichever area you choose. If you choose San Francisco, that means Golden State. If you choose New York, that probably means the Knicks, or Nets, or maybe both. If you choose Amsterdam, well, that's not any of them. Having never tried one from Amsterdam, I'm not sure if there would be major lag or not. Go crazy. I choose New York 1. I don't really have time to care about Knicks games on a regular basis.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Choose droplet options][10]

[Zoom][11]

## DigitalOcean Control Panel

Choose Ubuntu 13.04 x64, and leave Enable VirtIO on (I have no idea what this is, but it's free!). Any version of Ubuntu should work, but I'm doing mine on 13.04, so if you want to follow along with my specific instructions, choose what I choose.

Click Create Droplet.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![More droplet options][12]

## While You Wait, Check Your E-mail

Step four. Wait for your server to set up, and check your e-mail for your Root password.

The e-mail you get is important. It has all of the information you need to connect to your server.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Check your e-mail for login details][13]

[Zoom][14]

## Connect to Your Server Via SSH

Connect to your server via SSH. If you run Windows, you will need to download and use something like [PuTTY] to connect. If you run a Mac, then you can use the Terminal (use Spotlight to search for Terminal if you are unfamiliar with it).

Open your SSH client, and type ssh root@[your server's ip address] and press enter. If your IP address was 192.241.145.95, then you would type:


    ssh root@192.241.145.95.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![SSH into your server using Terminal][15]

## Copy and Paste Your Password

Copy and paste your password from your e-mail into your terminal window and press enter. You'll be logged in and ready to go.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Enter your password to get started][16]

## Smart People Use Security

There are entire professions dedicated to locking down servers from people who would use them to do bad things like send spam. We could spend all day on that, but I'm not going to. We're going to set this up in a way that you can easily blow it up and start over again if anything bad were to happen to your server.

I'm not smart.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

## Instal PPTPD

PPTPD is the application the server will use to tunnel your requests. We'll install it using the apt-get command:


    apt-get install pptpd

Confirm you want to install it by typing


    y

And pressing enter

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Install pptpd][17]

## Configure PPTPD

Type the following command to edit the configuration file:


    sudo nano /etc/pptpd.conf

Scroll to the very bottom and remove the # sign from the front of the following lines:


    #localip 192.168.0.234-238,192.168.0.245
    #remoteip 192.168.1.234-238,192.168.1.245

Leaving:


    localip 192.168.0.234-238,192.168.0.245
    remoteip 192.168.1.234-238,192.168.1.245

Save and exit by typing Control X and pressing Enter when it asks to save.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Configure pptpd][18]

## More PPTPD Configuration Stuff

Next type:


    sudo nano /etc/ppp/pptpd-options

Find the lines containing 'ms-dns' and add


    ms-dns 8.8.8.8
    ms-dns 8.8.4.4

This will set up the server to use Google's fast DNS service. If you don't know what that means, don't worry, it'll work.

Save the same way as with the last file. Control %2B X, Y, then Enter.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![More pptpd configuration stuff][19]

## Create a VPN Account


    sudo nano /etc/ppp/chap-secrets

Go to the bottom line, and put a username, pptpd, password, and an asterisk, putting a tab in between each.

Save and exit.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Create an account to login with][20]

## Allow IP4 Forwarding


    sudo nano /etc/sysctl.conf

Remove the # symbol from the line with the following text:

#net.ipv4.ip_forward=1

Leaving

net.ipv4.ip_forward=1

Save and exit.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Allow IP4 forwarding][21]

## Reboot, Just for Kicks

I don't know if this is actually necessary. But I like to do it.


    reboot

You will need to log in again using the steps before.


    ssh root@[youripaddress]

Then copy and paste your password.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

## Configure Your Mac to Connect to Your Server's VPN

Now let's check to see if we got everything set up right. Here are the steps for your Mac:

Open System Preferences.

Click on Network.

Click the + button in the bottom left corner.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Add a new VPN connection on your Mac][22]

## Configure Your Mac: Select VPN Setup

Select VPN and choose PPTP as the VPN Type. You can name the Service whatever you want.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Choose VPN option][23]

## Enter Your Password and Connect

Click on Authentication Settings and enter your password. Then click 'Connect'.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Enter your VPN server information][24]

## Check Your Connection Status

Google


    what is my ip address

We want the result to say the address of your server that you set up. If you've done it right, then you're golden! No more blackouts!

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Check your IP address][25]

## Save Your Droplet as an Image

I mentioned above how we weren't going to be too worried about Security. That's because we're going to save an image that you can use if anything goes wrong. This will save you all of the above steps, in case you set up a new server down the road. This also means you can turn your server off during the off-season, and turn it back on once the season starts (like I did!).

Log back into your Digital Ocean account, and click on Images and Take a Snapshot.

Digital Ocean will ask you to power off your server to take the snapshot. Open up the Terminal again and type:


    sudo shutdown -h now

Then try again.

After it creates the snapshot, you will be able to create new Droplets (or servers) using that Snapshot. No more configuration needed.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

![Create an image so you can shut it down and restart it][26]

[Zoom][27]

## Connecting Other Devices

You can use the same VPN settings to connect any device that allows you to connect via VPN.

Any Mac, Windows, or Linux machine. iPads, iPhones, Android devices. All of those are easy. Just find the VPN settings and enter the username and password you set up earlier.

AppleTV's, Roku's, and others may require a little bit of extra setup, as they don't give you VPN settings. You can change the settings in your Router, but that may push ALL of your traffic through an unsecured server, which is something you probably don't want. E-mail me and I'd be happy to help look into this.

_Did you have a problem with this step? [E-mail me][6] so I can fix it._

## The End!

Wow. That was long. They say it takes a great writer to keep things concise. Today, I am not that writer. I felt it would be better to make sure I fully explained everything, and I didn't have a lot of time to edit it down to the essential steps.

This is a Version 1.0 of this tutorial for you Jazz fans. It's a work in progress. I'm happy to update it if there is any confusion anywhere.

Additionally, I plan to add the following:

  1. AppleTV support and directions
  2. Roku support and directions
  3. iPad/iPhone screenshots and directions

If you want to thank me, why don't you give me a follow on Twitter (@calebhicks for general stuff, and @kelubonsports for Jazz stuff). If you don't want to hassle with setting up your own VPN server, but still want to avoid Jazz blackouts on League Pass Broadband, e-mail me (calebhicks@gmail.com) and we can work something out. I'm thinking $30 for the season and I'll give you access to my own server.

GO JAZZ!

   [1]: http://www.nba.com/leaguepass/broadband/
   [2]: http://www.nba.com/nba_tv/blackouts.html
   [3]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/The-Solution.png
   [4]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/What-the-VPN-Does-sm.png
   [5]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/What-the-VPN-Does.png
   [6]: mailto:calebhicks%40gmail.com
   [7]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Sign-Up-for-Digital-Ocean-sm.png
   [8]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Sign-Up-for-Digital-Ocean.png
   [9]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/DigitalOcean-Control-Panel.png
   [10]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Choose-Your-Server-Options-sm.png
   [11]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Choose-Your-Server-Options.png
   [12]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/DigitalOcean-Control-Panel-1.png
   [13]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/While-You-Wait--Check-Your-E-mail-sm.png
   [14]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/While-You-Wait--Check-Your-E-mail.png
   [15]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Connect-to-Your-Server-Via-SSH.png
   [16]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Copy-and-Paste-Your-Password.png
   [17]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Instal-PPTPD.png
   [18]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Configure-PPTPD.png
   [19]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/More-PPTPD-Configuration-Stuff.png
   [20]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Create-a-VPN-Account.png
   [21]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Allow-IP4-Forwarding.png
   [22]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Configure-Your-Mac-to-Connect-to-Your-Server-s-VPN.png
   [23]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Configure-Your-Mac--Select-VPN-Setup.png
   [24]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Enter-Your-Password-and-Connect.png
   [25]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Check-Your-Connection-Status.png
   [26]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Save-Your-Droplet-as-an-Image-sm.png
   [27]: https://dl.dropboxusercontent.com/u/74616/Clarify/league-pass/Save-Your-Droplet-as-an-Image.png