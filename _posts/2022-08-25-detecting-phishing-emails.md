---
title: "Detecting Phishing Emails"
date: 2022-08-25 00:48:00 +0000
tags:
  - "Email"
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiemazsbJQSBY5kawdl9mAxPENRcqueqEJOSJCnLUQwK-FirfSCC0EKBXLQ9YeOMV_2ExXQqcY8SGgMeucTjHalHBqgSMI5F2eH5Koi3f9tJFIixbU_lArogXV5UqOpxEi012cLRjvtlDJOrIZ9nkb02yLMKZDh_U8e_MnpPM1JTvs3woOEh1gozoTb6Q/w640-h426/istockphoto-1078729656-612x612.jpg)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiemazsbJQSBY5kawdl9mAxPENRcqueqEJOSJCnLUQwK-FirfSCC0EKBXLQ9YeOMV_2ExXQqcY8SGgMeucTjHalHBqgSMI5F2eH5Koi3f9tJFIixbU_lArogXV5UqOpxEi012cLRjvtlDJOrIZ9nkb02yLMKZDh_U8e_MnpPM1JTvs3woOEh1gozoTb6Q/s612/istockphoto-1078729656-612x612.jpg)

Detecting and preventing the effects of phishing emails has become a primary interest for enterprises and governments today. Often because phishing emails lead to network breaches, ransomware, and exfiltration of sensitive information.

Patching vulnerabilities, ensuring AV/EDR/XDR is installed on endpoints, network segmentation, and MFA are all great to do, but one step we can take before relying on these measures is ensuring the end-user community is routinely educated on how to detect phishing emails.

So how do we detect phishing emails?

## Screening Emails

Here are some of the items on what I call my "initial phishing screening checklist":

- Sender name and email address (especially domain) that doesn't match a legitimate one.
- Statements urging me to act quickly.
- Was I expecting an email like this?
- If I know the person and/or can reach them by phone, can I confirm it is them truly sending the email? (Out-of-band communication).

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhq5jux5YX05YCDGWYAHjy_X51MjG7qTFPUMyiEU86aBAeas7PWoXUiFt-Yf5fVjtA4l0N5LrrjWbBg_ZOPZKA1sZpc7vSBJaxgyyuIC-em-TIVTB__yLs_UsI8qGp8S6nljbfVpTgFLye9_NIIh00xi4krJYmRjw9E40QorsQyyR9wx6ixmHXIvhHh7g/w640-h389/phishing-attack-email-example.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhq5jux5YX05YCDGWYAHjy_X51MjG7qTFPUMyiEU86aBAeas7PWoXUiFt-Yf5fVjtA4l0N5LrrjWbBg_ZOPZKA1sZpc7vSBJaxgyyuIC-em-TIVTB__yLs_UsI8qGp8S6nljbfVpTgFLye9_NIIh00xi4krJYmRjw9E40QorsQyyR9wx6ixmHXIvhHh7g/s795/phishing-attack-email-example.png)

At least on this one they give 24 hours not "this needs to be done immediately or you will lose access!"

Know that no single one of these is a fool-proof method of detecting a phishing email. Or even if all of these "red flags" are present it could still be a legitimate email. With these types of indicators detecting phishing emails is part art and part science.

Honorable mention - Outlook (and likely other email clients) will display a contact photo of someone in your organization just because the sending name and email matches and known contact. Outlook doesn't know or care that that information was spoofed and that the email header shows the email came from another country, not your co-worker. Don't rely on name, email, or picture as reliable indicators for email.

## Digging Deeper

The initial screening process is good, but it won't get you very far when someone can spoof the sending email address of your company, has the email signature of someone at your company, and they write a very convincing email as to why you should open their attached document.

Without additional hints like an [external email banner](https://o365reports.com/2020/03/25/how-to-add-external-email-warning-message/), this could be a difficult email to detect as phishing.

So let's dig a bit deeper.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjDHHkH3FHq3TUPJxO16Mj_iKsGaZgwcJiQRaKZDDy7wlx4t5_U7UZj3uEUx-DbYJMCCbyeZc8NyX0Hhi3222fg7yRvPEc3mkgl_NLBOvNyimmrHtubEeVQVApE1w8lbegCgT8XEfdpw-slG8QMyKJk_dMjiopDJtq94DQRgNSOp7sRg4dkiWcxvZymIg/w640-h410/email_envelope_vs_email_header.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjDHHkH3FHq3TUPJxO16Mj_iKsGaZgwcJiQRaKZDDy7wlx4t5_U7UZj3uEUx-DbYJMCCbyeZc8NyX0Hhi3222fg7yRvPEc3mkgl_NLBOvNyimmrHtubEeVQVApE1w8lbegCgT8XEfdpw-slG8QMyKJk_dMjiopDJtq94DQRgNSOp7sRg4dkiWcxvZymIg/s482/email_envelope_vs_email_header.png)

  

The three components of an email are (1) the SMTP envelope, (2) email header, and (3) the body of the email.

The **SMTP envelope** is similar to the traditional envelope that someone delivering your mail would see. It contains a record showing who the email is from and who to send it to. As this gets passed along from mail carrier to mail carrier (or SMTP server / mail transfer agent in the case of email), that's all that needs to be seen to know where to deliver the piece of mail.

Mail carriers never have to open the mail and see who it's addressed to, and servers don't need to look beyond the SMTP envelope for their information. In the case of email, the email client (Outlook, Gmail, etc.) doesn't display the SMTP envelope information to the user, just the information in the email header.

The **email header** is another location where sending address and intended recipient are entered. In most legitimate cases, these entries are the same as what's found on the SMTP envelope. In the case of phishing emails, these can be completely different and there is nothing built-in to the SMTP protocol to protect against it. The email client will display whatever information is located here and not check against the SMTP envelope for consistency. This is how an email from across the world can be spoofed to look like it came from your co-worker according to Outlook.

The **email body** is the actual email message. The link, attachment, or words that the sender wants you to interact with.

In reality, just about all elements of the SMTP envelope and email header can be spoofed. If a phishing email is expertly crafted, these can all look legitimate but the email still be phishing.

That being said, actually looking at the contents of the header and SMTP envelope is the best thing to do after going through the "initial screening process" we talked about earlier. Most often the email header will be spoofed, but the SMTP envelope is left alone to show the true source of the email.

## Detonating

If all other checks are inconclusive, the link and/or attachment needs to be detonated in a sandbox environment. This can be an isolated virtual machine or it can be a spare laptop you have disconnected from the network or on a separate network.

If you don't want to do it yourself, many companies provide this service for a fee. Office 365 has a great offering in their [Safe Links](https://docs.microsoft.com/en-us/microsoft-365/security/office-365-security/safe-links?view=o365-worldwide) and [Safe Attachments](https://docs.microsoft.com/en-us/microsoft-365/security/office-365-security/safe-attachments?view=o365-worldwide) features that detonates attachments and links before they are sent to the recipient.

That being said, nothing beats a "dirty laptop" running Wireshark, Procmon, and other tools to detect what opening a given link will do. But with enough volume of phishing emails it's nice to offload some of that work to a service.

## Protections - SPF, DKIM, DMARC

Since email and SMTP were created we've come to recognize some of the shortfalls of SMTP. It was not designed with security in mind. As a result, solutions such as these were invented:

- Sender Policy Framework (SPF)
- Domain Keys Identified Mail (DKIM)
- Domain Based Message Authentication Reporting and Conformance (DMARC)

These all have their own pros and cons and I intend to write another post about them. For now, know that they are: good to implement from a security perspective, assist your organization's emails in not being caught in spam filters, and protect against someone spoofing your company's domain and not getting caught.

## Conclusion / Final Thoughts

There's a reason phishing emails are still a major tool used by threat actors -- they can be hard to detect and can have devastating impact. I hope some of this information helps in detecting and filtering out phishing emails from your organization.

A personal note: there seems to be a bit of a debate in the online infosec community these days as to whether security awareness training provides real value in educating end users. In case you're not aware, these services provide end-user awareness training typically in the form of company created phishing emails. These fake phishing emails are then tracked to see if the end-users click the phishing link/attachment so IT/Security can be made aware. My opinion is that as long as the price is reasonable, educating users and filtering out a non-zero percentage of real phishing emails by helping people recognize them and deleting them is a real value. This type of training should be accompanied by other methods of training such as small groups, regular informational emails/blogs/posters, and annual formal training.

Lastly, in case anyone wants to read them, here are the RFCs for SMTP:

**SMTP Envelope**

<https://www.rfc-editor.org/rfc/rfc5321>

**SMTP Header/Email**

<https://www.rfc-editor.org/rfc/rfc5322>