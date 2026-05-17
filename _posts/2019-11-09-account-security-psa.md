---
title: "Account Security - Making a Secure Password"
date: 2019-11-09 19:43:00 +0000
tags:
  - "Passwords"
  - "Authentication"
---

![Most common passwords 2018](/assets/img/posts/account-security-psa/04.jpg)

*Most common passwords 2018*

#### Making a Secure Password

If you use any of the passwords in the lists above (or anything close to them), this post is for you. Even if you think you've got a strong password I'd ask you to keep reading, as many people have the wrong idea about what makes up a strong password.

It's been stated for years to use capital letters, numbers, special characters, and not your pet's name as a password. This is true for Facebook logins, company domain logins, and even bank account logins. I believe it's simply human nature -- we're given a set of requirements with the expectation that if we follow them then our password is secure. Then we create the easiest, most memorable passwords that meet those requirements and don't think twice about it believing we're all set. While not on the "top 15 most common" list, what usually results from these requirements is something like "FacebookPassword123!" or worse "Password1" if the site's requirements are especially lacking.

This is a recipe for disaster and why so many people's accounts are compromised on a daily basis (database dumps containing millions of records of usernames and passwords don't help either). So what actually is a good password?

I completely agree with Troy Hunt in that the [only secure password is the one you can't remember](https://www.troyhunt.com/only-secure-password-is-one-you-cant/). For 99% of your passwords, I recommend a password manager. [Paid](https://1password.com/) or [free](https://pwsafe.org/), it doesn't matter (as long as strong encryption methods are used). You can then have your password manager randomly generate a 32 character password for you that you don't have to worry about remembering. The only passwords you will have to remember are your computer login and the master password to your password safe.

![](/assets/img/posts/account-security-psa/01.png)

![](/assets/img/posts/account-security-psa/03.png)

  
  
So what about the passwords we do have to remember? Or if you choose not to put your online banking information or some other login in your password safe? The [latest NIST Guidelines](https://blog.24by7security.com/unpacking-the-nist-password-requirements-in-2019) do a pretty good job with minimum recommendations, though I think the 8 character minimum should be increased.   

The major takeaway I like to emphasize is the concept of pass **phrases**. A pass phrase is a series of words such as "John Baked 1 Cake For The Party!". 32 characters, easy to remember, and good luck cracking it in any reasonable amount of time. Most operating systems support the use of spaces in account passwords, and every password manager I've ever used does the same.

There is no reason not to take advantage of this and make your accounts exponentially more secure.

![XKCD password strength](/assets/img/posts/account-security-psa/05.png)

*[XKCD](https://xkcd.com/936/)*

#### Multi-Factor Authentication

A password -- something you know -- is a single factor of authentication. You present your identity (username) and then provide the password to gain access. This is true even if your phone is reading your fingerprint instead -- your account still has a password you could enter if your fingerprint reader  broke. As a second step of verification you can request that a text message be sent to you, or that you need to enter a code given by an authentication app. Having just the code or just the password to the account will not work, you need both. This is multi-factor authentication.

While far from perfect ([SIM swaps](https://www.zdnet.com/article/sim-swap-horror-story-ive-lost-decades-of-data-and-google-wont-lift-a-finger/), [Social Engineering](https://cyware.com/news/attackers-using-social-engineering-to-bypass-multi-factor-authentication-the-fbi-warns-6075a438), etc), multi-factor authentication significantly reduces the chance that your account will be compromised. If a service offers it, enable it. If a service offers both the ability to use an app and SMS for MFA, choose the app ([Google Authenticator](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2&hl=en_US), [Authy](https://play.google.com/store/apps/details?id=com.authy.authy&hl=en_US)). Finally, TwoFactorAuth [has a great site](https://twofactorauth.org/) that compares services' multi-factor offerings.

![](/assets/img/posts/account-security-psa/02.png)
I've only scratched the surface of these topics with what's written here, but these are some of the most important points to make and will make the biggest difference for the least amount of effort.