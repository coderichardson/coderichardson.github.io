---
title: "Configuring Secure Ciphers Suites and TLS"
date: 2021-12-18 23:17:00 +0000
tags:
  - "Ciphers"
  - "TLS/SSL"
  - "Windows"
---

Hey everyone, today we're back on cipher suites. If you want a refresher of TLS and secure cipher suites overall, check out [my previous post](https://blog.codyrichardson.io/2021/07/secure-cipher-suites-and-tls-in-2021.html).

There are many instances in which you'll need to edit cipher suites on a system -- compliance efforts, CIS benchmarks, or simply ensuring your system doesn't use insecure suites. There are a few ways to go about this and I'll detail two of them now: IIS Crypto and the Windows registry.

### IIS Crypto

My favorite way of editing TLS versions and cipher suites is using [IIS Crypto](https://www.nartac.com/Products/IISCrypto). IIS Crypto allows you to select your desired TLS/SSL version, cipher suites, and backup the registry, all with a few mouse clicks. Only downside is that it's Windows only (even the command line version).

![](/assets/img/posts/configuring-secure-ciphers-suites-and/01.jpg)
This is what IIS Crypto will look like on an unmodified Windows 10 system. Note the separate **Server Protocols** and **Client Protocols** sections. These are important to keep straight depending on what system is listening for connections and what system is initiating connections. If you modify just one of these on both a server and client you may break their ability to make a connection!

Also, notice all the boxes are checked but seemingly "grayed out". This is IIS Crypto indicating that the default value is set. This is also true over on the **Cipher Suites** page. Yes, there are multiple pages with mostly redundant information on them that you need to ensure both are set accurately. More on that later. (Also, if you're curious about some of the functionality of IIS Crypto they have [a great FAQ](https://www.nartac.com/Products/IISCrypto/FAQ)).

![](/assets/img/posts/configuring-secure-ciphers-suites-and/02.jpg)
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

![](/assets/img/posts/configuring-secure-ciphers-suites-and/03.jpg)
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

![](/assets/img/posts/configuring-secure-ciphers-suites-and/04.jpg)
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

![](/assets/img/posts/configuring-secure-ciphers-suites-and/05.jpg)
*Credit: Microsoft (https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/manage-ssl-protocols-in-ad-fs)*

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