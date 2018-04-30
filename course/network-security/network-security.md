---
layout: course
course: active
title: Network Security
description: Overview of Cyber Security Topics and Career Paths
permalink: /network-security/
network-security: show
estimated-time: 30
---
{% include estimated-time.html %}

<div class="embed-responsive embed-responsive-16by9">
  <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/c0K-aPhAajM" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
</div><br>

## Overview
Nearly every computing device or software component interacts with a network today. Network Security plays a major role in securing all types of devices. To understand how threats against networks happen we must understand the basics of networking. Internet is made of several hierarchical layers and software and devices in each layer has its own set of vulnerabilities.

## Birds-Eye View of Networking
#### What actually happens when you "google" for something in your web browser?
Classic interview/security question because you can go very deep into details of networking. We will do a condensed answer. We use names (domain names) like www.google.com to browse the internet, but the internet uses numbers (IP addresses) like (108.177.98.106). This is similar to concept of phone numbers vs names in your phone’s contacts app.
#### First Step
So first step is to translate a domain name → IP address using a central service: ‘Domain Name Service’ (DNS). Your DNS settings are usually pushed to your phone/computer when it initially connects to a cell phone/WiFi network so it knows where to ask for these translations. Companies like Google will register one or more domain names (www.google.com, www.gmail.com, etc) with a special registrar so that everyone knows how to reach the IP address for each of these. DNS has a few root servers that store all the correct translations needed to respond to these questions, but for efficiency a hierarchy of saved DNS translations is used to save these answers (a ‘cache’) at every level in the internet. Your browser will check its own DNS cache for www.google.com’s IP address, then the Operating System cache, then your local home/company router, then your internet service provider’s DNS server, and so on. Sometimes none of these will have the answer and your translation request will reach the root DNS server but this is unusual. Usually you or somebody else nearby has asked for www.google.com’s IP address recently.
#### What are the potential security issues of DNS?
What if you typed www.googgle.com? DNS will try to resolve this and if an attacker registered the domain www.googgle.com, DNS will give you an IP address. The Google impersonator can ask for your Google password, send malware, serve ads and make money, etc. from this IP address
Attack known as *typo squatting*.

What if one of the caches (browser, operating system, router, service provider DNS server, etc) that initially saved the translation  www.google.com → 108.177.98.106 was maliciously changed to some other IP  www.google.com → 100.100.99.99. The Attacker can now serve their own content from that IP pretending to be www.google.com. This type of attack is known as *DNS cache poisoning*.

What if someone claimed ownership of www.google.com at the registrar and changed its associated IP address? The attacker can now serve their own content from that IP pretending to be www.google.com. This attack is known as *Registrar Hacking*.

There are many more vulnerabilities as well! …

#### Second Step
Your browser will setup a connect to communicate with www.google.com at IP address 108.177.98.106

Uses an agreed upon communication method called TCP (transmission control protocol) that can send data reliably across the entire internet even if small portions of data are lost on a ‘spotty’ connection
Connection setup goes from your device over Wi-Fi to a router (or directly to a cell phone network) → your internet provider → many → ‘hops’ → of → routing → across → the → internet → … → a Google server at 108.177.98.106

Finalize connection setup and goes all the way back from Google server back to your device

#### Third Step
Open up ‘Developer Tools’ in Chrome while asking Google a question, navigate to the ‘Other Tab’, and you will see these HTTP request and response headers going to from and from your web browser and Google’s server
Google will send back many HTTP responses (HTTP OK 200, etc) with text, images, and instructions to make your browser ask for even more content over HTTP.
These responses travel the return route over the internet → your internet service provider → Wi-Fi/cell phone network → your device
Some of the content will be customized (search results, account settings menus) if you have visited/logged into www.google.com before

www.google.com probably left a ‘cookie’ (a small file) on your computer last time you visited that your web browser will reference when asking Google for content so Google can customize its page for you

#### Security Analysis
What can go wrong in this step?

What if a website/bad program tricks you into giving up your saved cookie for www.google.com?

Someone can impersonate your last/current browser session with www.google.com (read your gmail, use your google wallet, etc)
Attack known as ‘session forgery and cross-site scripting (XSS)’

What if something in the network between you and Google (Wi-Fi router, internet provider router, etc,) that handled your request or Google’s response made changes to the content?

Can change the search results, show that your Google wallet has balance when it doesn’t, etc
Attack known as ‘man in the middle attack (MITM)’

So even in this quick birds-eye networking overview, you’ve seen 5+ attacks based on assumptions made at various network levels
Every level of network has some vulnerabilities. Attackers are good at choosing where to attack by balancing:

How easy (time/money) is it to attack
How anonymous can they remain while attacking it
What power (information/money) they can gain from attacking it

## Lab: Network Scanning
Wi-Fi: it is everywhere and connects everything

By design it has great coverage an allows any device to communicate with it
Very easy to observe information being transmitted over Wi-Fi (attackers can use it to steal information or impersonate someone)

<br>
<div class="embed-responsive embed-responsive-16by9">
  <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/wPwJqtjKS_w" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
</div><br><br>

### Lab Exercise Goal:

Observe Wi-Fi network traffic
Filter and isolate specific traffic going from one device to a specific website
Observe username and password sent in cleartext for login request to a website

### Requirements

- A Wi-Fi hotspot (like your phone)/Wi-Fi router you own
- Wireshark installed on your computer

### Tool: Wireshark

Free open-source software used for observing network traffic

Network troubleshooting and performance
Education and learning
(Attackers) nefarious sniffing of traffic

`Download it here: https://www.wireshark.org/#download`

### Ethical Testing Environment

Use your own local wifi network (your own home wifi router or setup a hotspot on your mobile device in range of your computer)
Only observe traffic from devices you own

### Lab Walkthrough

1. Open Wireshark and start capture

    - Observe how much automatic network traffic is ongoing.
    - Operating System Updates
    - Email check
    - Program updates


2. Use your computer’s browser to visit the test website we have setup at http://security.enablingprogrammableself.com/index.php


3. Filter Wireshark traffic so it only shows traffic going to our test website

    - Use operating system terminal app: Windows `Command Prompt` / Mac `Terminal`
    - Once in the terminal app, type: `ping security.enablingprogrammableself.com`
    ping is a networking utility that tests the reachability of a domain and in turn also gives us the current DNS IP translation for the domain
    - Observe the IP of the destination server in the reply (ie. `75.119.202.178`)


4. Return to Wireshark and enter this as a filter (`ip.dst`)

    - You should now only see traffic that is going to our test website


5. For purposes of this exercise we will ALSO filter on traffic leaving our test device (in this case the same computer you are using for Wireshark)

    - Find your device’s IP by entering `ipconfig` (Windows) or `ifconfig` (Mac/Linux)
    - Note your device’s IPv4 address
    - Return to Wireshark and modify your filter to ALSO filter on `ip.src` (the IP you just looked up in this step)
    - You are now only seeing traffic from your test device reaching our test website


6. Get a `clean slate` to observe traffic

    - Stop the capture and then hit capture again (you can hit `continue without saving`)    
    - Make sure your IP `src/dst` filter is enabled again


7. Go visit http://security.enablingprogrammableself.com/index.php again (hit enter, not reload)

    - Observe the TCP handshake to setup the communication
    - Observe the HTTP GET requests
    - Click on the first HTTP GET request for `/index.php`
    - Right click on this entry and choose to `Follow` the `HTTP Stream`
    - How many HTTP responses did the browser return for the original GET request?


8. Enter an email address (fake one is fine, try ` yourname@fake.email.com`), and a password (try `yourname_fakepassword`) in the browser and hit `submit`


9. Go back to Wireshark and change the filter from the TCP stream back to our original `ip src/dst` combo filter

    - Scroll to the bottom and work your way backwards until you see a `HTTP POST` request from your test device
    - Once again right click and `Follow --> HTTP` stream
    - Can you see the email address and password sent in cleartext as part of the POST request body?


10. Remove your filter and observe the deluge of traffic that filled up Wireshark while you were testing your device/website. Good luck finding your transactions without filters! :)
