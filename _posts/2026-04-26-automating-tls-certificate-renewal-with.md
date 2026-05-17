---
title: "Automating TLS Certificate Renewal with Certbot"
date: 2026-04-26 01:27:00 +0000
tags:
  - "TLS/SSL"
  - "Certificates"
  - "Linux"
  - "Cybersecurity"
---

![](/assets/img/posts/automating-tls-certificate-renewal-with/01.png)
[Certification Authority Browser Forum (CA/Browser Forum)](https://cabforum.org/) is "a voluntary gathering of Certificate Issuers and suppliers of Internet browser software and other applications that use certificates (Certificate Consumers)." This group has determined that SSL/TLS certificates will soon be required to expire every 47 days (or less). Compared to the industry standards of even a few years ago, this is a significant change in requirements.   
  

**[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhQLttnvJs8SVGXx1ijjW_28Zf3dI4_fOVVbrpFUm1vnrbmHS50FKfuWN-UvGU3JWyMSeBqiwy_viMn20fkIrEWYR033qKQCOjy7fS51NZt_-ry2MQTatSHbAz0opIIsX1H8kRefMPAPJt5pc8Bu9uccubrw5lc6JU_1I870mahuT45u0plFvtqPKhrOMfq/w640-h360/tls_validity_schedule.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhQLttnvJs8SVGXx1ijjW_28Zf3dI4_fOVVbrpFUm1vnrbmHS50FKfuWN-UvGU3JWyMSeBqiwy_viMn20fkIrEWYR033qKQCOjy7fS51NZt_-ry2MQTatSHbAz0opIIsX1H8kRefMPAPJt5pc8Bu9uccubrw5lc6JU_1I870mahuT45u0plFvtqPKhrOMfq/s2720/tls_validity_schedule.png)**

Those organizations that have already deployed automated methods of certificate renewal may find this to be a minor inconvenience -- just adjust the frequency with which their automated tasks run and go about their day. For those that are used to manually renewing certificates once a year, this is a massively impacting change. This is true for small shops with a simple online presence, to moderately sized organizations with IT teams that simply did not have a need for automated certificate renewal in the past.

It is for these reasons I want to explore a basic method of implementing automated certificate renewal. Depending upon your Certificate Authority (CA), your options for automated renewal will likely look different though use similar "under-the-hood" mechanics.

Today we will be looking at using certbot for renewal automation, Let's Encrypt as our CA, and Cloudflare as our domain registrar and DNS provider. But first, let's talk about how the automation works.

### How ACME Works

ACME (Automatic Certificate Management Environment) is the protocol that Let's Encrypt and certbot use to talk to each other. At its core, ACME answers one question: "How does the CA know you actually control the domain you're requesting a cert for?" ACME has been adopted by most other vendors' certificate renewal automation processes and is the industry standard ([RFC-8555](https://datatracker.ietf.org/doc/html/rfc8555/))

I've listed the steps below that are specific to my scenario, but some implementation details can vary depending on the given circumstances. For example, the DNS TXT record validation that I use is one of [several ways that domain ownership can be validated](https://letsencrypt.org/docs/challenge-types/). This specific implementation is DNS-01 -- like all things it comes with pros and cons compared to other possible methods. That linked article from Let's Encrypt is a great resource to learn more about the other methods.

1. certbot asks Let's Encrypt for a certificate for my domain.

2. Let's Encrypt issues a challenge — essentially a secret token it expects to find in a DNS TXT record at my domain's DNS records.

3. certbot calls the Cloudflare API to create that TXT record automatically.

4. certbot tells Let's Encrypt to go check for the newly created TXT record. Let's Encrypt queries DNS, finds the expected value, and considers the challenge satisfied.

5. certbot submits a CSR (Certificate Signing Request) containing my public key and domain name.

6. Let's Encrypt signs and returns the certificate. certbot saves it to disk and cleans up the TXT record.

![](/assets/img/posts/automating-tls-certificate-renewal-with/02.png)
### DNS, Cloudflare, and API Key Setup

Since DNS plays a central role in the ACME protocol (at least in the DNS-01 validation implementation), we need to get it setup. For convenience, in my case, I registered a test domain with Cloudflare and am also choosing to control DNS with Cloudflare. These functions can be handled independently if desired.

In order to allow LetsEncrypt to issue certificates for my domain, a Certificate Authority Authorization (CAA) record must be created in DNS. Select the CAA record type and enter the certificate authority's domain (letsencrypt.org) and you are done.

![](/assets/img/posts/automating-tls-certificate-renewal-with/03.png)
This is what it looks like completed in Cloudflare.

Next is setting up an API Key. While we don't need this quite yet, it makes sense to generate while we're in Cloudflare anyway. This API Key should be scoped to just the domain we are automating with only "DNS Write" permissions.

![](/assets/img/posts/automating-tls-certificate-renewal-with/04.png)
Take note of your API key once provided and then we are done here. Time to move on to certbot!

### Installing and Configuring Certbot

It's finally time to install certbot. While I primarily work on a Windows laptop, I wanted to work through this with certbot on a Linux system as it is typically deployed in production scenarios. For this, I chose to use WSL 2 on my local laptop using Ubuntu 22.04. The steps for that are outside the scope of this post, but it is pretty straightforward if you are interested. Otherwise, a VM or separate Linux system work as well.

I chose to install certbot via snap on Ubuntu for convenience. The apt-based package would work just as well, and is usually my preference when installing software. After this came installing the plugin for Cloudflare which will allow the automated connections (via that API key we made) to update DNS records.

```bash
# Install certbot
sudo snap install --classic certbot

# Link it to PATH
sudo ln -s /snap/bin/certbot /usr/local/bin/certbot

# Install the Cloudflare DNS plugin
sudo snap install certbot-dns-cloudflare

# Connect the plugin to certbot
sudo snap connect certbot:plugin certbot-dns-cloudflare
```

Finally, a quick test to make sure the plugin shows as installed using certbot plugins

![](/assets/img/posts/automating-tls-certificate-renewal-with/05.png)
Next we need to give certbot the API key to be able to connect to Cloudflare. While other methods can and should be considered (storage in a secret vault for example), for now we are going to store the API key in a permissions-locked ini file.

```bash
# Make an associated secrets directory for certbot.
mkdir -p ~/.secrets/certbot

# Create the .ini file
vim ~/.secrets/certbot/cloudflare.ini
```

Next was to copy and paste the API key into the cloudflare.ini file and lock it down.

```text
dns_cloudflare_api_token = YOUR_TOKEN_HERE
```

```bash
# Lock the file down such that only my user account can read it.
chmod 600 ~/.secrets/certbot/cloudflare.ini
```

![](/assets/img/posts/automating-tls-certificate-renewal-with/06.png)
Now we're ready for certificate issuance and renewal.

### Certificate Issuance and Automatic Certificate Renewal

Before we setup automatic renewal, let's manually request a certificate. Run the following command to request a certificate for your domain and wildcard:

```bash
sudo certbot certonly \
  --dns-cloudflare \
  --dns-cloudflare-credentials ~/.secrets/certbot/cloudflare.ini \
  -d DOMAIN_NAME \
  -d "*.DOMAIN_NAME" \
  --email EMAIL_ADDRESS \
  --agree-tos \
  --non-interactive
```

![](/assets/img/posts/automating-tls-certificate-renewal-with/07.png)
You can see the full chain and private key saved to my system. Note that the --expand flag was used in my session because I had an existing certificate to be replaced along with a wildcard. If it's your first time running this command you won't have to include this flag.

Now for the whole point of this...automating renewal. Since we installed via snap, a timer is installed by default along with certbot. I'll check the status of my timer now.

```bash
sudo systemctl status snap.certbot.renew.timer
```

![](/assets/img/posts/automating-tls-certificate-renewal-with/08.png)
The timer runs certbot twice daily. Each run checks all certificates in /etc/letsencrypt/renewal/ and renews any that are within 30 days of expiry. Certbot generated a renewal config file for your domain when it issued the cert:

```text
/etc/letsencrypt/renewal/DOMAIN_NAME.conf
```

This file records everything certbot needs to renew unattended — the authenticator, credentials path, domains, and Let's Encrypt endpoint.

Finally, to test and confirm that automatic renewal is setup to succeed we run the following:

```bash
sudo certbot renew --dry-run
```

![](/assets/img/posts/automating-tls-certificate-renewal-with/09.png)
As soon as we see "Congratulations" at the bottom we're all set!