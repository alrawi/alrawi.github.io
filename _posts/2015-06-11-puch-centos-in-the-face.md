---
layout:     post
title:      Punching CentOS in the Face!
date:       2015-06-11 00:53:29
summary:    Highlighting some frustration with CentOS interface renaming and configuration.
categories: rants infrastructure
---

### Ranty version
My OS of choice is CentOS 6.x hands down, but sometimes, especially in virtualized environment, I want to punch CentOS in the face. Here I am going to detail an issue that wasted a good 2 hours of my life. I have an oVirt controller node, which has 3 interfaces, management, NFS, and Internet.
- eth0 - management
- eth1 - NFS
- eth2 - Internet

I couldn't talk out on any of the interfaces and the root cause was the naming of the interfaces. So I am pretty lazy and I use cp a lot. I cp'ed ifcfg-eth0 ifcfg-eth1 and ifcfg-eth2. I forgot to change the MAC address and all hell broke loose. Now you have different naming associated with an interface and I thought I was doing it right... \<head shake\>... I wasn't. I caught the problem when I brought down all the interfaces using ifconfig ethX down except for one of the interfaces and realized the lights of the interface was still on. The one I kept up was off. So basically I knew right away what happened and without further ado I present the solution


### TL;DR! Solution
go here:
> /etc/udev/rules.d/70-persistent-net.rules

note the MAC address and the interface name. Modify them to match what you want. Then go here:
> /etc/sysconfig/network-scripts/ifcfg-ethX #incorrectly named interface and make it consistant with the file earlier.

Done!
