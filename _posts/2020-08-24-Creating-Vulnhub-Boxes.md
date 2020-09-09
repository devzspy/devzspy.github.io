---
published: true
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

You'll first want to have some kind of hypervisor. I would recommend [Oracle Virtualbox](https://www.virtualbox.org/) since it's free. It appears VMWare Player, which was free is now VMWare Workstation Player. There is a free version for non-enterprise users which is what we are.

If you have VMWare Workstation Pro, ESXi, or Hyper-V they should work also. I won't be covering a full VM creation as it's fairly straight forward. I will only provide some concepts that will be useful for when the VM has already been created.

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

## Building the Box

For this section, I will only be providing general concepts and things you should consider doing for your box once it's booted up.

### Hardware Requirements

You should try to give the VM as little resources as required. Basically, give the VM enough resources to perform the tasks it needs. 

There is no need to give a VM hosting a website 16GB of RAM and 8 cores. 

Start with the least amount of resources and if necessary increase them until the VM is working optimally.

As for the hard disk size, see what the recommended size is and give it +1 GB more just for good measures.

### Selecting OS

Pick your flavor of Linux OS whether it be CentOS, Ubuntu, Arch, etc. This is what your targets will be attacking. You can pick an old kernel version / old OS version if you wish. I prefer to use the latest and greatest to limit the unintended privilege escalation methods.

### Networking

When creating a box there are two preferred network connection types to use in VMWare, Virtualbox, etc. These two preferred network types are: Internal and Host-Only.

**Internal:** Allows two VMs to communicate with one another. The host and internet will not be able to reach the VMs.

**Host-Only:** Allows the host to communicate with the VM and the VM to communicate with other VMs.  This is the preferred network setting type incase you need to use the host for troubleshooting.

See the below graphic for a better breakdown and understanding of the different network setting types.

![](https://i.imgur.com/lFVbZdQ.png)

### Creating Intended Foothold & Privilege Escalation

Once you've got the OS setup & networking setup, this is the part where you would start to deploy the intended paths for initial foothold and privilege escalation.

Since I am only covering concepts, just take the pseudocode from before and actually put it into action. Maybe make things more difficult for the user by removing access to commands like **wget**. Totally up to you on what you wish to do with the box!.

## Outro

In closing, when creating a box for Vulnhub, consider your intended audience and tailor the box towards them. This will hopefully provide the most optimal experience for those of your intended audience.
