---
title: "SPF, DKIM, and DMARC Explained"
date: 2023-02-18 15:51:00 +0000
tags:
  - "Email"
  - "Cybersecurity"
---

## 

I found myself reading [RFC 733](https://www.rfc-editor.org/rfc/rfc733) today as I had no idea how long BCC emails had been around. Turns out, it's a long time (November 21, 1977). In fact, that is when the "Standard for the Format of ARPA Network Text Messages" was ratified so a whole lot of other things were included in that RFC that are still used in email today, not just BCC emails.

Some things that weren't proposed in 1977 for obvious reasons are [SPF](https://www.rfc-editor.org/rfc/rfc7208), [DKIM](https://www.rfc-editor.org/rfc/rfc6376), and [DMARC](https://www.rfc-editor.org/rfc/rfc7489). We'll be talking about those today! (If you're curious like I was what those RFCs are anyway, I linked them so you can check those out too). 

## SPF - Sender Policy Framework

SPF is an authentication mechanism that allows an email server to verify that an email it receives was sent from an authorized server. SPF does this by checking the domain contained in the email header (specifically the envelope sender/MAILFROM), queries for an SPF TXT record that should be contained in that domain's DNS records, and depending on what that record says the email server can take appropriate action.

Let's run through an example:

1. Apple sends an email to your Gmail inbox. This email leaves Apple's email server bound for one of Google's email servers.
2. Upon reaching Google's email server, Google's server checks the domain contained in the envelope sender (in the header of the email).
3. Google's server checks the DNS records of email.apple.com and determines that the sending IP address (sending email server) is authorized to send email from email.apple.com. Hence we can see in the email header spf=pass along with the IP address of the sending email server, and the statement that the IP address is a permitted sender.  

   ![SPF Pass](/assets/img/posts/spf-dkim-and-dmarc-explained/03.png)
4. As a result of SPF passing, Google's email server will not mark the email as spam ultimately helping it reach your inbox. This isn't the only check it will perform but we'll get to the rest later.

So what exactly is the SPF record that Google checks to ensure that the specified IP address / domain is a permitted sender?

```text
v=spf1 include:_spf-txn.apple.com include:_spf-mkt.apple.com include:_spf.apple.com ~all
```

SPF records can be checked a number of ways, but [MXToolbox's SuperToo](https://mxtoolbox.com/SuperTool.aspx)l is my favorite (and where the above output came from).

A quick breakdown on each of the components included above, also courtesy of MXToolbox's output.

| Prefix | Type | Value | PrefixDesc | Description |
| --- | --- | --- | --- | --- |
|  | v | spf1 |  | The SPF record version |
| + | include | [\_spf-txn.apple.com](https://mxtoolbox.com/SuperTool.aspx?action=spf%3agappssmtp.com&run=toolpage#) | Pass | The specified domain is searched for an 'allow'. |
| + | include | [\_spf-mkt.apple.com](https://mxtoolbox.com/SuperTool.aspx?action=spf%3agappssmtp.com&run=toolpage#) | Pass | The specified domain is searched for an 'allow'. |
| + | include | [\_spf.apple.com](https://mxtoolbox.com/SuperTool.aspx?action=spf%3agappssmtp.com&run=toolpage#) | Pass | The specified domain is searched for an 'allow'. |
| ~ | all |  | SoftFail | Always matches. It goes at the end of your record. |

A few notes:

- "include" statements can have hostname or IP address values (or both!)
- The "~all" in Apple's case could just have easily have been "-all" if they wanted (or not included it at all). The difference being that "~" tells the receiving email server that if SPF fails, the email should be marked as suspicious. "-" tells the receiving email server that if SPF fails, the email should be rejected.
- Instead of (or in addition to) "include" SPF records can contain other ways of designating permitted senders such as "a" and "mx".

In the example above you will notice that the IP address in the header (17.111.110.120) isn't specifically listed in the SPF record, nor is email.apple.com. Yet, SPF passes.

The reason for this is \_spf-txn.apple.com which does specifically list 17.111.110.0/23 as a permitted sender (among other subnets). In this way the SPF record is nested with permitted senders! Not something I personally see very often, but for a company the size of Apple it makes sense.

SPF is not without its pitfalls though. The biggest being that SPF looks at the envelope sender (MAILFROM) -- the part of the email that most users don't see. So attackers can use a domain they control, implement the correct TXT record for SPF to pass, but then spoof the the part of the email that users do see (letter sender/FROM) tricking them into thinking it has passed a security check it really hasn't.

## DKIM - DomainKeys Identified Mail

DKIM is an authentication mechanism with many similarities SPF. It verifies that an email server did indeed send a particular email, does this by performing a lookup of DNS records, and looks at the envelope sender/MAILFROM of an email to know what DNS records to lookup. However, there is a bit more under the hood. Let's go back to our Apple example we used in SPF:

1. Apple sends an email to your Gmail inbox.
2. Before the email leaves the Apple email server, the email body is hashed, and the body plus select email headers are digitally signed (hashed then encrypted with a private key).
3. Upon reaching Google's email server, Google's server checks the domain contained in the envelope sender/MAILFROM (in the header of the email).
4. Google's email server, upon checking the DNS records of Apple, sees that Apple has published a public key as a TXT record.
5. Google's email server takes this public key, decrypts the digital signature in Apple's email, and verifies that the hash Apple provided matches the value Google gets when they hash the received email. If the values match, DKIM passes!

This authentication design provides not just authenticity but integrity of the email as the hashes would not match if the email was altered in transit.  
  

![](/assets/img/posts/spf-dkim-and-dmarc-explained/01.png)
Below we can see a breakdown of what some of the values in the DKIM signature are:

```text
v=DKIM1; k=rsa; h=sha256; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAy4V3QZgjpUK3HSijzU+uGQlfBx8N40Ese/TaM0P8BES/kTKJS7OvtEfmA+ihMYcwh+vpvjK7aBIpV2CT49QnC/lXm8KwXad64VF18pgaCiuOW4rxC2L687Gn2BHEekcbl5FozRa716DLXpo07j5IX5sdvKPi6KylnmyOmjD/NqfvbLZf/lRlTb9pXf1N3fLu+W25vaotR4ZQpbrMQkKIANDafdL4KvPmfFOfYuZYiLpQfHfuJYok0aROsS5as1cEthN9MnkdSBAJHLG/f63+jNLgSC9x77YBWH2gPIDIqEanPVPFPJjs0yNh1zCWJUma9ihNXNwBP9GDclt042thAwIDAQAB
```

| Tag | TagValue | Name | Description |
| --- | --- | --- | --- |
| v | DKIM1 | Version | Identifies the record retrieved as a DKIM record. It must be the first tag in the record. |
| k | rsa (Length: 2048 bits) | Key Type | The type of the key used by tag (p). |
| h | sha256 | Hash Algorithms | A colon-separated list of hash algorithms that might be used. |
| p | MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAy4V3QZgjpUK3HSijzU+uGQlfBx8N40Ese/TaM0P8BES/kTKJS7OvtEfmA+ihMYcwh+vpvjK7aBIpV2CT49QnC/lXm8KwXad64VF18pgaCiuOW4rxC2L687Gn2BHEekcbl5FozRa716DLXpo07j5IX5sdvKPi6KylnmyOmjD/NqfvbLZf/lRlTb9pXf1N3fLu+W25vaotR4ZQpbrMQkKIANDafdL4KvPmfFOfYuZYiLpQfHfuJYok0aROsS5as1cEthN9MnkdSBAJHLG/f63+jNLgSC9x77YBWH2gPIDIqEanPVPFPJjs0yNh1zCWJUma9ihNXNwBP9GDclt042thAwIDAQAB | Public Key | The syntax and semantics of this tag value before being encoded in base64 are defined by the (k) tag. |

One not mentioned in the table above is the d tag. d indicates the domain that is checked for record of the public key (in our example, email.apple.com).

Another piece not mentioned is the s tag. s indicates the selector that is used in combination with tag d (remember, the domain) to locate the public key. In or example it is email0517. This can be changed and made almost any custom value an administrator wants. Selectors are beneficial in the event multiple public/private key pairs are used and you want some emails to be sent using key1 versus key2. Another benefit is easier key rotation -- in the event of compromise of key1, key2 can be used for all emails while key1 is decommissioned and replaced with another key.

DKIM is great for what it does and as we've seen provides additional benefits over just using SPF alone. However, DKIM also just looks at the envelope sender/MAILFROM address which isn't presented to the user. This means that someone can create a phishing email that passes both SPF and DKIM perfectly fine, but also spoofs your company's domain in the letter sender/FROM field (the FROM field you see when you open an email).

Thankfully those that send phishing emails *usually* don't go to the trouble of setting all that up. If they do, that's where DMARC comes in.

## DMARC - Domain-based Message Authentication, Reporting & Conformance

While not an email authentication protocol, DMARC builds on top of SPF and DKIM. Without enabling at least one of them first you cannot use DMARC. DMARC also has its own policy to be published in DNS which instructs email servers on what to do if SPF or DKIM fail. An even better feature of DMARC in my opinion that often goes unmentioned, is that it checks against the FROM sender unlike SPF and DKIM.

Let's run through our example from email.apple.com to see what DMARC does:

1. Apple sends their email to Google's email server. Apple has all the necessary SPF, DKIM, and DMARC DNS records published.
2. Google's email server receives the email from Apple and runs through the SPF and DKIM checks.
3. Google's email server now checks DMARC. It does this by:

- Looks up the DMARC policy of the letter sender / FROM domain (remember this is the one users can see in the email).
- Verifies if DKIM passed.
- Verifies if SPF passed.
- Verifies if the domain in the letter sender / FROM field "aligns" with the domains that SPF and DKIM check. In other words, does the sending email address that's visible to the user match the email address in DKIM's (d) parameter and SPF's envelope sender/MAIL FROM.

4. Apple's email passes SPF, DKIM, and DMARC checks so Google's email server passes the email along to the end user.

This is how email should flow in a relatively simple case. We'll look at what happens if things go wrong in just a bit.

![](/assets/img/posts/spf-dkim-and-dmarc-explained/02.png)
Just like SPF and DKIM, you can view the header of an email to see if DMARC passed or failed, along with additional detail about the domain's DMARC policy.

Details that aren't available in the email header but are available using MxToolbox's DMARC tool are shown in the table above.

```text
v=DMARC1; p=reject; rua=mailto:d@rua.agari.com; ruf=mailto:d@ruf.agari.com;
```

| Tag | TagValue | Name | Description |
| --- | --- | --- | --- |
| v | DMARC1 | Version | Identifies the record retrieved as a DMARC record. It must be the first tag in the list. |
| p | reject | Policy | Policy to apply to email that fails the DMARC test. Valid values can be 'none', 'quarantine', or 'reject'. |
| rua | mailto:d@rua.agari.com | Receivers | Addresses to which aggregate feedback is to be sent. Comma separated plain-text list of DMARC URIs. |
| ruf | mailto:d@ruf.agari.com | Forensic Receivers | Addresses to which message-specific failure information is to be reported. Comma separated plain-text list of DMARC URIs. |

Looking again at our example of email.apple.com we can see that Apple has set a policy (p) of REJECT. They have also set their subdomain policy (sp) to REJECT. When a subdomain policy is present it take precedence over the domain policy. Other possible values for these policies are NONE (do nothing) and QUARANTINE (spam folder of the email server or end user, depending on email server).

If Google's email server determined that SPF, DKIM, or DMARC validation failed it would look at the policy published in Apple's DNS server and take that action. An important note on the logic of this policy evaluation:

DMARC only cares if SPF **OR** DKIM pass. If one fails and the other passes, DMARC considers this a pass. That being said, DMARC can still fail if the domain fails "alignment".

## Summary

SPF, DKIM, and DMARC are great additions to RFC 733 and are extremely useful tools in verifying the legitimacy of emails. They're one of the first things I check when [detecting phishing emails](/posts/detecting-phishing-emails/).

If you have any questions or want me to cover any specifics of SPF, DKIM, or DMARC let me know!