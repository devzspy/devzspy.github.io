---
published: false
layout: post
title: Creating Boxes for Vulnhub
categories:
  - Vulnhub
tags:
  - walkthrough
  - vulnhub
  - Tutorials
---
## Introduction

If you're viewing this you're most likely interested in developing your first box for Vulnhub.

For those that are unaware of what Vulnhub is: Basically a website for individuals to upload vulnerable virtual machines (VMs) for others to perform assessments against to hone their skills.

You can find it at [Vulnhub](https://vulnhub.com). 

There are a few things you should consider before starting the development of your vulnerable box. Think of this like coding. We "pseudocode" our box with the target audience, intended user paths or footholds, intended privilege escalation paths, and finally if you wish to include any rabbit holes. Once we have all of the aforementioned pseudocode down on paper or whichever application for notes, we can start to develop the box.

You'll first want to have some kind of hypervisor. I would recommend [Oracle Virtualbox](https://www.virtualbox.org/) since it's free. It appears VMWare Player, which was free is now VMWare Workstation Player and now requires a license.

If you have VMWare Workstation Pro, ESXi, or Hyper-V they should work also. However, I am mostly going to cover the creation of a VM using Virtualbox

## Pseudocode

### Target Audience

For our box, we need to determine how difficult we are going to make this box. If we want to target a person that's never done a penetration test before or wants to break into the field we may want to include plenty of hints and tips. We may also want to consider making things extremely easy for them in terms of exploits or ways to get in. 

If we would like to target someone that has some experience but might be lacking some necessary skills, we can have less hints and maybe work on the fundamentals. Maybe, just maybe even throw a rabbit hole in their face. 

Then there are the more advanced users. You can provide absolutely no hints, riddle your box with rabbit holes, or just make the intended pathes a giant pain to do. 

In the end whichever demographic of users you intend to target will basically lay out the other steps of the box.

### Intended Foothold

This is the part where determine how the person whose downloaded our box is going to break into it to get their shell access. 

There are a number of different pathes you can utilize as the creator. The most common is having some form of web app that has a vulnerable aspect to it. 

Just a few examples:

* Web application with default credentials. The web application then has some form of upload or editing of files
* A Local File Inclusion (LFI) or Remote File Inclusion (RFI)
* Weak NFS permissions (NFS path has write access)
* Private SSH Key stored somewhere by accident
* SQL Injection

You get the idea. There are tons of ways you can go about this. 

### Intended Privilege Escalation

This is the part where you determine how the user is going to get root on your box to print out your root.txt file or whatever you call your flag file. 

Similar to the intended foothold, the skies the limit on methods of privilege escalation. If you need some ideas feel free to check out the right side of this image:

![](https://camo.githubusercontent.com/acb487594dbe457b6711a0a70eb545ec828159a8/68747470733a2f2f7062732e7477696d672e636f6d2f6d656469612f44415a73453256555141415f62705a2e6a7067)

### Rabbit Holes

These are intended to be red heirings. They are to steer the attacker of your box down the wrong path so they spend minutes, hours, or even some days banging their head to get shell access or root. 

Depending on your target audience, you can either fill this sucker up with them or have none at all. Again you are the creator.

## Building Our Box

I won't be providing full step by step instructions / screenshots for every step of the creation. For this section, I will be mostly including the important steps.

### Creating the Box

For this, download an image of any Linux OS. I prefer to just use Ubuntu for my boxes but you may use whatever pleases you.

Once you've downloaded the ISO, open VirtualBox adn click on New (see red box). Then enter the name of the machine, the OS type (Linux) and select the flavor of OS from the version drop down

![](https://i.imgur.com/9paGmVX.png)

Go ahead and then allocate the VM some RAM and disk space. Usually giving the VM about 1GB of RAM and 12GB of disk space is more then enough. Seeing as the recommended size is usually around 10GB. 

For the "Hard Disk File" type, I would recommend the VMDK (Virtual Machine Disk) so this could place nicely down the road with VMWare.

