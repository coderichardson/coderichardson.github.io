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

![](/assets/img/posts/linux-key-based-authentication/01.png)
You'll then be asked where to save the key pair. I'd recommend sticking with the home directory of the user account you intend to login to -- just make sure permissions on your home directory are secure! This is followed by overwriting any existing id\_rsa file present (and therefore not being able to authenticate with that key anymore if overwritten), and an optional password which encrypts the private key.

![](/assets/img/posts/linux-key-based-authentication/02.png)
Let's confirm the presence of the keys in ~/.ssh by listing the contents of that directory using ls -l ~/.ssh.

![](/assets/img/posts/linux-key-based-authentication/03.png)
And now we see them there!

## Transfer and Add Public Key to Remote Server

There are several ways of going about moving your public key to the remote server, but today we will use ssh-copy-id.

Type ssh-copy-id <username>@<hostname/IP> and press **Enter**. Yes, it really is that easy. You'll be prompted to confirm you trust the fingerprint of the host. Confirm this by typing yes and pressing **Enter**.

![](/assets/img/posts/linux-key-based-authentication/04.png)
You'll be prompted to enter your password -- this is the password of the account on the remote machine. Once successful the the key will be added to the appropriate directory and file on the remote server.

![](/assets/img/posts/linux-key-based-authentication/05.png)
Let's verify on the server that the authorized\_keys file is now present under the home directory of the remote user by again entering ls -l ~/.ssh.

![](/assets/img/posts/linux-key-based-authentication/06.png)
And there it is! Again, this is a copy of the *public* key we created back on the client. Note that the timestamp difference between it appearing here and me originally creating the key is only because this blog post was not done all in one evening. 😀

Finally, this is just one method to transfer the key to the remote server. You can use scp, copy-and-paste to append to an existing authorized\_keys file via a terminal window, or any other secure method.

## Login Remotely! (Verifying Configuration)

Let's give it a go: ssh cody@10.0.2.5 (the IP address of the server I'm working with).

![](/assets/img/posts/linux-key-based-authentication/07.png)
And we're authenticated! Notice the change from cody@client to cody@server without any prompt for a password.

If you run into issues at this step verify your permissions on the .ssh directory as well as the authorized\_keys file. They should be 700 (rwx------) and 600 (-rw------) respectively.

Finally, once confident in this system in your environment, consider disabling password-based logins entirely.

Feel free to comment or reach out with any questions!

### Additional Reading

- How to Configure SSH Key-Based Authentication on a Linux Server - <https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server>
- Configuring Passwordless Server Login Using SSH (EngineerMan) - <https://www.youtube.com/watch?v=tRJBC9rWH3A&t=>