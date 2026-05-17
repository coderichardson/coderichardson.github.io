---
title: "Windows Security Overview"
date: 2022-07-17 22:21:00 +0000
tags:
  - "Windows"
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiPRikAUHAVpVGgCvsH46tp_QN8FjUwVnCFGYIOirLMe-XoTP8waHGOjyaWUjjO2b6ifo4NTs3R3msLopXekBQJIFVGvti4_s_8Wxs4bZYZBB9nFtrRdj9us_XPrafhDL8jYRGt06itags6-lMI0rnLiXEPGFPenP0SJKXELTnwG3vRSTsEVs1w_n-oHg/w640-h360/win10_wallpaper.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiPRikAUHAVpVGgCvsH46tp_QN8FjUwVnCFGYIOirLMe-XoTP8waHGOjyaWUjjO2b6ifo4NTs3R3msLopXekBQJIFVGvti4_s_8Wxs4bZYZBB9nFtrRdj9us_XPrafhDL8jYRGt06itags6-lMI0rnLiXEPGFPenP0SJKXELTnwG3vRSTsEVs1w_n-oHg/s3840/win10_wallpaper.jpg)

  

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

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgHpB88AboEd2Eb5cTAVRmSR-KnA8czgFHmTGu_RN3GFcUNvVUDAdHRegxZfT9sWmm3KbIpfjsj9Y1oZJqfmaJcNnXOo70T88Bfs3ACgbStzQcdEg6I2Og2CIKvk7u8_lNqba_1IGdyzoKdEuAGFK3y_p1_FvBHuLsUImuPc_O41SckAGAqzpWa5pd3MA/w640-h566/2022-07-17%2017_13_04-Windows%20Security.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgHpB88AboEd2Eb5cTAVRmSR-KnA8czgFHmTGu_RN3GFcUNvVUDAdHRegxZfT9sWmm3KbIpfjsj9Y1oZJqfmaJcNnXOo70T88Bfs3ACgbStzQcdEg6I2Og2CIKvk7u8_lNqba_1IGdyzoKdEuAGFK3y_p1_FvBHuLsUImuPc_O41SckAGAqzpWa5pd3MA/s1039/2022-07-17%2017_13_04-Windows%20Security.png)

  

Specifically, in the Windows Security app you can manage Windows Defender (Virus & Threat Protection), your Microsoft account (Account Protection), Windows Firewall (Firewall & Network Protection), and new features such as App & Browser Control and those found under Device Security.

#### Windows Defender

Windows Defender (renamed Microsoft Defender, but I'm sticking with the Windows Defender title for now) has been around for a while now, but Windows 10 gave it the kick it needed to be a full-fledged antivirus product. It can perform active protection against executables, downloads, etc., scheduled scans, and of course manual scans on the entire system or just individual files.

It's not as good as many of the third party applications available, but it's far better than nothing.

Note that this is not the same as [Microsoft Defender for Endpoint](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint?view=o365-worldwide). Microsoft Defender for Endpoint is an enterprise antivirus application with additional features (and of course licensing costs).

#### Windows Firewall

Much like other areas of Windows 10 though (and Windows 11 as of this writing), configuring elements such as Windows Firewall are performed using the older interfaces. Depending on your opinion about the new applications and interfaces within Windows, that may be a good thing. 😀

Because of this, Windows Firewall largely works the same as it has for years. Rule creation is relatively straight-forward with options to enable/disable based on the network type your system is connected to.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEigYQdqMFvVZBZMSZhRayICvjhOu54VK6YS2iEJrDvHBrjiv1Amp6sKOhSZTYOsKQYEHA9JXfIZGie5JAGQ2mmF9hUXsbhF4nSeLMbDcpu23SJVfkMSPRxTwPyg-nR5BqP-Bk4jR42rQpl7mUvt8noA1_Tp9smiDMfegveZtG0KFUuHJzgO_nFGh_My1w/w640-h480/2022-07-17%2017_17_42-Windows%20Defender%20Firewall%20with%20Advanced%20Security.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEigYQdqMFvVZBZMSZhRayICvjhOu54VK6YS2iEJrDvHBrjiv1Amp6sKOhSZTYOsKQYEHA9JXfIZGie5JAGQ2mmF9hUXsbhF4nSeLMbDcpu23SJVfkMSPRxTwPyg-nR5BqP-Bk4jR42rQpl7mUvt8noA1_Tp9smiDMfegveZtG0KFUuHJzgO_nFGh_My1w/s1047/2022-07-17%2017_17_42-Windows%20Defender%20Firewall%20with%20Advanced%20Security.png)

#### App Control

App Control (Windows Defender Application Control / WDAC) is Microsoft's latest protection against running malicious software, or for enterprises, software a company simply doesn't want run without permission from the IT departments. It is an improvement on AppLocker.

Rules for software can be based on code-signing certificates (similar idea to Secure Boot and Trusted Boot), file hash, file name, file reputation, and more.

On personal systems the reputation checks alone are a great, free additional layer of security.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhbOekpPMa2fkUw9aK5YTuwPS2NaWXHi4GFUnHe32vh7dPteov8wy4_4ec8MFqKFnCNEWVs1I7wmIdEqwPFsYrYQlw7nK7h_T9qx4GX15C8qb5_zlw0jg0Ryb8diu66WM7wRrXQ14LLPGD_8zzz4RDgFAEOiF4IqPYuFTHDd4KINDPLgdPphyXuVWctiQ/w640-h530/2022-07-17%2017_30_20-Windows%20Security.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhbOekpPMa2fkUw9aK5YTuwPS2NaWXHi4GFUnHe32vh7dPteov8wy4_4ec8MFqKFnCNEWVs1I7wmIdEqwPFsYrYQlw7nK7h_T9qx4GX15C8qb5_zlw0jg0Ryb8diu66WM7wRrXQ14LLPGD_8zzz4RDgFAEOiF4IqPYuFTHDd4KINDPLgdPphyXuVWctiQ/s1030/2022-07-17%2017_30_20-Windows%20Security.png)

#### Device Security

Under Device Security you can confirm that Secure Boot is enabled, but this section also allows you to enable features such as *Memory Integrity* and verify your system has a Trusted Platform Module (TPM) and it is in use. More information on these topics can be found [on Microsoft's website](https://support.microsoft.com/en-au/windows/device-protection-in-windows-security-afa11526-de57-b1c5-599f-3a4c6a61c5e2).

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgRyJihsSv9dJp-EnWQUF06Z4AxZuUDb2VcKmcbcQ55MSRn5yuTqq5GouzJn7UJa2fale7nDE0zEo6OIw8FSG8LaSFuZP3JH39BKlONeuQ8MIV25YTWEm6uAJ4qDaR79aKeFlVKBAmmf-7g91GOSWbl6NJ8rMI_7e8MriGWOB0YEMAtgzt_NTkJ8gu0bQ/w346-h400/CoreIsolation_SecurityProcessor.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgRyJihsSv9dJp-EnWQUF06Z4AxZuUDb2VcKmcbcQ55MSRn5yuTqq5GouzJn7UJa2fale7nDE0zEo6OIw8FSG8LaSFuZP3JH39BKlONeuQ8MIV25YTWEm6uAJ4qDaR79aKeFlVKBAmmf-7g91GOSWbl6NJ8rMI_7e8MriGWOB0YEMAtgzt_NTkJ8gu0bQ/s599/CoreIsolation_SecurityProcessor.png)

## BitLocker

BitLocker provides drive encryption to secure your system given you are running Windows 10/11 Pro, Enterprise, or Education.

Sadly, that means BitLocker will not work on Windows Home versions of the OS. This is one thing personally I was hoping to see change with Windows 11, but I guess it is still generally more of an enterprise requirement. Maybe one day. In my opinion, this is the strongest argument for Home users to upgrade to Pro if the system in question is a laptop. Even more so if you travel frequently.

BitLocker supports a variety of methods for authentication, encrypts the drive using AES 128 by default though AES 256 is available, integrates well with Domain environments for enterprises looking for a drive encryption solution, and supports several secure options for recovery.

Details on BitLocker deployment can be found [on Microsoft's site](https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-basic-deployment).

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiWNDSMHf0iOIzc84YObXPfExhi5QJFiUkkuP5mRHtvQT-SJBabxFyMqxssI6LhXxV-NBBKgMlM1Tg5eUFFV9goz7WhKJ3NInYvEvXMeXI5ztyz-eoT8OMJdYbHGTmXvRwAOla6LqYY6rgy47wbVRJgLQNAJPD5xev7FMG4UlCXv6HztWdcKy7GfIGd4Q/w400-h245/bitlocker1.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiWNDSMHf0iOIzc84YObXPfExhi5QJFiUkkuP5mRHtvQT-SJBabxFyMqxssI6LhXxV-NBBKgMlM1Tg5eUFFV9goz7WhKJ3NInYvEvXMeXI5ztyz-eoT8OMJdYbHGTmXvRwAOla6LqYY6rgy47wbVRJgLQNAJPD5xev7FMG4UlCXv6HztWdcKy7GfIGd4Q/s627/bitlocker1.jpg)

## Conclusion

Some honorable mentions I didn't get into here are things like [Windows Hello](https://blogs.windows.com/windowsexperience/2016/10/31/windows-10-tip-how-to-set-up-windows-hello-on-your-pc/), [Credential Guard](https://docs.microsoft.com/en-us/windows/security/identity-protection/credential-guard/credential-guard), and [recovery options](https://support.microsoft.com/en-us/windows/recovery-options-in-windows-31ce2444-7de3-818c-d626-e3b5a3024da5) available in the Windows Recovery Environment.

Microsoft Windows in 2022 includes a large number of security features "out-of-the-box" even for Home users. I'd expect this trend to continue as Windows 11 is further developed and OS changes are made with a focus on security moving forward.