---
published: true
layout: post
title: "OSCP Exam Attempt #3"
categories: [oscp]
tags: [oscp, Pentesting, Exam]
---

![img](https://cdn-images-1.medium.com/max/800/0*cFufqYlUCHsfS1pI.png)

#### Disclaimer

I *PASSED* my third OSCP exam attempt. This is more just a post detailing my new experiences the third time around.

For those of you first tuning in, should you wish to review my first failed attempt you can do so here:  https://devzspy.github.io/oscp/2019/02/19/oscp-exam-attempt-1.html or review my second failed attempt here: https://devzspy.github.io/oscp/2019/04/09/oscp-exam-attempt-2.html 

### Proof of Success

![img](https://cdn-images-1.medium.com/max/800/1*9ptmaobhUrSa7NsNBAhjEg.png)

### **Introduction**

A month after failing my second exam attempt with 55 points, I was determined to pass for my third attempt more than ever. I had planned out my method for attacking the exam again.

In the end, I managed to acquire 80 points for my third attempt, submit my report and receive a passing grade/report.

In my second post ( https://devzspy.github.io/oscp/2019/04/09/oscp-exam-attempt-2.html ) I had mentioned I doubt I would receive the same 5 exam machines again. I still hold that doubt but I had 3 of the same hosts as my first exam attempt. So I guess it could happen….

### **Practicing More via Virtual Hacking Labs (VHL)**

After failing my second attempt with 55 points (again), I needed more practice. I had already done most if not all of the OSCP like hosts on HackTheBox.

![img](https://cdn-images-1.medium.com/max/800/0*lax4Z4nsiWcz1qVF.png)

I turned to VHL( https://www.virtualhackinglabs.com/ ) which provides an environment of 40 hosts. The VHL network is fairly similar to the OSCP environment in some aspects but very different in others.

![img](https://cdn-images-1.medium.com/max/800/0*htVSuRYtP9uK7n0C.jpg)

After finding out about VHL from someone in the PWK/OSCP Prep Discord server I am an admin on, I decided to sign up for a one month membership for about $130 USD.

VHL also gives out a certificate of completion as long as you fulfill their requirements. One thing to note; there isn’t an exam to obtain the certificate. One simply creates a report documenting the steps required to obtain root on 20 Beginner/Advanced machines while showing the “key.txt” output. This key.txt is the equivalent of OSCP proof.txt.

Additionally, VHL has a certificate of completion for their Advanced+ hosts. This certificate requires a total of 12 hosts to be compromised. 10 of which you can use any publicly known exploit or metasploit module for low privilege access. The other 2 require manual exploitation such as SQL Injections without the usage of SQLMap as an example.

I am in the process of writing both reports for the VHL Certificate of Completion and the VHL+ Certificate of Completion.

About 80% of the VHL Linux hosts are vulnerable to some DirtyCow variant. That being said, if you truly wish to learn and better yourself, stay away from using DirtyCow on their hosts and find the appropriate privilege escalation path.

You can join the VHL Discord Server via the following invite: https://discord.gg/bQfGnVQ

I rooted 37 of the 41 hosts over on VHL’s network.

### **Acquiring Additional Useful Tools**

I discovered some newer useful tools from my first exam attempt to my third exam attempt. Some of these tools I guess were always in my face but I never tried to use them or understand them.

Some of these tools/programs might seem obvious to some of you and others not so much. Without further ado:

- Powerless for Windows — https://github.com/M4ximuss/Powerless

> *Batch script that is fairly similar to that of Linux’s LinEnum.sh script. It is suggested that the user has accesschk.exe in the same directory.*

- PowerUp for Windows — https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc

> *This is a PowerShell based version of LinEnum which has additional useful features compare to that of Powerless.*

- Local Privilege Escalation Workshop — https://github.com/sagishahar/lpeworkshop

> *This workshop has scripts that can make a Windows and Linux system vulnerable to a number of different local privilege escalation techniques. There is also exercises, videos, and documents to follow along.*

- Get the F*** Out Bins — https://gtfobins.github.io/

> *GTFOBins is a curated list of Unix binaries that can be exploited by an attacker to bypass local security restrictions.*

- Wfuzz — https://github.com/xmendez/wfuzz

> *Fairly useful program for fuzzing websites for Local File Inclusions and much more. I preferred this over goWAPT which I posted in my second write up.*

### **Game Day….Again (For the last time)**

The exam was scheduled for Saturday, May 11th, 2019 at 6pm local time.

The OSCP Exam consists of 5 machines. You, the student, are provided with objectives and point values for each machine.

- 25 point buffer overflow machine
- 25 point behemoth riddled with rabbit holes
- 2 x 20 point machines
- 10 point machine

The student can receive all Windows hosts, Linux hosts, or even a mixture of hosts.

My first exam I had 4 hosts of the same kind. My second attempt had a mixture of Windows and Linux hosts. My third attempt also had a mixture of Windows and Linux hosts.

Fortunately for this attempt I did not have any VPN problems or issues with any of my exam hosts.

**Host#1: BufferOverflow**
I had completed the Buffer Overflow system in about 53 minutes according to my Toggl dashboard. Dramatic improvement from my second attempt which took 2 hours. That was partially due to missing a bad character.

There was a slight gotcha this time around that I also had on my first exam attempt. Some of that time went to reviewing my notes from said attempt to make my payload work.

**Host #2: 10 point** 
It turns out this was the same 10 point system I had on my first exam attempt. I did not root it on my first attempt as I finally got around to this at 18 hours in.

This took me about 30 minutes to get as I was reviewing my notes I had saved from the first attempt. I also reviewed my suggested potential exploits from researching the services the system was running.

**Host #3: 25 point behemoth**
Similarly to my 10 point host, this too was the same system as my first exam attempt EXCEPT for one minor difference. The OffSec Exam administrators changed something. Obviously, I can’t disclose what this minor change was but it played a crucial role in rooting this server.

According to my Toggl dashboard I spent about 2 hours and 21 minutes. A large portion of that time was reviewing my notes and suggested exploit steps from my first exam attempt based on things I researched. The privilege escalation wasn’t as bad and I’d rate it as probably easier than any of the 20 point hosts I had between my first and second exam attempt. The initial shell was probably the most difficult.

**Sleep Intermission:**
So before I went to bed around 1am local time I had about 60 points. I finally made it past that dreaded 55 point hurdle after 7 hours. A large portion of this was due to receiving the same hosts so I will consider myself just lucky at this point. I got about 5 hours of sleep according to my Fitbit but the stats showed I was extremely restless. Can you blame me? I finally made it past 55 points and all I needed effectively was 10 more points so I can write my exam report.

**Host #4:20 point host**
By now you can probably guess it…YEP! This too was similar to my first attempt. According to my Toggl dashboard I spent 30 minutes on this host.

This host was one I had rooted on my first exam attempt and the OffSec admins did not throw any curve balls on this one. Just followed the same steps and procedures as my first attempt.

**Host #5: 20 point host**
I spent about 3 hours and 45 minutes on this host but didn’t really make any progress. Nothing jumped out at me immediately and I probably went down a few rabbit holes for too long.

I did not get shell on this host and obviously did not get root as a result.

So with about 4 hours left on my exam I decided I would stop trying to get Host #5. I really wanted to get 100 points but I felt I could and should use my time more wisely.

**The Remaining 4 Hours:**
I decided to switch my focus from the final host I wasn’t making any progress on. Utilizing this time, I reviewed my notes and screenshots making sure I had everything required for the exam report. OffSec gives you a set of objectives like you need X screenshots as an example for the report. I made sure each host met the required objectives for the exam report.

If I missed anything I could just go back and repeat the steps while I still had VPN access. I also had the video recordings of every host through OBS Studios in case my lab time expired and I needed something.

### **Lab & Exam Writeup**

I had already created my lab write up a month before my first exam attempt. This was done about 3 months ago so I did not need to worry about it.

If I wanted to look on the bright side of things I effectively had 85 points as I submitted my lab report. You never know if OffSec removes points due to spelling, grammatical, or lexical errors.

For the exam write up I spent about 8 hours in total. I had received a template from someone I’ve became fairly friendly with over Discord as I completed hosts in the VHL network. He was kind enough to give me his skeleton template he used to pass the OSCP. For the most part his template was pretty close to the one OffSec provides with some minor changes. I took a bit further and changed it to fit my needs as well.

I spent those 8 hours immediately after my exam ended writing the report. I did not want to waste any time and I wanted it completed before I went to bed. So around 2am Monday morning I had finished. I went into work for a half day and left around 1pm.

Upon getting home I proceeded to review my report 2 or 3 times for any spelling, grammatical, or lexical mistakes. I swapped between “I”, “we”, and referring to myself in the third person for my report. Finally, I just settled with referring to myself in the third person.

- Exam Report: 47 pages
- Lab Report: 203 pages

Just a little over 50 hours of submitting my reports I received the email from OffSec saying I passed.

### **Take-Away**

These are continuations from my first and second failed attempts. All of these should hopefully help a new or struggling student finally pass their exam and join the ranks of OSCP holders.

1. If you fail an exam, review your notes and make suggestions for the next attempt you receive the same host again. Maybe you’ll actually get the initial shell or root this time
2. GET SLEEP. I can’t stress this enough. Even the OffSec admins / Proctors recommend getting sleep (Yes the proctors are nice and can chat here or there about every day things)
3. **Reiterating a point from my second attempt:** If you find a guide that fits what you need to do, tweak it so it fits your needs. Do not immediately dismiss it saying this won’t work. Make sure it does *not* work before moving on.
4. If you failed your exam try to find other ways to improve your weaknesses. Sign up for VHL, HTB, or download VMs off VulnHub.

------

I’ve had co-workers that know people that failed the exam 7 times even after rooting every host in the OSCP labs. There are people that pass the exam on their first try and only root 8 machines.

Do not use the amount of machines as an indicator of how well you will do on the exam. Do not be discouraged if you don’t get every host in the labs either as it’s not really necessary.

All I can say is keep trying until you succeed. I kept telling myself I would take the exam as many times as it took until I’ve seen every exam host and finally passed.

### **Shout Outs**

- PWK / OSCP Prep Discord Server — https://discord.gg/strQxxe
- Virtual Hacking Labs Discord Server — https://discord.gg/bQfGnVQ
- Discord buddies in no particular order: jerryblanks#5489, Shachath#4151, b0ats#9656, waar#2317, whoisflynn#1893, evader#9052, eminent#8701, Tib3rius#9220 and much more (seriously list goes on)