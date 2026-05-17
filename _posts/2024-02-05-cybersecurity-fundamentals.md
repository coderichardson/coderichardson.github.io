---
title: "Cybersecurity Fundamentals"
date: 2024-02-05 01:52:00 +0000
tags:
  - "Career"
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhkvRc4wEgyTFLAVQVUF2sGTRPCeNhfsdZYaMpdSmMF1Q__YqmCFWhhSDDfUoGTaLjGp7XjNHtMZI_Ub3xAvjLqLQUDndzggZvBHqqNQOz3P-ucs_UGtVIdVT5FS05DKfdU4PHU-YDKr99lga_rpNdC0YPam1L1PwcloWHXm5cGLzoYFOu29P-BeZZea2zt/w640-h360/cyber-criminal-in-front-of-computer-screens.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhkvRc4wEgyTFLAVQVUF2sGTRPCeNhfsdZYaMpdSmMF1Q__YqmCFWhhSDDfUoGTaLjGp7XjNHtMZI_Ub3xAvjLqLQUDndzggZvBHqqNQOz3P-ucs_UGtVIdVT5FS05DKfdU4PHU-YDKr99lga_rpNdC0YPam1L1PwcloWHXm5cGLzoYFOu29P-BeZZea2zt/s2309/cyber-criminal-in-front-of-computer-screens.jpg)

While some hacks truly are [sophisticated, nation-state attacks](https://thehackernews.com/2023/12/most-sophisticated-iphone-hack-ever.html#:~:text=The%20exploitation%20activity%20involved%20the,goal%20of%20gathering%20sensitive%20information.), many more are the result of simpler exploits or just social engineering. After the details of such a compromise are released, people comment about how organizations should be doing at least the "basics" or "fundamentals." So what are the fundamentals? And at what point do you cross over into intermediate or expert practices?

I have my opinion, but let me first share a couple official lists:

- [NIST - Cybersecurity Basics](https://www.nist.gov/itl/smallbusinesscyber/cybersecurity-basics)
- [CISA - Cyber Essentials](https://www.cisa.gov/resources-tools/resources/cyber-essentials)

These are great lists but allow me to expand.

## Multi-factor Authentication

First up is multi-factor authentication (MFA). Even in 2024, lack of MFA has resulted in account or organization compromise. [Take the recent SEC X / Twitter hack](https://www.reuters.com/technology/cybersecurity/us-secs-x-account-hacked-with-sim-swapping-agency-says-2024-01-22/) -- the US Securities and Exchange Commission had their X account taken over and was used to post false information. While "SIM swapping" also played a role in the hack, had MFA been enabled, the threat actor may have been stopped in their tracks.

Whether it's Google Authenticator, Microsoft Authenticator, Authy, Duo, or countless others -- install an MFA app on your smartphone and use it for every account you can. Better yet, use a [YubiKey](https://www.yubico.com/) or other physical token.

## Strong (and Unique!) Passwords

I've previously written about [how to make a strong password](https://blog.codyrichardson.io/2019/11/account-security-psa.html). One word I failed to mention then and will include now is **unique**. If there is only ever one change you can make to improve your security -- just make every password unique.

If you have one strong password and use it everywhere, odds are one of those sites are going to be compromised and they're not going to be using the best hashing or storage mechanisms they could be. Ultimately this leads to your unique password being cracked more easily or even worse, in plaintext, out on the Internet despite your best efforts to make a strong password.

Now on to making your password strong -- everything I said in my original post still holds true. You want to make pass*phrases*, not passwords. Or better yet, let a password manager do the work for you. I am a huge fan of [1Password](https://1password.com/) (no I'm not being sponsored or paid by them to say that) but there are several good options out there.

Ultimately with a combination of unique and strong passwords, even if your credentials are compromised, the damage is isolated to that one account.

## Keep Your Systems Updated

Keeping systems up-to-date with the latest patches is undoubtedly important. It's *especially* important if your systems are Internet facing. We're at an age in the Internet where the entire IPv4 space can be scanned in a matter if minutes. Once a vulnerable version of software has an exploit released publicly, hackers can and do perform such Internet-wide scans looking for this vulnerable software to exploit.

Take this [recent emergency directive](https://www.cisa.gov/news-events/directives/supplemental-direction-v1-ed-24-01-mitigate-ivanti-connect-secure-and-ivanti-policy-secure) from CISA regarding a vulnerability in some Ivanti software. In this case, the vulnerability is recognized as being so dangerous (and the ease of quickly detecting it on the Internet) that CISA is requiring US government agencies physically disconnect Ivanti appliances from the network. Similar vulnerabilities are found in [many Internet facing resources](https://www.fortiguard.com/psirt/FG-IR-23-097), often VPN appliances, which highlights the need for regularly monitoring for and installing updates when available.

The next level of importance is for those systems that aren't exposed to the Internet, but are active on your network. These are also important to keep up-to-date in the event that your network is compromised, any attacker would have fewer options for lateral movement or further exploitation of your systems.

## Change Defaults

In a similar fashion to keeping your systems up-to-date, changing default credentials is incredibly important on anything exposed to the Internet, and important on systems throughout your network in general.

Default credentials and configurations are documented by the manufacturer and known by attackers. Leaving a system exposed to the Internet with a username and password of "admin" is a guaranteed way to have your network breached.

## Don't Daily-Drive Administrator

Regardless of environment, you never want your primary account to be an administrator account. Always use a regular, unprivileged account for day-to-day activities, and escalate to an administrator account as needed.

Operating in this fashion has multiple benefits, the greatest of which is that if malware is executed on your system it has restricted access in what is can do and reach on your network.

## Verify Contacts

As mentioned earlier, something that is often the culprit of even high-profile hacks is social engineering. The best way to do this is to verify the identity of who you are dealing with. This is especially true for those that email or call you. Email accounts are frequently compromised and used to impersonate the true owner, and phone numbers are spoofed on caller ID. Not only that, but with answers to basic information about a person, customer support representatives can authorize you as the owner of an account. Just look at some of the recent [SIM swapping attacks carried out](https://www.bleepingcomputer.com/tag/sim-swap/) (including the SEC account hack mentioned earlier) -- they're popular for a reason..

While there are several technical controls to help verify the authenticity of someone emailing you, some of which [I've detailed before](https://blog.codyrichardson.io/2023/02/spf-dkim-and-dmarc-explained.html), there is nothing like picking up the phone and calling a known-good number. This can be true even with senders you frequently converse with. You never know when someone's email account will be compromised.

It's a bit more difficult when you are a company needing to authenticate those that call into your business. Most companies are bad at this, some are abysmal, but just a handful I've come across are pretty good. To be clear, I'm not saying I have the answer that everyone should follow -- far from it. I empathize with the balance between security and ease of customer service for most businesses. Sure, you could make customer verification accurate 99.9999% of the time but introduce a ton of friction on the road to delivering good customer service.

The best balance I have found is a consumer account that has MFA enabled by default, and then a PIN is provided to the customer once they are logged into that account. When the customer calls into the customer support line, they need that PIN.