---
title: "What Happens When You Type a URL in a Browser and Press Enter?"
date: 2021-01-23 19:56:00 +0000
tags:
  - "Web Applications"
---

There is just so much to unpack if you really get into the details. Others online have already done a great job answering this question with minute details I wouldn't have even thought to include in this post had I not discovered their work (see the explanation of keystrokes being entered on a USB keyboard and the related circuitry vs a capacitive touchscreen) so I'm not going to try to out-detail a 70+ person collaborative effort.

Instead here are some of the things I like to highlight when answering this question along with parts I've had to educate myself on (browser rendering steps, parsing JS and CSS, various trees, and that end of the flow were really interesting to read about as I don't usually have exposure to them).

|  |
| --- |
|  |
| Credit: [@manekinekko](https://twitter.com/kamranahmedse/status/1297131414190776320) |

  

This graphic does a fantastic job detailing the flow of information that occurs when someone enters a URL in a browser and presses enter. For more information click on each of the steps below:

1. [URL is entered](https://en.wikipedia.org/wiki/Address_bar).
2. [DNS lookup occurs](https://www.cloudflare.com/learning/dns/what-is-dns/).
3. [Once IP address is determined a TCP connection is made (usually over port 443 or 80) via the TCP/IP 3-way handshake](https://www.techopedia.com/definition/10339/three-way-handshake).
4. [HTTP request is made for the website](https://www.cloudflare.com/learning/ddos/glossary/hypertext-transfer-protocol-http/).
5. [Web server responds with their HTML website plus any other code used on their site (CSS, JS, anything but Adobe Flash, etc](https://blog.hubspot.com/marketing/web-design-html-css-javascript)).
6. [The browser renders the webpage -- parsing, DOM, CSSOM, and more](https://blog.logrocket.com/how-browser-rendering-works-behind-the-scenes-6782b0e8fb10/).

Some things this graphic doesn't show but I like to discuss are:

- How does the browser/computer know how to get to a DNS server? How does this differ between a computer that's been on the network for a year vs a brand new computer on the network?
- Local DHCP, DNS, HOSTS file. How does the computer have an identity on the local network let alone the Internet?
- Network Address Translation's (NAT) role in sending and receiving traffic from the web server.
- Address Resolution Protocol's (ARP) role in forming frames and packets to get out of the local network.
- Web proxies, stateful and stateless firewalls, TLS/SSL, and public-key cryptography.
- Browser/session cookies, geolocation detections, and compliance requirements such as GDPR.

This of course doesn't even begin to get into the various security vulnerabilities along the way and how to best mitigate them.

It really is a feat of human engineering that all this works as well as it does as fast as it does and we carry it around in our pockets often without a second thought!

If you'd like me to expand on any of the steps above feel free to reach out or comment below and let me know!

#### References & Extras

- https://github.com/alex/what-happens-when#
- https://twitter.com/kamranahmedse/status/1297131414190776320