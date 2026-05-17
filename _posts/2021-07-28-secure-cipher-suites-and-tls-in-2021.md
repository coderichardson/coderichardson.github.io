---
title: "Secure Cipher Suites and TLS"
date: 2021-07-28 01:44:00 +0000
tags:
  - "Ciphers"
  - "TLS/SSL"
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj3sQvbtlAOvDZWK8Pgzjr3JJejCIEP5lw-GDftLnkZzkwPLbCJYkoW1f3VtQ108BMPjT15T7Tw1OuF1VJTMzJ9zb4YNmnljHKBoKDvSmMWZDjw_0w2RNIHcH9E4TGvg_upg43MXLcacFBQ/s16000/tls-cipher-suite.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj3sQvbtlAOvDZWK8Pgzjr3JJejCIEP5lw-GDftLnkZzkwPLbCJYkoW1f3VtQ108BMPjT15T7Tw1OuF1VJTMzJ9zb4YNmnljHKBoKDvSmMWZDjw_0w2RNIHcH9E4TGvg_upg43MXLcacFBQ/s582/tls-cipher-suite.png)

  

### TLS

As of writing (July 2021), there is really only one widely supported, secure protocol for establishing secure communications on the Internet -- TLS 1.2.

Even Microsoft which has a history of supporting legacy items (looking at you Internet Explorer) [is deprecating TLS 1.0 and TLS 1.1](https://docs.microsoft.com/en-us/lifecycle/announcements/transport-layer-security-1x-disablement) in many of its products (and in some cases outright disabling). And just in case it wasn't clear, all versions of SSL are insecure as well. Fully updated installs of [Windows 10](https://docs.microsoft.com/en-us/windows/win32/secauthn/protocols-in-tls-ssl--schannel-ssp-) and [macOS](https://support.apple.com/guide/deployment-reference-macos/network-security-apd1775f8cbb/web), unfortunately, still leave TLS 1.0 enabled for client and server connections.

Chrome, Safari, Firefox, and Edge dropped support for anything less than TLS 1.2 [a while back now](https://www.computerworld.com/article/3313589/big-browsers-to-pull-support-plug-for-tls-10-and-11-encryption-protocols-in-early-20.html). If you're using an up-to-date version of one of those browsers you are good-to-go there (note this doesn't mean other applications on your system won't use TLS 1.0/1.1).

Vendors are currently working on adoption and I hope that very soon TLS 1.3 will replace TLS 1.2. Cloudflare has a fantastic [blog post](https://blog.cloudflare.com/rfc-8446-aka-tls-1-3/) on TLS 1.3 covering its design changes, benefits over TLS 1.2, and overall a ton of great information on the topic. Once you're done here I highly encourage checking it out.

If this were a couple years ago, this section would have been A LOT longer. Thankfully now, most everyone agrees just using TLS 1.2 is the way to go. Now on to cipher suites where things are...less decisive, let's say.

### Secure Cipher Suites

NIST's latest guidelines ([SP 800-52r2](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-52r2.pdf)) can mostly be broken down into this:

1. *Prefer ephemeral keys over static keys (i.e., prefer DHE over DH, and prefer ECDHE
   over ECDH). Ephemeral keys provide perfect forward secrecy.*
2. *Prefer GCM or CCM modes over CBC mode. The use of an authenticated encryption
   mode prevents several attacks (see Section 3.3.2 for more information). Note that these
   are not available in versions prior to TLS 1.2.*
3. *Prefer CCM over CCM\_8. The latter contains a shorter authentication tag, which
   provides a lower authentication strength.*

This means that all of the following are technically acceptable ciphers, but some are more secure than others:

- TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384 (0xC0, 0x2C)
- TLS\_ECDHE\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0xC0, 0x30)
- TLS\_DHE\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x00, 0x9F)
- TLS\_DHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x00, 0x39)
- TLS\_DH\_DSS\_WITH\_AES\_256\_GCM\_SHA384 (0x00, 0xA5)
- TLS\_DH\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x00, 0xA1)

The ciphers given in NIST documentation also aren't the only ones used. For example, these ciphers Google Chrome v92 uses to negotiate with [clienttest.ssllabs.com](http://clienttest.ssllabs.com):

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhiXNGPjPHNXDXarFye-bC1S_9aC-pQa_f-fVHAThyphenhyphenX3LqDGOoLP0THr7pxtJ1FKOy3UIJelYbHglyMCM_aGQl3fx4Ho__ctLKDvwYGOLqQZRfpwLC1FSW5mrPKXSBKBxExOAL3WweUjb9g/w640-h382/2021-07-27+20_44_18-Window.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhiXNGPjPHNXDXarFye-bC1S_9aC-pQa_f-fVHAThyphenhyphenX3LqDGOoLP0THr7pxtJ1FKOy3UIJelYbHglyMCM_aGQl3fx4Ho__ctLKDvwYGOLqQZRfpwLC1FSW5mrPKXSBKBxExOAL3WweUjb9g/s1144/2021-07-27+20_44_18-Window.png)

  

You'll notice CHACHA20 and POLY1305 listed (used for encryption and MAC respectively). NIST may not have adopted these, but [tests so far](https://eprint.iacr.org/2007/472) indicate they are secure (not to mention fast which is why they were adopted -- specifically as a stream cipher for mobile devices where AES computations are expensive).

By default, Windows 10 fully patched in July 2021 [still allows NULL cipher suites](https://docs.microsoft.com/en-us/windows/win32/secauthn/tls-cipher-suites-in-windows-10-v1903) (cipher suites that don't perform any encryption of the data but provide authenticity and integrity checks) among other insecure cipher suites. I'll be covering how to disable these and restrict usage to secure cipher suites in a future post.

Edit: Here is the future post (<https://blog.codyrichardson.io/2021/12/configuring-secure-ciphers-suites-and.html>).

### References

<https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-52r2.pdf>

<https://docs.microsoft.com/en-us/windows/win32/secauthn/cipher-suites-in-schannel>

<https://blog.cloudflare.com/rfc-8446-aka-tls-1-3/>

<https://blog.cloudflare.com/do-the-chacha-better-mobile-performance-with-cryptography/>

<https://eprint.iacr.org/2007/472>

<https://docs.microsoft.com/en-us/windows/win32/secauthn/protocols-in-tls-ssl--schannel-ssp->

<https://support.apple.com/guide/deployment-reference-macos/network-security-apd1775f8cbb/web>