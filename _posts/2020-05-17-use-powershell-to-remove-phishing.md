---
title: "Use PowerShell to Remove Phishing Emails from Users' Mailboxes in Office 365"
date: 2020-05-17 17:21:00 +0000
tags:
  - "PowerShell"
  - "Email"
  - "Cybersecurity"
---

Anyone on the blue team side of security thinks about how to prevent and train users not to click on phishing emails. Phishing emails are the initial vector [for the vast majority of companies that fall victim to ransomware](https://www.vadesecure.com/en/ransomware-attacks-why-email-is-still-the-1-delivery-method/), and others [harvest credentials to be used in data breaches](https://blog.rapid7.com/2019/08/20/how-attackers-can-harvest-users-microsoft-365-credentials-with-new-phishing-campaign/).

Office 365 / Exchange Online provides built-in protections for anti-spam and anti-phishing efforts (including ATP), but these can also be combined with 3rd party external vendors such as Symantec, ProofPoint, Cisco, SOPHOS, and more. With these technologies in place the percentage of phishing emails that are received by your users drops significantly. Most provide protection even if an email gets through by screening links and attachments if a user clicks on them (in addition to your local AV software).

But because we know that some of the emails will get through and we want them deleted as soon as possible, we have two options:

1. Send out an email asking people to be aware of a phishing email circulating the company and to delete it if received.
2. Remove the email from users' mailboxes before they have a chance to open it.

It's this second option we'll be exploring in the rest of this post. It takes only minutes to setup and perform, and is a great addition to your anti-phishing toolkit.

However, the commands given here (especially the purging of emails as admin across your Office 365 tenant) are extremely powerful and should be used carefully. If you're unsure of what you're doing, stop, and read about the commands in [Microsoft's documentation](https://docs.microsoft.com/en-us/office365/enterprise/powershell/cmdlet-references-for-office-365-services).

**Prerequisites**

1. Use Office 365 / Exchange Online for your email provider and be a Global Administrator.

2. Update PowerShell to at least v5.1.

3. Install the Exchange Online Remote PowerShell Module from Office 365:

```powershell
Start-Process "iexplore.exe" "https://cmdletpswmodule.blob.core.windows.net/exopsmodule/Microsoft.Online.CSE.PSModule.Client.application"
```

![](/assets/img/posts/use-powershell-to-remove-phishing/01.jpg)
**Search & Purge**

Launch the newly installed Exchange Online Remote PowerShell Module from PowerShell.

```powershell
explorer.exe "$env:appdata\Microsoft\Windows\Start Menu\Programs\Microsoft Corporation\Microsoft Exchange Online Powershell Module.appref-ms"
```

A separate PowerShell window will appear -- your Exchange Online Remote PowerShell Module.

![](/assets/img/posts/use-powershell-to-remove-phishing/02.jpg)
Connect to Office 365.

```powershell
Connect-IPPSSession -UserPrincipalName <USERNAME>
```

Start a new Content Search in Office 365. The following search just uses the email subject, but [additional filters can be added](https://www.codetwo.com/admins-blog/search-mailbox-exchange-2013-2016-online-attributes/).

```powershell
New-ComplianceSearch -Name "<NAME OF SEARCH>" -ExchangeLocation All -ContentMatchQuery 'Subject:"<EMAIL SUBJECT>")'
```

Start the Content Search we just created.

```powershell
Start-ComplianceSearch "<NAME OF SEARCH>"
```

Check the status of the Content Search.

```powershell
Get-ComplianceSearch -Identity "<NAME OF SEARCH>" | Format-Table -Auto Name,RunBy,JobEndTime,Status,Items
```

Purge the email from any location it is found. By default this performs a "Soft" delete, where the user can restore the email within Outlook. Additional parameters available for a "Hard" delete.

```powershell
New-ComplianceSearchAction -SearchName "<NAME OF SEARCH>" -Purge
```

Check the status of the Purge.

```powershell
Get-ComplianceSearchAction -Identity "<NAME OF SEARCH>_Purge"
```

Disconnect the current session.

```powershell
Get-PSSession | Remove-PSSession
```



And the phishing email is gone!