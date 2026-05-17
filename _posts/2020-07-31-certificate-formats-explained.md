---
title: "Certificate Format Basics"
date: 2020-07-31 23:38:00 +0000
tags:
  - "Certificates"
  - "TLS/SSL"
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhNZsASEkKxA2il2rbh7dOd-juIS4Fp-Z1JqL1xrP54MYkliAX34JKrQxhsqfrw7Yin7bGV6_fuk5QMUHXYFq1aGEN3bYg8n3cKxBUz97_MpdEQo8BpDofEliIQHfJI8xMmU_OYrUzUiQ6B/w500-h411/TLS_SSL+Certificate+Formats+-+Diagram.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhNZsASEkKxA2il2rbh7dOd-juIS4Fp-Z1JqL1xrP54MYkliAX34JKrQxhsqfrw7Yin7bGV6_fuk5QMUHXYFq1aGEN3bYg8n3cKxBUz97_MpdEQo8BpDofEliIQHfJI8xMmU_OYrUzUiQ6B/s478/TLS_SSL+Certificate+Formats+-+Diagram.png)

Certificates are amazing. They are all standardized, there's a single, universal, secure format that most everyone uses, just about anyone can manage them, and a single validation failure in a chain can no longer cause production outages.

Now that the jokes are out of the way, if you're anything like me you find it difficult to keep track of the certificate formats, how they're encoded, which formats allow for the private key to be included and which don't, why exactly I need to use one format of certificate on this box but it needs to be converted before I put it on Windows, etc. But certificates actually play a vital role in security and they're important to understand.

I won't be covering all certificate formats today, but I'll cover several -- including the most common ones and what differentiates them from other certificate formats. Note I define certificate *format* as the defined formatting of the certificate (defined in an RFC or otherwise), and certificate *type* as describing a certificate's use. [Here is a great breakdown](https://www.sslshopper.com/special-ssl-certificate-types.html) on the different certificate types. If you have questions about something not covered here feel free to comment below and I'll do my best to answer.

#### .pem

This is one of the most powerful certificate formats as a single .pem file can contain your entire certificate chain and key pair! That is your root, intermediate, and primary/domain certificate, csr, and key-pair all in one!

The easiest way to remember what makes PEM different is that it's really just a file with base64 encoded data that can represent up to and including everything you need / obtain from your CA for your certificate chain to be complete. Or you may find just a couple of the items in the chain. Only way to know what's in it is open it and find out.

|  |
| --- |
| [.pem example](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhfrB10PaO1qcdxytSHCXh3Nd8lisUnQqLBkTXF9hMcpKRah5Tt9r-w5mjos6baWkYWLM8z9nkRPkImeZKhHNq_H_TITQBrqkJ1cJNxLNGMtFetBmJjtrdYDI81GuGVQ6YhPIdBwgR9ICVj/s584/pem-example.png) |
| .pem example (certificate + csr) |

#### .cer / .cert / .crt

See **.pem** above. Windows just recognizes this as a certificate while it does not recognize .pem.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj751ZswRxmRCwSMb3a6EYnIPyV8Y90vtTlBxaYDVpAsdZFtBHVrPfZy-cGd3V1ZkaFEG4wuVeX7Z62syO2imfci2KaKp1AGYkIbjYkqirpPJE37HBdDEB0ch6nAQeXF-cvtCpci5jlYYFk/s0/windows_recognizes_this.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj751ZswRxmRCwSMb3a6EYnIPyV8Y90vtTlBxaYDVpAsdZFtBHVrPfZy-cGd3V1ZkaFEG4wuVeX7Z62syO2imfci2KaKp1AGYkIbjYkqirpPJE37HBdDEB0ch6nAQeXF-cvtCpci5jlYYFk/s173/windows_recognizes_this.png)

#### .p7b / .p7c

Also Base64 encoded, this format is recognized by several platforms. While out of the scope of this post, the RFCs they're based on define the actual format/standard ([PKCS#7](https://tools.ietf.org/html/rfc2315) and [CMS](https://tools.ietf.org/html/rfc5652)). These can contain varying numbers and types of certificates (root, intermediate, etc.) but will never include the private key.

#### .pfx / .p12

The '12th' standard in PKCS (Public Key Cryptography Standards). These formats are password protected and encrypted by symmetric key. PFX is the predecessor to PKCS#12. These can contain all certificates in the chain as well as the private key. OpenSSL can conveniently convert these certificate formats to a .pem to split out if desired.

#### Additional Reading

I'd encourage reading up on the RFCs surrounding PKCS#7, PKCS#12, and others (maybe other blog posts or articles explaining the RFCs...they can get dry at times).

While some of the knowledge above is due to experience, much of it is due to reading, watching videos, and experimenting with OpenSSL. In no particular order, here are some reference links you may find useful:

- <https://www.thesslstore.com/blog/how-to-convert-a-certificate-to-the-correct-format/#:~:text=509%20digital%20certificate%20encoded%20in,!)%20is%20represented%20as%20ASCII.>
- <https://serverfault.com/questions/9708/what-is-a-pem-file-and-how-does-it-differ-from-other-openssl-generated-key-file>
- <https://en.wikipedia.org/wiki/PKCS>
- <https://crypto.stackexchange.com/questions/37084/is-pkcs7-a-signature-format-or-a-certificate-format>
- <https://tools.ietf.org/html/rfc1424>
- <https://tools.ietf.org/html/rfc7292>
- <https://tools.ietf.org/html/rfc2315>