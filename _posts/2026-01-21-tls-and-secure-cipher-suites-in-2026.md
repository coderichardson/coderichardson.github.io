---
title: "TLS and Secure Cipher Suites in 2026"
date: 2026-01-21 03:24:00 +0000
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEizMmKp1e7zAk8evZdigLutNxRb6O5fWP5rAbWeK5mhLpAuk5zbK3FNBiOWHfA9xdIcgTLXBXOrrN2iPWj6uj4wXI8-7xL-irzC9IdmzucIdMFip5L-ILyLK3bUJjy8Ucb8fvI8jVzkXxLxXg4Q1T16Eo1ymn2gKIrdvzWcZtVogAx8leUontz7XMu42Or6/w640-h426/TLS%20Cipher%20Suites.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEizMmKp1e7zAk8evZdigLutNxRb6O5fWP5rAbWeK5mhLpAuk5zbK3FNBiOWHfA9xdIcgTLXBXOrrN2iPWj6uj4wXI8-7xL-irzC9IdmzucIdMFip5L-ILyLK3bUJjy8Ucb8fvI8jVzkXxLxXg4Q1T16Eo1ymn2gKIrdvzWcZtVogAx8leUontz7XMu42Or6/s1536/TLS%20Cipher%20Suites.png)

  

### TLS

It's been 4.5 years since I last wrote about the [state of TLS and secure cipher suites](https://blog.codyrichardson.io/2021/07/secure-cipher-suites-and-tls-in-2021.html). A lot has changed in that time including some updates around TLS and cipher suites, so I wanted to provide an update while it has been on my mind.

First and foremost -- TLS 1.3 is gaining ground. Qualys' SSL Labs shows that even as of June 2025, [75% of sites surveyed supported TLS 1.3](https://www.ssllabs.com/ssl-pulse/). This is great news, and I look forward to continued adoption of TLS 1.3 and it eventually becoming the norm. I will link again to two fantastic Cloudflare blog posts that explain the details and benefits of TLS 1.3, but I am looking forward to the following changes in particular:

1. **It's faster**. I don't just care about security, I also care about performance and stability. TLS 1.3 reduces the number of required round-trip communications from two to one thereby reducing the total amount of time needed for a connection. Just thinking about the elimination of all that wasted network traffic is exciting.
2. **It's more secure.** Through a number of means, TLS 1.3 is simply more secure. Many vulnerabilities in TLS 1.2 and before cannot even exist in TLS 1.3 as the associated ciphers are not permitted.
3. **It's a lot easier to choose secure cipher suites.** There are way too many options in TLS 1.2. Take ECDHE-ECDSA-AES-GCM-SHA256 as an example. Each element in that TLS 1.2 cipher suite represents a choice that an engineer or administrator has to be informed about and continue to monitor for improvements or needed changes. Not so with TLS 1.3 cipher suites. More on that in a bit.

As promised, those Cloudflare articles:

- [A Detailed Look at RFC 8446 (a.k.a. TLS 1.3)](https://blog.cloudflare.com/rfc-8446-aka-tls-1-3/)
- [Why Use TLS 1.3?](https://www.cloudflare.com/learning/ssl/why-use-tls-1.3/)

Windows Server 2022 [supports and has enabled by default TLS 1.3](https://learn.microsoft.com/en-us/windows/win32/secauthn/protocols-in-tls-ssl--schannel-ssp-). The same is true for Windows 11 (21H2). This is as both a client and server.

As for Linux, I'll focus on Ubuntu for the moment which received TLS 1.3 support in Ubuntu 18.04 via a back-ported update. With Linux, TLS 1.3 support varies depending on the system, version of openssl running, and other variables. But generally speaking, TLS 1.3 is now widely supported on many Linux platforms.

This means that not today, but at some point in the not-too-distant future, TLS 1.3 will be the standard and having anything else will be odd but still technically supported until we can do away with TLS 1.2 entirely.

With any luck, in another 4 to 5 years I'll be able to post another update glad to see that everything is running TLS 1.3. Fingers crossed.

### Cipher Suites (TLS 1.2)

As mentioned previously, there is a laundry list of potential options when it comes to TLS 1.2. Each component of a given cipher suite in TLS 1.2 can have so many options that the total number of possible combinations is mind-numbing.

So rather than point out all of the potentially bad cipher suite options, I'm going to lay out what is considered secure as of today (January 2026).

TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384

TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256

TLS\_ECDHE\_RSA\_WITH\_AES\_256\_GCM\_SHA384

TLS\_ECDHE\_RSA\_WITH\_AES\_128\_GCM\_SHA256  
TLS\_DHE\_RSA\_WITH\_AES\_256\_GCM\_SHA384

TLS\_DHE\_RSA\_WITH\_AES\_128\_GCM\_SHA256

That's it. That really is it outside of ciphers such as CHACHA20 and POLY1305 (which *still* haven't been FIPS 140-3 certified and approved by NIST). And importantly, that is it in the order of each cipher suite and in the overall over of suites top to bottom.

For example, you'll find RSA in a number of these cipher suites, but if you chose to use RSA as a key exchange (the first variable) you've suddenly made a poor choice by modern standards.

Now to break down why these are good to help you understand the selection process:

- **ECDHE** - Elliptic Curve Diffie-Hellman Ephemeral provides perfect forward secrecy, and is faster and more efficient than DHE (Ephemeral Diffie-Hellman). For these reasons it is the gold standard for key exchange protocols in TLS 1.2. DHE is still acceptable and secure, but should be utilized as a secondary option hence the algorithms' respective locations on the list.
- **ECDSA** - Elliptic Curve Digital Signature Algorithm is a public key cryptography algorithm which uses smaller keys than competing algorithms (such as RSA) with equivalent security. This also generally means faster loading of webpages and saving CPU cycles.
- **AES** - All of the other options for bulk encryption have been found to be insecure for one reason or another. No RC4, 3DES, DES, etc. A longer key length is more secure but both 128 and 256 AES are secure as of today.
- **GCM** - Galois/Counter mode is a specific mode of operation for AES. [There are many](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation). Similar to AES itself, all of the alternatives to GCM have been found to be insecure for one reason or another.
- **SHA256/384** - Historically, this represents both the MAC for application data and the hashing process during the TLS handshake. Interestingly, when GCM is in use, its presence only indicates the hashing algorithm used during the TLS handshake.

### Cipher Suites (TLS 1.3)

Below is a common, secure list of TLS 1.3 cipher suites.

TLS\_AES\_128\_GCM\_SHA256

TLS\_AES\_256\_GCM\_SHA384

TLS\_CHACHA20\_POLY1305\_SHA256

Again, that's it. And this contrast highlights part of why I'm so excited about TLS 1.3 -- it is so much simpler. At least in terms of choosing cipher suites and how they are comprised.

The cipher suite only tells you how application data is protected. Key exchange, authentication method, MACs, and several other elements have been essentially hard-coded into TLS 1.3 and they have hard-coded the secure options. Cipher suites can now focus entirely on how data is protected.

That being said, one downside to all of this is that TLS 1.3 has now abstracted away operations that are still occurring. It's still important to know what is happening in TLS 1.3 even if it is no longer spelled out in the cipher suites. It will be interesting to see how this is handled moving forward and as TLS 1.3 becomes the standard.