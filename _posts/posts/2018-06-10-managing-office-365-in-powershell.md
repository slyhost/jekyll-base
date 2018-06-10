---
layout: blog
title: Managing Office 365 in Powershell
date: '2018-06-10T19:05:02+01:00'
thumbnail: /images/uploads/powershell_5.0_icon.png
---
If you've spent any time with the Office 365 partner portal, you'll know how frustrating it can be... If not, Let me explain... 

Basically, Microsoft's "Modern" versions of their management portals seem to cache everything and cause chaos with cookies. On multiple occasions, we've had to log out fully when managing another tenant due to the semi-persistent cookies it creates that define which admin portal you log into. One moment you will be editing the title of a client's SharePoint site, Next minute your boss runs in wondering why your main site now shows as "Contoso Engineering". 

## Powershell Time

Hopefully if you've been in It for more than a few seconds, you'll know what powershell is. If not, you're missing out! Check out the Microsoft Virtual Academy for some handy videos to get you started. 

Powershell is a command line interface designed with automation in mind. If you can do it with a GUI, it's pretty likely you'll be able to script it in Powershell and run it in a few seconds accross multiple machines. It's pretty handy for automating installations of software (I personally have a few scripts to set up machines for clients right out of the box). 

One really good feature is that Office 365 supports remote powershell commands, you can essentially start a Powershell session with a 365 server and execute commands inside your tenant. This makes management of everything in there super fast and much more reliable. 

## Connecting to 365

First things first, Let's figure out how to get a session open to Office 365. For this example, we'll connect up to the Exchange Online service directly and show how to manage mailboxes. 

```
$Credentials = Get-Credential
```
