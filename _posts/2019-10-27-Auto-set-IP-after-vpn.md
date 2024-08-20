---
published: true
layout: post
title: "Get IP address for VPN automatically"
tags: [vpn, htb, oscp]
---

# Introduction

I wanted to create something that would automatically grab my VPN adapter's assigned IP address. I started looking into ways to do it and came up with a command that would give me the IP itself. However, it would not create an environment variable for me or do everything fully. As such I recalled a peer that goes by Tib3rius that had created something similar to what I was working for. I can't take full credit for this!

These scripts are used to automatically set an environment variable `IP` after connecting to a VPN. This setup is specifically for Hack The Box where your IP address may change periodically whether on the free or VIP servers.

These scripts may also be used for the OSCP Lab environment or any other environment. You will need to make some changes in order to make it work. For the OSCP Labs the necessary changes will be listed for your convenience.

## source.sh File

This will be a pretty basic file but it will be called with our openvpn command.

```bash 
#!/bin/bash
source /root/update-ip.sh
```

## update-ip.sh File

Here is the necessary code to automatically grab the VPN adapter's assigned IP address. It will then create an environment variable called `IP` which will contain your adapters IP address.

```bash
#!/bin/bash

if ifconfig tun0 &> /dev/null; then
	IP=`ifconfig tun0 | grep 'inet ' | awk '{print $2}'`;
else
	IP=`ifconfig eth0 | grep 'inet ' | awk '{print $2}'`;
fi

export IP;
```

In order to make this work for the OSCP Labs, simply copy and paste the below for your convenience:

```bash
#!/bin/bash

if ifconfig tun0 &> /dev/null; then
	IP=`ifconfig tap0 | grep 'inet ' | awk '{print $2}'`;
else
	IP=`ifconfig eth0 | grep 'inet ' | awk '{print $2}'`;
fi

export IP;
```
Please note the only change was instead of it being `tun0` it is now `tap0`.

## openvpn alias (Optional)

I typically like to use screen / tmux for holding open my VPN connection. That way if I accidentally close out of the terminal session, my connection will stay alive. 

Once I've created the screen/tmux session, I use the below alias which should be placed in your `.bashrc`

`alias vpn='openvpn --script-security 2 --up "/root/source.sh" --config /insert/path/to/ovpn/file'`

Make sure you update the `--config` parameter path to wherever your ovpn file may be located.

## Example of Usage

You would add the below alias into your `.bashrc`

`alias msf-multi-handler='msfconsole -x "use exploit/multi/handler;setg LHOST $IP;setg LPORT 4444;setg EXITFUNC thread;set PAYLOAD generic/shell_reverse_tcp;clear;show options"'`

This would launch the msfconsole for you, select the multihandler "exploit", set your lhost and lport. Make sure your payload's exit function is set to thread and use a generic reverse shell.