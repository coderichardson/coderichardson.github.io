---
title: "Hashcat - Cracking MD5 and NTLM Hashes"
date: 2020-06-28 20:44:00 +0000
tags:
  - "Passwords"
  - "Hacking"
---

Today we'll be exploring [Hashcat](https://hashcat.net/hashcat/) -- "the world’s fastest and most advanced password recovery utility". This, along with similar tools, should be used only for password recovery, pentest engagements, CTFs, etc and never for illegal purposes.

I could write an entire series about the capabilities Hashcat provides, but we will cover a few basic examples for now ([besides, Hashcat does a pretty good job of that themselves](https://hashcat.net/wiki/)):

1. Crack MD5 hashes using the rockyou.txt wordlist.
2. Crack NTLM hashes using the rockyou.txt wordlist.
3. Crack NTLM hashes using a mask attack (modified brute force).

## I'll be using Kali Linux as Hashcat comes pre-installed, but Hashcat can run on Windows, macOS, and other Linux distributions as well.

As you'll see, I'll be using some lists of hashes I made previously. Tools to generate hashes using dozens of algorithms are available online -- just save the output as a text file if you want to follow along.

## Cracking MD5 Hashes Using rockyou.txt Wordlist

I've generated a list of MD5 hashes from a list of simple passwords, and we will use Hashcat to crack this list of MD5 hashes.

|  |
| --- |
|  |
| *using a wordlist to crack md5 hashes* |

Before hitting Enter, let's break down this command:

|  |  |
| --- | --- |
| hashcat | calls the hashcat program |
| -m | specify the hash type |
| 0 | '0' after '-m' indicates a hash type of MD5 |
| -a | specify the attack mode |
| 0 | '0' after '-a' indicates an attack mode of "Straight" (wordlist) |
| -o | specify where to output results |
| /home/cody/Desktop/cracked\_secrets.txt | preceded by '-o', the file\_path+file\_name of where to store the output of the cracked hashes. |
| /home/cody/Desktop/secure\_passwords.txt | list of hashes |
| /usr/share/wordlists/rockyou.txt | full path and filename for the wordlist we are using |

Now that we know what the parameters are doing, let's press Enter.

|  |
| --- |
|  |
| *secure\_passwords.txt successfully cracked using rockyou.txt wordlist* |

After some time, Hashcat successfully cracked the MD5 hashes!

Now let's see the contents of the generated cracked\_secrets.txt.

|  |
| --- |
|  |
| *contents of cracked\_secrets.txt* |

There are the plain-text passwords along with their MD5 hashes!

For the sake of simplicity and clarity if you're following along, subsequent sections will use the same passwords but different hashing algorithms. Since different hashing algorithms will be used, you shouldn't have to clear your potfile, but this is where it's located in case you have a need (~/.hashcat/hashcat.potfile). For example, if repeating these tests you'll want to clear this file between tests (otherwise your cracking results will be instantaneous since Hashcat already has these passwords cracked).

|  |
| --- |
|  |
| *clear the contents of ~/.hashcat/hashcat.potfile* |

## Cracking NTLM Hashes Using rockyou.txt Wordlist

Now let's repeat the process with a more commonly found hash (MD5 and SHA-1 are both considered insecure at this point and have largely been replaced with SHA-256) -- NTLM.

Here we have the contents on the secure\_passwords\_ntlm.txt file which we'll be trying to crack.

|  |
| --- |
|  |
| *contents of secure\_passwords\_ntlm.txt* |

We'll use the same command as we did for the MD5 hashes, but we will swap the -m 0 for -m 1000. We'll also need specify the different text files.

```bash
hashcat -m 1000 -a 0 -o /home/cody/Desktop/cracked_secrets_ntlm.txt /home/cody/Desktop/secure_passwords_ntlm.txt /usr/share/wordlists/rockyou.txt
```

|  |
| --- |
|  |
| *using a wordlist to crack ntlm hashes* |

We can see that the NTLM hashes were also successfully cracked! This a perfect example of why [everyone should use a secure password](https://blog.codyrichardson.io/2019/11/account-security-psa.html).

|  |
| --- |
|  |
| *secure\_passwords\_ntlm.txt successfully cracked using rockyou.txt wordlist* |

The contents of cracked\_secrets\_ntlm.txt. Again, these are the same passwords used in the MD5 hash listing, but the hashes are different as expected.

|  |
| --- |
|  |
| *contents of cracked\_secrets\_ntlm.txt* |

## Cracking NTLM Hashes Using Mask (Modified Brute-Force)

Now onto what makes Hashcat unique -- mask attacks. Specifically, mask attacks that are much faster than traditional brute-force attacks (due to intelligent guessing and providing a framework for hashcat to use -- [you can read more about this at the Hashcat website](https://hashcat.net/wiki/doku.php?id=mask_attack)) and they utilize your GPU instead of your CPU.

For this example I've trimmed the secure\_passwords file down to one NTLM hash.

The syntax here is slightly different from when we use a wordlist, but the core of it is the same. I've highlighted the changed areas (other than file names) below in red:

```bash
hashcat -m 1000 -a 1000 -o /home/cody/Desktop/cracked_secrets_ntlm_mask.txt /home/cody/Desktop/secure_passwords_ntlm_mask.txt ?l?l?l?l?l?d
```

The ?l and ?d used are representative of character sets:

- ?l = abcdefghijklmnopqrstuvwxyz
- ?u = ABCDEFGHIJKLMNOPQRSTUVWXYZ
- ?d = 0123456789
- ?h = 0123456789abcdef
- ?H = 0123456789ABCDEF
- ?s = «space»!"#$%&'()\*+,-./:;<=>?@[\]^\_`{|}~
- ?a = ?l?u?d?s
- ?b = 0x00 - 0xff

So what our command breaks down to is that we are guessing for a password that is 6 characters long -- 5 lower case characters followed by 1 number. This drastically reduces the amount of time required to crack the hash. Adding any amount of "unknown" to this process (password length, password complexity, or both) increases the amount of time it will take to crack the hash.

  

|  |
| --- |
|  |
| *using a mask to crack NTLM hashes* |

The mask attack took slightly longer than the wordlist attack (as expected), but not much. Granted our password wasn't secure by any standard. We can see below the status of Cracked, along with other information including the mask used.

|  |
| --- |
|  |
| *secure\_passwords\_ntlm\_mask.txt successfully cracked using mask* |

Here we can see the contents of the cracked\_secrets\_ntlm\_mask.txt contains the NTLM hash and the corresponding plaintext password.

|  |
| --- |
|  |
| *contents of cracked\_secrets\_ntlm\_mask.txt* |

What we've done here just scratches the surface of Hashcat, and I'd like to do another write-up at some point regarding more advanced features. Maybe put my RTX 2070 SUPER to the test on passwords more secure than potat0! If there's anything specific you'd like to see let me know in the comment section below.