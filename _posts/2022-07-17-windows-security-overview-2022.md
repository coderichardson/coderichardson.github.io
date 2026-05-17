---
title: "Windows Security Overview"
date: 2022-07-17 22:21:00 +0000
tags:
  - "Windows"
  - "Cybersecurity"
---

![](/assets/img/posts/windows-security-overview-2022/01.jpg)
In terms of security, we've come a long way since the days of Windows XP. Even compared to your typical Windows 7 Enterprise install just a few years ago there have been huge security advancements in the industry and specifically within Windows. Here is an overview of some of those improvements, and if this series is popular enough, I may do a deep-dive on some of the individual features in the future.

## Secure Boot

Before ransomware became the go-to malware for bad actors, one of the popular, more sophisticated pieces of malware was the rootkit. This allowed code to be run in kernel mode within Windows effectively bypassing most antivirus software installed on the system. This also meant being capable of performing almost anything on the system without issue.

To mitigate this issue something was needed to verify that the bootloader run before Windows was legitimate. This is where Secure Boot fits into the Windows Security picture (though Secure Boot works with macOS and Linux computers as well). For more details, [Microsoft has an interesting write-up](https://docs.microsoft.com/en-us/windows-hardware/design/device-experiences/oem-secure-boot) directed to OEMs as the audience regarding Secure Boot.

The bootloader is signed using a trusted certificate. When this signature is checked during the startup process, if valid, the operating system is subsequently allowed to boot. The baton is then handed over to *Trusted Boot.*

## Trusted Boot

Trusted Boot relies on a similar concept as Secure Boot in regards to digital signatures, but instead of the bootloader being signed, the signature is for the Windows kernel. This is verified as legitimate and the boot process continues.

Windows then verifies the subsequent steps in the boot-up process such as drivers.

## Windows Security App

The Windows Security app was introduced in Windows 10. It consolidates management of several components in prior versions of Windows and adds additional features as well.

![](/assets/img/posts/windows-security-overview-2022/02.png)
Specifically, in the Windows Security app you can manage Windows Defender (Virus & Threat Protection), your Microsoft account (Account Protection), Windows Firewall (Firewall & Network Protection), and new features such as App & Browser Control and those found under Device Security.

#### Windows Defender

Windows Defender (renamed Microsoft Defender, but I'm sticking with the Windows Defender title for now) has been around for a while now, but Windows 10 gave it the kick it needed to be a full-fledged antivirus product. It can perform active protection against executables, downloads, etc., scheduled scans, and of course manual scans on the entire system or just individual files.

It's not as good as many of the third party applications available, but it's far better than nothing.

Note that this is not the same as [Microsoft Defender for Endpoint](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint?view=o365-worldwide). Microsoft Defender for Endpoint is an enterprise antivirus application with additional features (and of course licensing costs).

#### Windows Firewall

Much like other areas of Windows 10 though (and Windows 11 as of this writing), configuring elements such as Windows Firewall are performed using the older interfaces. Depending on your opinion about the new applications and interfaces within Windows, that may be a good thing. 😀

Because of this, Windows Firewall largely works the same as it has for years. Rule creation is relatively straight-forward with options to enable/disable based on the network type your system is connected to.

![](/assets/img/posts/windows-security-overview-2022/03.png)
#### App Control

App Control (Windows Defender Application Control / WDAC) is Microsoft's latest protection against running malicious software, or for enterprises, software a company simply doesn't want run without permission from the IT departments. It is an improvement on AppLocker.

Rules for software can be based on code-signing certificates (similar idea to Secure Boot and Trusted Boot), file hash, file name, file reputation, and more.

On personal systems the reputation checks alone are a great, free additional layer of security.

![](/assets/img/posts/windows-security-overview-2022/04.png)
#### Device Security

Under Device Security you can confirm that Secure Boot is enabled, but this section also allows you to enable features such as *Memory Integrity* and verify your system has a Trusted Platform Module (TPM) and it is in use. More information on these topics can be found [on Microsoft's website](https://support.microsoft.com/en-au/windows/device-protection-in-windows-security-afa11526-de57-b1c5-599f-3a4c6a61c5e2).

![](/assets/img/posts/windows-security-overview-2022/05.png)
## BitLocker

BitLocker provides drive encryption to secure your system given you are running Windows 10/11 Pro, Enterprise, or Education.

Sadly, that means BitLocker will not work on Windows Home versions of the OS. This is one thing personally I was hoping to see change with Windows 11, but I guess it is still generally more of an enterprise requirement. Maybe one day. In my opinion, this is the strongest argument for Home users to upgrade to Pro if the system in question is a laptop. Even more so if you travel frequently.

BitLocker supports a variety of methods for authentication, encrypts the drive using AES 128 by default though AES 256 is available, integrates well with Domain environments for enterprises looking for a drive encryption solution, and supports several secure options for recovery.

Details on BitLocker deployment can be found [on Microsoft's site](https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-basic-deployment).

![](/assets/img/posts/windows-security-overview-2022/06.jpg)
## Conclusion

Some honorable mentions I didn't get into here are things like [Windows Hello](https://blogs.windows.com/windowsexperience/2016/10/31/windows-10-tip-how-to-set-up-windows-hello-on-your-pc/), [Credential Guard](https://docs.microsoft.com/en-us/windows/security/identity-protection/credential-guard/credential-guard), and [recovery options](https://support.microsoft.com/en-us/windows/recovery-options-in-windows-31ce2444-7de3-818c-d626-e3b5a3024da5) available in the Windows Recovery Environment.

Microsoft Windows in 2022 includes a large number of security features "out-of-the-box" even for Home users. I'd expect this trend to continue as Windows 11 is further developed and OS changes are made with a focus on security moving forward.