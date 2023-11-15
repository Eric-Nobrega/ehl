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

### What is DNS?

DNS (Domain Name System) is a system that translates human-readable domain names (www.google.co.uk) into IP addresses (192.168.1.1) that computers use to identify each other on a network. DNS is crucial as it makes it so that people do not need to memorize complex IP address, and instead, can remember a simple domain name.

---

### Current Home Lab Environment

In my current home lab environemnt, I have 2 virtual machines. Virtual machine 1, acts as a domain controller (EHL-DC01). Virtual machine 2, acts as a remote desktop server (EHL-RDS01). I'll be walking through how I have configured DNS in this simple environment, cover the benefits of why I have done certain things, etc.

![Test](https://raw.githubusercontent.com/Eric-Nobrega/ehl/main/content/posts/images/dcipconfig.png)

*The Domain Controller's IP is set statically to 192.168.0.151*

The first step in configuring DNS in this environment is to set the primary DNS server of the domain controller to itself. 

![Test](https://raw.githubusercontent.com/Eric-Nobrega/ehl/main/content/posts/images/dcdnssnapshot.png)

This is common practice as it ensures that the domain controller can locate itself for necessary services. 

### If the preferred DNS is set to itself, with no secondary DNS setup, how can the domain controller resolve domain names?

The answer to this, is **Forwarders**. 

Forwarders are DNS servers that a DNS server uses to forward DNS queries that it cannot resolve locally. 

When a DNS server receives a DNS query from a client, it will first check its own cache and local records. If it does not have the information needed to resolve the query, it will do the following:

1 - Perform a recursive query, this is basically where it will start from the root DNS servers, and follow the chain of referrals until it obtains the necessary information. This is the traditional way that DNS servers will resolve queries.

2 - DNS servers can forward the query to another DNS server that may have a better chance of resolving it. This other DNS server is known as a "forwarder".

Forwarders can help to enhance DNS resolution efficiency, especially for external queries, since they have larger caches and optimized routes for resolving common domain names, which results in a reduced time to get a response. 

In a corporate environment, it's usually preferred to manually configure the DNS as it allows for greater control and customization of DNS settings. 

![Test](https://raw.githubusercontent.com/Eric-Nobrega/ehl/main/content/posts/images/dcforwaders.png)

We can now set the primary DNS to the domain controller's IP.

![Test](https://raw.githubusercontent.com/Eric-Nobrega/ehl/main/content/posts/images/rdsdns.png)