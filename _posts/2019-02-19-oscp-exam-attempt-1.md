---
published: true
layout: post
title: "OSCP Exam Attempt #1"
categories: [oscp]
tags: [Pentesting, Exam]
---

![img](https://cdn-images-1.medium.com/max/800/0*cFufqYlUCHsfS1pI.png)

#### **Disclaimer:** 

I failed my first OSCP exam attempt. This is more just a post detailing my experiences and take aways from this OSCP exam attempt.

#### **Introduction:**

I started my OSCP journey about 3 months ago back in November 2018. I had been volunteering for my companies Red Team without much prior knowledge of a proper penetration test. My degree is a Bachelors of Science in Computer Security & Forensics. My major or program back in university was brand new so they did not have everything hashed out curriculum wise. So I took some classes here and there and one of them was to play around with Backtrack. We didn't really cover any tools and my professor just said "here's Backtrack, try running the Armitage Hail Mary" command.

Anyway, I've learned a lot of different tools, methodologies, and ways of thinking after starting to volunteer my time with the Red Team at my company. I was able to secure funding from my company to pay for my 90 day lab time and OSCP exam attempt. Before even starting my lab time I spent quite a while just downloading VMs off VulnHub. I would do fairly well with most machines I downloaded but was quite nervous to start my OSCP journey in the labs and eventually take the OSCP exam. It took a couple of my co-workers to basically say "quit being a whimp and start it already" but more in a sugar coated manner. 

#### **Starting the OSCP Journey** 

I had tried the OSCP labs once before back in 2015 but got a few weeks in before I had a loss in the family and I ultimately let my lab time expire and never scheduled an exam. As previously mentioned I started my lab time in November 2018 and ignored the exercises at first as I could always go back and do them again as I had done them back in 2015. They changed a bit since 2015 as it was Penetration Testing with Backtrack and Offensive Security had just made the swap to Kali Linux. 

My recommendation for anyone starting their journey , would be to read over the 380 page PDF document and watch the 8 hours of video content they provide. The PDF and video materials will actually help with a few servers in the lab environment you have the privilege of using after paying for it. Some of the lab machines verbatim follow the materials they give you, so definitely review them!

Keeping detailed and organized notes during the labs (and even for the exam) is crucial. My first time in the labs back in 2015 I had used KeepNote but I was not thrilled with it. This time in the labs I had used CherryTree and found a rather useful template by another student, [James Hall](https://411hall.github.io/). That template can be downloaded directly from James via https://411hall.github.io/OSCP-Preparation/ or you can get it from my site directly via https://adamluvshis.com/CTF_template.ctb. I did make a few changes to add some other tool names to scans or suggestions James had already made. 

Here's an example of my hierarchy and organization of notes:

![OSCP Lab Notes](https://i.imgur.com/244HhZ1.png)
                            

#### **Working in the Labs**

I had set a goal out for myself to try and obtain at least 5 servers a week, so about 1 server every weekday. There were times where I'd work on weekends as well but I ultimately did not want to spend all of my time on the computer as well I work on computers for a living.

I'd go to my day job and work the usual 8am to 5pm, come home eat dinner and watch an episode of a show with my girlfriend, and then get to the labs. I'd spend about 5 to 8 hours a night during the week working in the labs. Some nights I'd get 2 or 3 hosts and some I didn't get any due to the difficulty of the server, looking at you Sufferance, gh0st, and Humble...

Offensive Security recommends utilizing the image of Kali Linux they provide: https://images.offensive-security.com/pwk-kali-vm.7z - you can get more info about it: https://support.offensive-security.com/pwk-kali-vm/

I personally did not use this image in the labs, however, I did use it during the exam. That being said, I had my VirtualBox/VMWare open on one monitor and my CherryTree open on the other monitor. 

My lab time expired February 2nd, 2019 and at the end of it I had rooted 46 (including the duplicate hosts) of the 57 machines I was aware. The lab environment consists of the student network (the DMZ), the IT network, Development network, and the Admin network. 

One would have to pivot from machines in the student network to the other machines in IT, Development, and Admin networks through SSH gymnastics and other pivoting techniques. 

I was fairly confident I would do well during my exam after obtaining all but 2 systems in the student network (they apparently have dependencies on the Admin network which I did not get anything in) and systems in the other networks.

Some tips for the labs:

- The IRC bot in #offsec at irc.freenode.net is generally useless. It has a helpful hint here or there for only a few specific targets.

- The forums have some good tips if you get stuck. Try to avoid using the forums as your go-to as you won't have it for the exam. 

  - Some students also have no idea what they are talking about. 
  - I personally would look for the threads that contained "Last_IP_Octet - Hotot's Take" as this student provided useful tips without giving away the answer if I ever got stuck and needed a last resort.

- Utilize the support chat over at 

  https://support.offensive-security.com/chat.php

  - If you suck up to the admins they might just give you a hint in the right direction.

- ALWAYS revert a machine before you work on it.

  - Wait about 5 minutes after a revert. Some services do not start immediately on system reboot.

- Each machine has a "proof.txt" file located in the administrators desktop or root directory. 

- Document each step you take text + screenshot or screenshot at the very least.

- Join the PWK/OSCP Prep Discord: https://discord.gg/strQxxe - you can find me on there as FalconSpy **(FalconSpy#0512)**

#### **Game Day**

The exam was scheduled for Saturday, February 16th at 2pm local time. 

The OSCP Exam consists of 5 machines. You, the student, are provided with objectives and point values for each machine. 

- 25 point buffer overflow machine
- 25 point behemoth riddled with rabbit holes
- 2 x 20 point machines
- 10 point machine

You are provided a 6th machine to perform your debugging for the buffer overflow

I show up 30 minutes before my scheduled exam start just to make sure I am ready. 15 minutes before my scheduled exam I am allowed to start the process with my proctors. All seemed like it was going well with the proctors. I had my screen share available, my webcam feed working, connected to the VPN, or so I believed. 

I started scanning 2 hosts both running similar scans and would start to enumerate whichever machine had a scan come back first. However, none of my scans came back properly. It turns out I had issues with my VMWare network connection to the host machine which in turn had issues with the VPN. I spent about an hour with OffSec admins on the support chat trying to debug the issue. Turns out having VirtualBox and VMware both installed, they were trying to share the same virtual ethernet adapter causing my scans and connection to the VPN to fail.

I'm already down an hour from troubleshooting which wasn't ideal. 11 hours or so pass on my first machine with a few breaks in between (one of the 20 point machines) and I had found the proper exploit but just wasn't executing things on my end properly to obtain my low privileged shell. This felt pretty demoralizing and I felt the anxiety building up. I had found some suggestions on things to try after some carefully crafted Google searches and thus I finally obtained my low privilege shell. The privilege escalation came shortly after and it felt good to finally have 20 points under my belt. I felt revitalized!

It's probably about 2am my local time so 14 hours into the exam and I had just made my way into the 2nd 20 point machine with a low privileged shell. I spent probably another 3 hours trying to find the privilege escalation but nothing quite stood out even after going through my normal routines. I even ran some of the Linux Privilege Checker scripts which were adapted to bash shell scripts to make things easier (just incase the server did not have Python). Nothing particularly stood out here either. 

At this point I am about 18 to 19 hours into my exam and decide to skip over the privilege escalation on the 2nd 20 point host. I proceeded to work on the 25 point buffer overflow and had that down in about 30 minutes. I had practiced a plethora of buffer overflows in and out of the labs as this was an area I knew I was weak in before starting my OSCP journey. I was now 55 points in counting the low privileged access on the 2nd 20 point host.

I spent another 2 or 3 hours trying to find the proper privilege escalation on the one host I've acquired a foothold on but did not find anything. I ignored the 25 point host even after doing some scans. I thought I had found the proper way in or it could've been a rabbit hole. At this point I won't ever know unless Offensive Security decides to release information about decommissioned exam machines (I am not going to hold my breadth on this one).

I'm about 21 hours into my exam and I take one look at my scans for the 10 point host and I am beyond exhausted. I was up for about 30+ hours myself. I could really think of how I should go about starting this host and decided to throw in the towel and except the failure. I would use this failure as a learning opportunity for my 2nd exam attempt whenever I decided to schedule it.

#### **Lab & Exam Writeup**

Although I threw in the towel for the exam and did not create an exam writeup, I still crafted my lab write up 2 weeks before my exam was scheduled. From the moment my lab time expired up to the exam I made sure I had all the required information in my lab write up including the exercises. 

Offensive Security provides the student with a lab and exam write up template. You can use this if you wish, however, I did not. I treated my lab write up in a boot to root format. Similar to how I wrote the VulnHub Walkthroughs on the site. The admins ideally want a report that you can present to someone such that they can follow each step you took to perform the penetration test their selves. The report should include step by step screenshots, any code modifications made if required, links to exploits, etc. If you wrote any custom exploits or code, this needed to be in the report as well if used on 1 of the 10 machines you have to write a report on. You can include more than 10 but generally not worth.

Some lab machines had some data for us to exfiltrate. If one of your target machines you are reporting on has data you exfiltrated, make sure that data is in the report.

In the end my lab + exercise report was roughly 220 pages.

If I were to create an exam report for my first attempt then I'd follow the same boot to root format. This format will be used for my second attempt.

#### **Take-Aways**

1. Manage time wisely
2. Take more frequent breaks if you get stuck. I personally tried to take a break every 2 to 3 hours. 
3. Move onto another machine once you become stuck and took a break to clear your head.
4. Do not become consumed by a single machine. (For example spend 11 hours on one host like I did even with breaks).
5. If something you expect to work isn't working, it's by design. The admins might've changed something to make the exam machine harder for the student or it's to mimic a real world situation.