---
title: "Configuring SSH Key Based Authentication"
date: 2020-10-23 02:32:00 +0000
tags:
  - "Authentication"
  - "Certificates"
  - "SSH"
  - "Linux"
---

## Overview

Most personal computers and many organizations running Linux servers utilize password-based authentication. This is what most of us are used to -- you enter a username and password in order to authenticate your account and gain access to a system. While straightforward and commonplace, this isn't the best solution in most cases. Today I'll be explaining why key based authentication is more convenient, more secure, and allows for automation of tasks without saving credentials in plain-text in a text file.

Key based authentication involves the use of private and public keys ([public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography)). The private key is stored on the client and the public key is stored on the server in a special file (~/.ssh/authorized\_keys). This allows any system with the corresponding private key to login to the server where we just stored the public key.

Our steps are:

1. Generate key pair (public / private key).
2. Transfer public key and add it to the authorized\_keys file on the remote server.
3. Login remotely using a public/private key!

## Generate Key Pair

First let's run ssh-keygen to generate the public / private key pair:

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjKgeF3yjh9IUGTh_9zhAzQ6MTN_ar7RfvS2WqIuy1DYW3R-uNniyYPImLcgkcsMj8B5lCrabxFxHRR34vhHAZrHG_B9v8qhDBIf_HHqhMb0_F8Ka0MNWgGB00ScFVcKMt0oFNguelwkfWL/w400-h44/2020-10-21+21_11_40-cody%2540client_%257E.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjKgeF3yjh9IUGTh_9zhAzQ6MTN_ar7RfvS2WqIuy1DYW3R-uNniyYPImLcgkcsMj8B5lCrabxFxHRR34vhHAZrHG_B9v8qhDBIf_HHqhMb0_F8Ka0MNWgGB00ScFVcKMt0oFNguelwkfWL/s407/2020-10-21+21_11_40-cody%2540client_%257E.png)

You'll then be asked where to save the key pair. I'd recommend sticking with the home directory of the user account you intend to login to -- just make sure permissions on your home directory are secure! This is followed by overwriting any existing id\_rsa file present (and therefore not being able to authenticate with that key anymore if overwritten), and an optional password which encrypts the private key.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh74YeNPfJeiXNcLVYgN78nawGdYXgFg491cVQIBN_YTnDzFmkueSVeSlFe1HQzumZwGmUnLoKV86Raeto34B8Tov7O0cC93KrJ-ClJt70hSev3pSRH38S6S9FiVhQnXPVJFTvwX62I1yGU/w400-h319/2020-10-21+21_15_12-cody%2540client_%257E.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh74YeNPfJeiXNcLVYgN78nawGdYXgFg491cVQIBN_YTnDzFmkueSVeSlFe1HQzumZwGmUnLoKV86Raeto34B8Tov7O0cC93KrJ-ClJt70hSev3pSRH38S6S9FiVhQnXPVJFTvwX62I1yGU/s635/2020-10-21+21_15_12-cody%2540client_%257E.png)

Let's confirm the presence of the keys in ~/.ssh by listing the contents of that directory using ls -l ~/.ssh.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgtPYQxb2jjrAVi-y7rmLbRxfJJHOc-h1Yh3MxjnB24S-trOb40qmA1-zgaYDVONwXIEV3NJFIjCbEdvRztBNwtqBNUzvNx16CQr5VuVkD1C3xwVDUrLZg_P3uMexf8TYRfpu5D1CPErnno/w400-h68/2020-10-21+21_29_32-cody%2540client_%257E.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgtPYQxb2jjrAVi-y7rmLbRxfJJHOc-h1Yh3MxjnB24S-trOb40qmA1-zgaYDVONwXIEV3NJFIjCbEdvRztBNwtqBNUzvNx16CQr5VuVkD1C3xwVDUrLZg_P3uMexf8TYRfpu5D1CPErnno/s522/2020-10-21+21_29_32-cody%2540client_%257E.png)

And now we see them there!

## Transfer and Add Public Key to Remote Server

There are several ways of going about moving your public key to the remote server, but today we will use ssh-copy-id.

Type ssh-copy-id <username>@<hostname/IP> and press **Enter**. Yes, it really is that easy. You'll be prompted to confirm you trust the fingerprint of the host. Confirm this by typing yes and pressing **Enter**.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiTAUBNpLOUqbhZ211ilbBe00WeFMFzcOarPCXCC-OaK9jR2z3mUeQoT5ru-wl3V4uW7jjewHrFvplo76Soj6wpiMrPfrQOIC-CLpB2v4z_EZ9Hfe4jGyxGw5w0frH54dsKSPWd68pYfEvC/w640-h80/2020-10-22+20_26_33-Window.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiTAUBNpLOUqbhZ211ilbBe00WeFMFzcOarPCXCC-OaK9jR2z3mUeQoT5ru-wl3V4uW7jjewHrFvplo76Soj6wpiMrPfrQOIC-CLpB2v4z_EZ9Hfe4jGyxGw5w0frH54dsKSPWd68pYfEvC/s902/2020-10-22+20_26_33-Window.png)

You'll be prompted to enter your password -- this is the password of the account on the remote machine. Once successful the the key will be added to the appropriate directory and file on the remote server.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhJilhe2mhNvF9f5Mnmswvyx8fIlozogeCIvvIIb6nolVvfIh_sxsldtzPg26bQSRjXQypf2CJZAH6AU5bqNKSOXV7B6GapA-NDDaeVTtLo-_jxQO6ReAMOyxYVmoUNDd2Z1CCsnKWhNqtC/w640-h154/2020-10-22+20_33_15-Window.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhJilhe2mhNvF9f5Mnmswvyx8fIlozogeCIvvIIb6nolVvfIh_sxsldtzPg26bQSRjXQypf2CJZAH6AU5bqNKSOXV7B6GapA-NDDaeVTtLo-_jxQO6ReAMOyxYVmoUNDd2Z1CCsnKWhNqtC/s932/2020-10-22+20_33_15-Window.png)

  

Let's verify on the server that the authorized\_keys file is now present under the home directory of the remote user by again entering ls -l ~/.ssh.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiVIkda3xGAPgD1ynUJItoOA3x2H7fRFjy0QHkHCQRXryl4ecJ2pNunGvLXFojsEUJYAEbEHhfkbkOY-TP9S-Rzf7xi8SXbbAdk4Lz1V-vpRnok68Fdzju7_Gk3q_jeHGm8qKWGUvLYFES6/w400-h50/2020-10-22+20_38_44-Window.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiVIkda3xGAPgD1ynUJItoOA3x2H7fRFjy0QHkHCQRXryl4ecJ2pNunGvLXFojsEUJYAEbEHhfkbkOY-TP9S-Rzf7xi8SXbbAdk4Lz1V-vpRnok68Fdzju7_Gk3q_jeHGm8qKWGUvLYFES6/s570/2020-10-22+20_38_44-Window.png)

  
And there it is! Again, this is a copy of the *public* key we created back on the client. Note that the timestamp difference between it appearing here and me originally creating the key is only because this blog post was not done all in one evening. 😀

Finally, this is just one method to transfer the key to the remote server. You can use scp, copy-and-paste to append to an existing authorized\_keys file via a terminal window, or any other secure method.

## Login Remotely! (Verifying Configuration)

Let's give it a go: ssh cody@10.0.2.5 (the IP address of the server I'm working with).

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhWHeRUb9sZVIE1g-479XKlOxmKRsYO3Ld3kG69f1-UwDxDAy_fdt8IkVpkroxxa0gss8MkXOj61YUdgwCVP9CAtuJLIICqwKjd_MdrbSsgXfFfgigLkkamulsdOxBtb_aFIWMODqPL1Cky/w640-h112/2020-10-22+20_37_50-Window.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhWHeRUb9sZVIE1g-479XKlOxmKRsYO3Ld3kG69f1-UwDxDAy_fdt8IkVpkroxxa0gss8MkXOj61YUdgwCVP9CAtuJLIICqwKjd_MdrbSsgXfFfgigLkkamulsdOxBtb_aFIWMODqPL1Cky/s694/2020-10-22+20_37_50-Window.png)

  

And we're authenticated! Notice the change from cody@client to cody@server without any prompt for a password.

If you run into issues at this step verify your permissions on the .ssh directory as well as the authorized\_keys file. They should be 700 (rwx------) and 600 (-rw------) respectively.

Finally, once confident in this system in your environment, consider disabling password-based logins entirely.

Feel free to comment or reach out with any questions!

### Additional Reading

- How to Configure SSH Key-Based Authentication on a Linux Server - <https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server>
- Configuring Passwordless Server Login Using SSH (EngineerMan) - <https://www.youtube.com/watch?v=tRJBC9rWH3A&t=>