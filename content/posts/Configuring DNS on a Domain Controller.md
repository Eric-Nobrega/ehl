---
title: "Configuring DNS on a Domain Controller"
date: 2023-11-15
# weight: 1
# aliases: ["/first"]
tags: ["Networking", "DNS"]
author: "Eric"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---

DNS (Domain Name System) is a system that translates human-readable domain names (www.google.co.uk) into IP addresses (192.168.1.1) that computers use to identify each other on a network. DNS is crucial as it makes it so that people do not need to memorize complex IP address, and instead, can remember a simple domain name.

In my current home lab environemnt, I have 2 virtual machines. Virtual machine 1, acts as a domain controller (EHL-DC01). Virtual machine 2, acts as a remote desktop server (EHL-RDS01). I'll be walking through how I have configured DNS in this simple environment, cover the benefits of why I have done certain things, etc.

![Test](https://raw.githubusercontent.com/Eric-Nobrega/ehl/main/content/posts/images/dcipconfig.png)
