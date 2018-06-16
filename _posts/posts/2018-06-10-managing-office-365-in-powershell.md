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
# Get credentials$Credentials = Get-Credential# Establish session$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication  Basic -AllowRedirection# Import sessionImport-PSSession $Session
```

_Make sense? Great. You're good to go!_

If that doesn't make sense... I'll explain. 

First, you need credentials. Get-Credential opens up a box to let you put these in, $Credential is a variable that stores these details in so they can be referenced by other commands. (This step can actually be skipped, if you run the second command on it's own and $Credential is empty, it will prompt for them anyway).

Next, we need to establish a session on the 365 server. This opens up a powershell connection to office 365 and allows you to import the commands. It's a bit strange the way it does this, but it works! This session is then stores in $Session. 

We then need to import the session into our current powershell session... Sounds complicated, but it's easy. Just Import-PSSession $Session and you're done!

What this does, it bring in the commands from the 365 server so you can run them locally. The changes will then be pushed up to office 365 and take effect almost immediately. Making changes this way is **much **faster than using the admin portal and is much more reliable. Also, You can script it to make it even faster!
