---
title: "Studying Cybersecurity - How to Learn New Concepts"
date: 2020-12-05 19:09:00 +0000
tags:
  - "Career"
  - "Cybersecurity"
---

Learning cybersecurity or any "specialty" within IT can be challenging. Whether you're a Sysadmin, Security Analyst, Network Engineer, or Database Administrator, there's a lot of learning involved. So how do you get started? And what can help you along? There are two concepts that I often find myself coming back to: Black Boxes and Elephants.

## Black Boxes - Focusing on What's Important

When I'm learning something I frequently ask why or how. I usually *have* to ask (and find out) or I have trouble focusing on the actual subject I'm trying to learn. As you can imagine, this can be both a good and bad thing. Go too far down the rabbit hole? You've lost your way and have become distracted. Be inquisitive and learn some of the details behind new concepts? Now you have a deeper understanding of a topic. This is where Black Boxes come in. Try to recognize when you've strayed too far from the original path, mark it for later reading, and let that area function without you understanding what's happening. At least until you've learned what you set out to learn originally.

**The good side**: Say you're brushing up on your networking knowledge and are learning about VLANs. You can either accept that broadcast messages do not reach nodes on another VLAN despite being connected to the same switch...or you can find out why. This is a great opportunity to learn a bit about [Ethernet frames and 802.1Q](https://en.wikipedia.org/wiki/IEEE_802.1Q), Access vs Trunk ports, etc.

**The bad side**: Say you're learning some of the finer details of TLS/SSL. Public Key Infrastructure, Certificate Authorities, web browser certificate stores, and the asymmetric vs symmetric encryption steps are all crucial. I've personally placed a Black Box on the mathematical process of how a key can be used to encrypt something but not decrypt it ([in the case of asymmetric encryption](https://en.wikipedia.org/wiki/Public-key_cryptography)). There is some very complicated math involved there and I'm willing to trust that the process just works. But everything "before" that? Fair game. Insecurities in SSL, improvements made in [TLS 1.3](https://en.wikipedia.org/wiki/Transport_Layer_Security#TLS_1.3), why SHA-256 hashes should be used in TLS 1.2 and not MD5, and the pros/cons of using ECC vs RSA...all good things to explore because they're actually relevant to what you were originally trying to learn. At least if you ever have to create a certificate and secure traffic to a website.

Knowing where and when to place a Black Box can be extremely helpful and keep you focused. Understand that there is a process that takes place, you're given some output from it that you need, and can carry on with what you're trying to do.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjYUU33m2KtiF1SMRvcjyWjqWaYve7pXgK3IRV7wZ5GFv44Tp-1CJN1o5Ib-hXuA7gdN-WxRUY00kYMFxInJZOgDunPcTCve8815qwdL_lPJuukXh_KaD9azO6QksUIp8pYOgVfAGkI671F/w400-h170/blackbox-3.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjYUU33m2KtiF1SMRvcjyWjqWaYve7pXgK3IRV7wZ5GFv44Tp-1CJN1o5Ib-hXuA7gdN-WxRUY00kYMFxInJZOgDunPcTCve8815qwdL_lPJuukXh_KaD9azO6QksUIp8pYOgVfAGkI671F/s510/blackbox-3.jpg)

## Elephants - How to Learn When There's Too Much To Learn

This one is an extremely popular saying, but I want to include it because it really does help me in the learning process: "How do you eat an elephant? One bite at a time."

It has since been revised, but when I took the CCNP it was comprised of three tests -- Routing, Switching, and Troubleshooting. When combined, this was an elephant of information. Thankfully Cisco broke the subjects down into their own tests which helped, but even within those tests there was a TON of information to learn. Dividing the material into categories, learning a topic at a time, and making regular progress is the only way to tackle something like that.

This is true for other certifications (CISSP comes to mind), but it's also important when implementing a new product, managing just about any project, learning to program, or more relevant to the title of this article, learning cybersecurity. Like with any subset in IT, there are subsets of subsets -- you can go down the paths of encryption research, compliance, security operations, reverse engineering of malware, secure coding, penetration testing, incident response, and a plethora of other subjects. These all have their own elephants and often require knowing a little about each of the other areas too.

Methodical progress is key. The rate will vary from person to person, but eat irregularly and your food goes bad. Eat too much at once and you get sick. Take it a bite at a time.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgms6AG9zPArrWsiZy-O3bZOl_6sZ8d2jxw8yYWqg-A9zIT3pLweQq8RMf5qAKXmT6GuXHlcndZIfitHbs_gTE-eg38JJSWPtOwSLY2S1_HIgz_8lpNSzfgAR2P5cULLthSBHV1imRXa5I6/w400-h341/00e6ca16c81034b31da19e6113ef456b.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgms6AG9zPArrWsiZy-O3bZOl_6sZ8d2jxw8yYWqg-A9zIT3pLweQq8RMf5qAKXmT6GuXHlcndZIfitHbs_gTE-eg38JJSWPtOwSLY2S1_HIgz_8lpNSzfgAR2P5cULLthSBHV1imRXa5I6/s337/00e6ca16c81034b31da19e6113ef456b.jpg)

## Summary

These concepts go hand-in-hand and have become increasingly useful to me over time. They relieve the feeling of being overwhelmed and help me stay focused on what's important. If you have any advice for what you do when learning something new leave a comment below or feel free to reach out on Twitter!