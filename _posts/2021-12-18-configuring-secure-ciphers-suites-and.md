---
title: "Configuring Secure Ciphers Suites and TLS"
date: 2021-12-18 23:17:00 +0000
tags:
  - "Ciphers"
  - "TLS/SSL"
---

Hey everyone, today we're back on cipher suites. If you want a refresher of TLS and secure cipher suites overall, check out [my previous post](https://blog.codyrichardson.io/2021/07/secure-cipher-suites-and-tls-in-2021.html).

There are many instances in which you'll need to edit cipher suites on a system -- compliance efforts, CIS benchmarks, or simply ensuring your system doesn't use insecure suites. There are a few ways to go about this and I'll detail two of them now: IIS Crypto and the Windows registry.

### IIS Crypto

My favorite way of editing TLS versions and cipher suites is using [IIS Crypto](https://www.nartac.com/Products/IISCrypto). IIS Crypto allows you to select your desired TLS/SSL version, cipher suites, and backup the registry, all with a few mouse clicks. Only downside is that it's Windows only (even the command line version).

[![](https://blogger.googleusercontent.com/img/a/AVvXsEgAaEWnGGltr69maU5DKTdfCn1rL9KiEWjUx28c0w5Bq9b3H0GrSilliD475UQdbjTT5nbFNyslU2SKD352oT182zPMBq_asiR3J9LDKGHmrEgVF3fOC-MY1RY48MG5cztmmn8LsNv0tSlTDdn9IqaWD5ieovHG_X41nO437GKrb9lzUmlFTPMhe2TjHA=w640-h533)](https://blogger.googleusercontent.com/img/a/AVvXsEgAaEWnGGltr69maU5DKTdfCn1rL9KiEWjUx28c0w5Bq9b3H0GrSilliD475UQdbjTT5nbFNyslU2SKD352oT182zPMBq_asiR3J9LDKGHmrEgVF3fOC-MY1RY48MG5cztmmn8LsNv0tSlTDdn9IqaWD5ieovHG_X41nO437GKrb9lzUmlFTPMhe2TjHA=s886)

  

This is what IIS Crypto will look like on an unmodified Windows 10 system. Note the separate **Server Protocols** and **Client Protocols** sections. These are important to keep straight depending on what system is listening for connections and what system is initiating connections. If you modify just one of these on both a server and client you may break their ability to make a connection!

Also, notice all the boxes are checked but seemingly "grayed out". This is IIS Crypto indicating that the default value is set. This is also true over on the **Cipher Suites** page. Yes, there are multiple pages with mostly redundant information on them that you need to ensure both are set accurately. More on that later. (Also, if you're curious about some of the functionality of IIS Crypto they have [a great FAQ](https://www.nartac.com/Products/IISCrypto/FAQ)).

[![](https://blogger.googleusercontent.com/img/a/AVvXsEhvnsH53FaEYu51VKJRBlRsb0KgFOD2DkCiHMXnUSig6CVgoUfvh_Wrczkiv6rf1SQ8diBpnIg8RobbCvsIy5l7-lDgwR2oHwgmNvmZGGhysTlpQDwHmBTzjen-WH95rZY11YnfZQlMkzXQh-yyreC0zP66geFrpKnT7o6Ak_8yLnAFDBeyCuLLXxtIIw=w640-h532)](https://blogger.googleusercontent.com/img/a/AVvXsEhvnsH53FaEYu51VKJRBlRsb0KgFOD2DkCiHMXnUSig6CVgoUfvh_Wrczkiv6rf1SQ8diBpnIg8RobbCvsIy5l7-lDgwR2oHwgmNvmZGGhysTlpQDwHmBTzjen-WH95rZY11YnfZQlMkzXQh-yyreC0zP66geFrpKnT7o6Ak_8yLnAFDBeyCuLLXxtIIw=s886)

  

Check/un-check the desired protocols and cipher suites, then click **Apply**. You'll need to reboot your system for the changes to take effect (or check the "Reboot" box before clicking Apply in IIS Crypto).

Then you're done! Yes, it's really that easy. The hard part is troubleshooting connections you inevitably break because some software you have installed insists on using TLS 1.1 or won't work with ECDHE.

### Windows Registry

So [what is IIS Crypto actually doing](https://www.nartac.com/Products/IISCrypto/FAQ/what-registry-keys-does-iis-crypto-modify) that's making these changes? And what if I don't want to (or can't) install software to do this?

Don't worry. IIS Crypto is just conveniently modifying the registry so you don't have to.

Remember to backup your registry before making any changes and reboot after making these changes in the registry.

#### Protocols

Open Registry editor and navigate to:

HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\

On a default install of Windows there will be nothing beyond the Protocols key. For every protocol you want to enable or disable you will need to create a few things:

- One key under Protocols reflecting the name of the protocol (e.g. TLS 1.2)
- Two keys under *that* key -- **Client** and **Server**
- Two REG\_DWORD values -- **Enabled** and **DisabledByDefault**
- Set the Enabled value to **1** (binary) and the DisabledByDefault value to **0** (binary)

- This enables TLS 1.2 as a client protocol and it will be enabled by default.
- Swap these values if you want to disable the protocol.

[![](https://blogger.googleusercontent.com/img/a/AVvXsEiDZwg6zzaX72ie2JZuYHIKkBQ2dQDWcbwFUzdx21oscIVi5lx4xdxwHtqFEwFkSY76g-JZ5QkwwVj7t4YwZmktq0loblYHZ7nyXkf8Cxp4hIQ_ryApO_Bp7nhKXuG8TnbdEbqRYCj3S3htMqO2ovy7aj03QADb6ik8_FtwLUP5pRlY33cYtPiWxEAsZg=w640-h464)](https://blogger.googleusercontent.com/img/a/AVvXsEiDZwg6zzaX72ie2JZuYHIKkBQ2dQDWcbwFUzdx21oscIVi5lx4xdxwHtqFEwFkSY76g-JZ5QkwwVj7t4YwZmktq0loblYHZ7nyXkf8Cxp4hIQ_ryApO_Bp7nhKXuG8TnbdEbqRYCj3S3htMqO2ovy7aj03QADb6ik8_FtwLUP5pRlY33cYtPiWxEAsZg=s897)

  

#### Cipher Suites

Open Registry Editor and navigate to:

HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\

Again, this will be empty by default.

For every cipher suite you want to enable or disable you will need to create a few things:

- One key under Ciphers reflecting the name of the cipher in the following format:

- *Name* *VALUE*/*VALUE*
- E.g. SCHANNEL\Ciphers\AES 256/256

- One REG\_DWORD value -- **Enabled**
- Set the Enabled value to **1** (binary)

- This enables the cipher suite.
- Make Enabled **0** (binary) to disable the cipher.

[![](https://blogger.googleusercontent.com/img/a/AVvXsEjaf4nF4pqss4jwMtpi0v5ocyVPtbAE3KNY6awwmwyXUo34YMdUvSKxQbUZxfMulU2PINJXHdNuC922_Z3zFjeEziTwry-T8EU7jcSktjpBhWTuoGRaiP05znPCvPHQBj3Ae0nggXmWwAriuTuSq88VC7idZqEGm3oqC_p5t5IoQTLWjoqWRDIPL7StSQ=w640-h464)](https://blogger.googleusercontent.com/img/a/AVvXsEjaf4nF4pqss4jwMtpi0v5ocyVPtbAE3KNY6awwmwyXUo34YMdUvSKxQbUZxfMulU2PINJXHdNuC922_Z3zFjeEziTwry-T8EU7jcSktjpBhWTuoGRaiP05znPCvPHQBj3Ae0nggXmWwAriuTuSq88VC7idZqEGm3oqC_p5t5IoQTLWjoqWRDIPL7StSQ=s897)

#### Cipher Suite Order

Lastly, we have the Cipher Suite order. This is found at:

```text
HKEY\_LOCAL\_MACHINE\SOFTWARE\Policies\Microsoft\Cryptography\Configuration\SSL\00010002
```

Again, by default this will not have any values set.

You can edit this directly or [use Local Group Policy](https://docs.microsoft.com/en-us/windows-server/security/tls/manage-tls) (or of course normal Group Policy when pushing this change out to several systems).

Create a value named **Functions** of type REG\_MULTI\_SZ. This is where you list your desired cipher suites. If you choose to go this route, remember four things:

1. The order matters. First in the list will be tried first and so on. You may list 20 here but some applications may stop looking after 10. Prioritize appropriately.
2. The cipher suites are comma separated values.
3. Do not include any spaces.
4. The cipher suite(s) you want to use are named correctly. This can vary [depending on your Windows OS](https://security.stackexchange.com/questions/203128/what-are-the-p-values-in-some-cipher-string) (mostly around Elliptical Curve cipher suites as Windows 10/2016 no longer requires \_P256, etc., designations on EC suites while 2012R2 and before does).

|  |
| --- |
|  |
| Credit: Microsoft  (https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/manage-ssl-protocols-in-ad-fs) |

### Final Thoughts

You can see why I like IIS Crypto or controlling this via GPO.

Some other things I couldn't dedicate an entire section to today but want to mention:

1. Some applications will completely ignore your cipher suite preferences. For example, Google Chrome comes with its own set of cipher suites it will attempt to use when connecting with the world.
2. If you run into trouble remember [Wireshark](https://www.wireshark.org/) can tell you exactly what is being proposed as acceptable cipher suites on both the client and server sides.
3. Other parameters than those covered here can cause problems in connections -- for example, [KeyExchangeAlgorithms](https://www.nartac.com/Products/IISCrypto/FAQ/Why-are-some-of-the-new-cipher-suites-not-included-with-the-best-practices).
4. Linux/UNIX systems also need to be hardened to use TLS 1.2 with secure cipher suites. That's a post for a different day, but in case that's what you came here looking for here's a couple links to get you started:

- https://access.redhat.com/documentation/en-us/red\_hat\_enterprise\_linux/7/html/security\_guide/sec-hardening\_tls\_configuration
- https://community.tenable.com/s/article/How-to-check-the-SSL-TLS-Cipher-Suites-in-Linux-and-Windows
- https://unix.stackexchange.com/questions/153917/openssl-updating-ciphers-suites

Hope this helps!