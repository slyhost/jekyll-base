---
layout: post
title: Internet facing SSH - The survival guide
---

SSH is a great tool, especially with the whole world embracing containers and companies announcing tiny Linux VPS's for less than the price of a sandwich. All these instances spinning up all over the internet have one thing in common, Insecure SSH severs.

Some providers will lock down SSH by default to only allow SSH Keys, which is great, but there are a lot of people that spin up machines online, at work or even at home that have port 22 wide open on their external IP's just expecting that "Nobody will hack in because they don't know my IP".

One of the biggest targets for these hacks were Raspberry Pi's. By default they used the pi:raspberry credentials with SSH enabled, people then thought "I'll port forward it and I can get to it from anywhere!". 10 minutes later and your Pi is now part of an email spam network. Luckily the Raspberry Pi foundation has changed this behaviour and disabled SSH by default and prompts you to change the pi users password before allowing you to enable it.

*Locking it down*

There are 3 main guidelines you should follow when setting up an SSH server that will be open to the internet: 

1. Never allow root login
2. Always use SSH keys and disable password authentication
3. Change the default port from 22

