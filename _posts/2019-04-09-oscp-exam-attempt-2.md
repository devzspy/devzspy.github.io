---
published: true
layout: post
title: "OSCP Exam Attempt #2"
categories: [oscp]
tags: [oscp, Pentesting, Exam]
---

![img](https://cdn-images-1.medium.com/max/800/0*cFufqYlUCHsfS1pI.png)

#### Disclaimer

I failed my second OSCP exam attempt. This is more just a post detailing my new experiences the second time around. Additionally, I’ll be adding to the take-aways from my first attempt.

For those of you first tuning in, should you wish to review my first attempt you can do so here:  https://devzspy.github.io/oscp/2019/02/19/oscp-exam-attempt-1.html 

### **Introduction**

A month after failing my first exam attempt with 55 points, I was determined to try again. I had planned out my method for attacking the exam the second go around. I had also tried to work on various areas that I felt I was weak during my first exam.

In the end, I failed my second attempt with 55 points again. However, I have a hunch on what I needed to do in order to get 75 points. In the end though, I will never know unless I receive the same 5 exam machines which I doubt will happen.

### **Practicing More via HackTheBox**

I had purchased a year subscription to [HackTheBox](https://www.hackthebox.eu/) and looked up all of the hosts that were OSCP like:

![img](https://cdn-images-1.medium.com/max/800/0*lax4Z4nsiWcz1qVF.png)

In order to access the above machines a user must purchase the HTB Subscription or as they call it VIP status. This allows a user to access retired boxes, reduce the number of users attacking a machine, and see guides on how to complete retired boxes only. In addition to purchasing HTB VIP, the machines also must be in rotation that week.

Every week VIP users can “upvote” a system to be in the Retired pool for the following week. Every Monday morning around 2am GMT the servers that received the most votes (up to 20) are enabled while the others become disabled.

Each week I would attempt to complete all of the active OSCP like hosts. Some of the hosts only the low privilege user was OSCP like or only the privilege escalation.

I would watch videos produced by [IppSec](https://www.youtube.com/channel/UCa6eh7gCkpPo5XXUDfygQQA) on YouTube to see how he would tackle a machine or look for some general tips. IppSec produces a video for just about every Retired machine. Highly recommend watching his videos.

### **Acquiring Additional Useful Tools**

After failing my first exam, I went about trying to find some other tools that would automate tasks I would normally perform or help with time management.

- Running various nmap scans
- Performing LFI Fuzzing
- Pretty Tmux / Tmux Logging
- Video Recording
- Time Tracking Software (Just something I wanteed)
- Mind Mapping Sofware

**Nmap Scanning**: one of the Administrators on the PWK/OSCP Prep Discord server ( https://discord.gg/strQxxe ) has created a tool called AutoRecon - https://github.com/Tib3rius/AutoRecon

**LFI Fuzzing:** A WAPT (Web Application Pen Testing) program called goWAPT — https://github.com/dzonerzy/goWAPT

**Tmux:** I had installed something called “[Oh My Tmux](https://github.com/gpakosz/.tmux)” — https://github.com/gpakosz/.tmux which just makes things look nice and easier to manage tmux sessions. You can grab a copy of my .tmux.conf via https://github.com/devzspy/.tmux

I had also used a plugin called tmux-logging which can be found here: https://github.com/tmux-plugins/tmux-logging — essentially this allows a user to capture everything that has occurred in a tmux session window / pane after the fact or real time logging.

**Video Recording:** For those that are familiar with streaming on various services like Twitch, YouTube, Facebook etc, this will come as no surprise. That being said I had use Open Broadcaster Software Studio aka OBS Studio. I used this to record everything on the two monitors so I can go back to grab screenshots or just to have incase.

![img](https://cdn-images-1.medium.com/max/800/0*oETLKLqOv8LOSOCN.jpg)

**Time Tracking Software:** I had utilized the program website Toggl — https://toggl.com/. I was able to track how long I spent on each machine. This was also useful for time keeping as I intended to take a break after working on any host for 2 hours.

![img](https://cdn-images-1.medium.com/max/800/0*VI8XEcbNpdpbxPHN.png)

**Mind Mapping Software:** For this I used a free tool called FreeMind which can be acquired here https://sourceforge.net/projects/freemind/ — I used this to keep my thoughts in track as I went through each host.

![img](https://cdn-images-1.medium.com/max/800/0*YCrPvZvklDGG0QqO.png)

### **Game Day….Again**

The exam was scheduled for Saturday, April 6th, 2019 at 1pm local time.

The OSCP Exam consists of 5 machines. You, the student, are provided with objectives and point values for each machine.

- 25 point buffer overflow machine
- 25 point behemoth riddled with rabbit holes
- 2 x 20 point machines
- 10 point machine

The student can receive all Windows hosts, Linux hosts, or even a mixture of hosts.

My first exam I had 4 hosts of the same kind. My second attempt had a mixture of Windows and Linux hosts

Fortunately for this attempt all things went well with my VPN connection.

**Host#1: BufferOverflow**
For my first attempt I left the Buffer Overflow (BOF) machine for last as I was quite confident in my abilities. The second attempt it was the first thing I did. The reason for this change was to allow for nmap scans / tools like AutoRecon to scan each machine so I would not be sitting around again like last time.

I had completed the BOF system in the first 2 hours. I had a slight hiccup by missing a bad character which had me go back a few times to make sure I had all the required bad characters. I had 25 points under my belt compared to my first attempt where it took 10 hours to get even 10.

**Host #2: 10 point host**
From the BOF I decided to tackle the 10 point host. Not much to say here realistically speaking. It took about 30 minutes. I was now at 35 points about 3 hours into my exam.

**Host #3: 20 point host**
I moved onto the first 20 point host and had low privilege shell after about 30 minutes of meticulously reviewing the output from AutoRecon scans of the host. This put me at 45 points in and I continued to try and privilege escalate in the 1 hour and 30 minutes I had left before I’d take a break and move to the next host. Unfortunately I never ended up getting a root shell to acquire the proof.txt. I did come back to this host and I had an inkling of what was required just couldn’t pull it off.

**Host #4:20 point host**
Moving onto the next 20 point host I too had a low privilege shell after about 30 to 45 minutes. Similarly I reviewed the results from AutoRecon. This host unfortunately had a severe area I was weak in which ultimately lead to me not acquiring a root shell / proof.txt. It was only after starting on this host I realized just how weak I was.

**Sleep Intermission:**
Around 11 hours into the exam I had 55 points. I proceeded to get about 5 to 6 hours of sleep. Compared to my first exam where I did not sleep at all.

**Host #5: 25 point behemoth**
Waking up after a short sleep of 5 to 6 hours I tried to tackle the 25 point host. I started by reviewing the output of AutoRecon. I had a fairly good idea of the way in for this behemoth. I proceeded to find some exploits for what I believed was the way in. I found some manual exploits and some metasploit framework versions of the exploit. Unfortunately, I never tried the metasploit framework version which could have been my way in.

Similar to the first exam I did not get anywhere with the 25 point behemoth.

After spending about 2 hours on the behemoth I used what time left I had in my exam (about 6 hours) to try and privilege escalate on Host #3 and #4.

### Lab & Exam Writeup

Due to not acquiring the necessary 65 points ( and hoping my notes would bring me to 70) or flat out acquiring 70 points I did not bother creating a report again.

I still had my lab write up from before the first attempt. This does not require any changing and is ready for submission should I reach the 65 point mark.

Offensive Security provides the student with a lab and exam write up template. You can use this if you wish, however, I did not. I treated my lab write up in a boot to root format. Similar to how I wrote VulnHub Walkthroughs in the past. The admins ideally want a report that you can present to someone such that they can follow each step you took to perform the penetration test their selves. The report should include step by step screenshots, any code modifications made if required, links to exploits, etc. If you wrote any custom exploits or code, this needed to be in the report as well if used on 1 of the 10 machines you have to write a report on. You can include more than 10 but generally not worth.

Some lab machines had some data for us to ex-filtrate. If one of your target machines you are reporting on has data you ex-filtrated, make sure that data is in the report.

In the end my lab + exercise report was roughly 220 pages.

### Take-Away

Feel free to review my take-away from the first attempt. Again those can be found here:  https://devzspy.github.io/oscp/2019/02/19/oscp-exam-attempt-1.html  towards the bottom

Some of the take-aways below I followed but felt necessary to reiterate for those first tuning in.

1. Continue to manage time wisely. This is crucial for the exam
2. Get some sleep. Everyone works well after a fairly decent rest. At least 4 to 5 hours minimum I feel. To each and everyone’s own though
3. Do not rely heavily on scripts like Linux PrivEsc Checker and Windiws PrivEsc Checker. They will not work on the exam hosts or provide substantial exploits for priv esc.
4. I need to work on my weak areas revolving around Privilege Escalation and finding misconfigurations in systems. (Reinforces #3)
5. If you find a guide that fits what you need to do, tweak it so it fits your needs. Do not immediately dismiss it saying this won’t work. Make sure it does *not* work before moving on.