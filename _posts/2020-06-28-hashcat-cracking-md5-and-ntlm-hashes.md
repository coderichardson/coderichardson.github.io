---
title: "Hashcat - Cracking MD5 and NTLM Hashes"
date: 2020-06-28 20:44:00 +0000
tags:
  - "Passwords"
  - "Hacking"
  - "Linux"
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

![using a wordlist to crack md5 hashes](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjCsAV4Vm6_KM58GUytjWixFw2rcpDi7uF9hDY2i4PTe7jM-rnAstWPqA9nHS4VQSwLZ6DRudkVqQC0yQ3zQydG2dqlCjge6d1HfF71pk2Q8QUrB0hsF2hv7mLlR5D9Ab8KURYHFNkZ2U8D/w781-h194/1.png)

*using a wordlist to crack md5 hashes*

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

![secure_passwords.txt successfully cracked using rockyou.txt wordlist](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi7CHvI3ckJ0z_F8hFnxFdyf3J1HI1q62Wzh0gzgvmUQ7FErgaWb1HR1lYzrxShqS_vWgEm6Q0tU0m-NfPOCCAv-g0PFvjDkvRqbizMcBgK-v8PXdgZdZqcO_vjo3RgP2QYhg1DFQh_IwFU/w781-h536/2.png)

*secure_passwords.txt successfully cracked using rockyou.txt wordlist*

After some time, Hashcat successfully cracked the MD5 hashes!

Now let's see the contents of the generated cracked\_secrets.txt.

![contents of cracked_secrets.txt](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjnIAi04XXyMc8a6zCmwSKbrRLZbQVfWYwM_P-sbNB1uQR3p_PTVlrOMcu03WsHFl1mXKKCTGkqkjRsREldLGr6eYIzKr7i5HdTsqj33KXERN5wQHdxyWJVEdw9ynXLSwY40nC_vrIQWT98/w625-h568/3.png)

*contents of cracked_secrets.txt*

There are the plain-text passwords along with their MD5 hashes!

For the sake of simplicity and clarity if you're following along, subsequent sections will use the same passwords but different hashing algorithms. Since different hashing algorithms will be used, you shouldn't have to clear your potfile, but this is where it's located in case you have a need (~/.hashcat/hashcat.potfile). For example, if repeating these tests you'll want to clear this file between tests (otherwise your cracking results will be instantaneous since Hashcat already has these passwords cracked).

![clear the contents of ~/.hashcat/hashcat.potfile](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg6L6hxgzQWX3u6Foiw3qV7A7HBzw79yxm7JMjdbDsL5yKF0AlRiW1egtyWUwQKstzX-cQ6wtNVVsUZWlNAGPDN2s7djPchfMeKyNqC5Kq-yeLXXuWQmDS0tQtcht9juWskM3JyqOmDRZUj/w625-h255/clear_potfile.png)

*clear the contents of ~/.hashcat/hashcat.potfile*

## Cracking NTLM Hashes Using rockyou.txt Wordlist

Now let's repeat the process with a more commonly found hash (MD5 and SHA-1 are both considered insecure at this point and have largely been replaced with SHA-256) -- NTLM.

Here we have the contents on the secure\_passwords\_ntlm.txt file which we'll be trying to crack.

![contents of secure_passwords_ntlm.txt](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgmWuJ4qDfRDxTmjY4O9Gsp_Y1NW5GZ7lW-oq2kbUKhRIP3NhPws9V-f3Jdrmbix2NvTIk_T2drw0rd9z6tV0XZOcY3u8ak2zKwE1BQT9J2PexUzHjt_LNTeDffEhkN0tEv5jJ6L-YJ_FmZ/w625-h489/secure_passwords_ntlm.png)

*contents of secure_passwords_ntlm.txt*

We'll use the same command as we did for the MD5 hashes, but we will swap the -m 0 for -m 1000. We'll also need specify the different text files.

```bash
hashcat -m 1000 -a 0 -o /home/cody/Desktop/cracked_secrets_ntlm.txt /home/cody/Desktop/secure_passwords_ntlm.txt /usr/share/wordlists/rockyou.txt
```

![using a wordlist to crack ntlm hashes](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEioxLIfVzWmzISeN4itzrQKAUa47Flx8QvRoRbDoGsMljnhCZ62YZQoBoPAR11wzwkOb-t6YzCaR_xLelOTbzRVwV0Y2KIlstYrSskXmgjdgdZ1Wl1iwIC6zjBPBtXD6Qu7Kut5AeX2meBe/w781-h291/4.png)

*using a wordlist to crack ntlm hashes*

We can see that the NTLM hashes were also successfully cracked! This a perfect example of why [everyone should use a secure password](https://blog.codyrichardson.io/2019/11/account-security-psa.html).

![secure_passwords_ntlm.txt successfully cracked using rockyou.txt wordlist](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg3OFzKMVGqmtIBXTOL7CVTGMn6SngzUNAxt8tnT-0U2U-Bn4O4PX2C-qytzbxepQUw2YN0P43_C8VwWeTUDwajbn8cEB3iZTc9NyG8Joq-oILfbBxPXbfSxa6D3iPyOSpiSzqATCR5jZut/w781-h524/ntlm_cracked.png)

*secure_passwords_ntlm.txt successfully cracked using rockyou.txt wordlist*

The contents of cracked\_secrets\_ntlm.txt. Again, these are the same passwords used in the MD5 hash listing, but the hashes are different as expected.

![contents of cracked_secrets_ntlm.txt](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhIoPlYypuJF1utBeoJzpGRZsql1StI2knhoYZN3cPJFxOUCtHh3NwacF3TXD1TMluKnVKeKo8uA-T6KX-Evm9Jgu6GFYtRiRe_7T4L0mvBX7CT7c63SYAQaXIDYjXlUeLx8lkEAIGgiVPF/w781-h361/ntlm_cracked_secrets.png)

*contents of cracked_secrets_ntlm.txt*

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

  

![using a mask to crack NTLM hashes](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgzYRQ8zQvxZCPG__bKmaS96DNqz2WaY5UsKQNOuo_XI99BcWjpbjzv3fIGiIk8N-4UpXtebfUUDsiZ-FCHw9l-1oWlfJcwj6SSXsP_fy1KQWOE1mLhQlY7i0E2HS5jelik7hmx9Av1Df0T/w781-h286/mask_attack.png)

*using a mask to crack NTLM hashes*

The mask attack took slightly longer than the wordlist attack (as expected), but not much. Granted our password wasn't secure by any standard. We can see below the status of Cracked, along with other information including the mask used.

![secure_passwords_ntlm_mask.txt successfully cracked using mask](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgg1A9nymcYWP0FuJ6MKObBRjdB3ljBFr8fxYW-_tEVXhE_ERbNovPL0cL7RCo1JHFmg2T7bye-QpqlU5_775MikYvXk-fpjXR-9aluqGh3RqddzSH9Ui8Sk7_girh2rGkRH-ohTfiD1Jxc/w781-h489/mask_attack_results.png)

*secure_passwords_ntlm_mask.txt successfully cracked using mask*

Here we can see the contents of the cracked\_secrets\_ntlm\_mask.txt contains the NTLM hash and the corresponding plaintext password.

![contents of cracked_secrets_ntlm_mask.txt](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgDceq-KYZD4NsSLb_j5nuAYXse58JgsswfYq4XihqwLGCZ0Df8W-zXT88VptbaSME7u0l0dBHN0lsZnVPh3rU-3b8jtP8jBL0Toa17ohMZpR0e4ubBoydnoKhxyuBDAVSwxIwp55OQqFvy/w625-h166/cracked_secrets_ntlm_mask.png)

*contents of cracked_secrets_ntlm_mask.txt*

What we've done here just scratches the surface of Hashcat, and I'd like to do another write-up at some point regarding more advanced features. Maybe put my RTX 2070 SUPER to the test on passwords more secure than potat0! If there's anything specific you'd like to see let me know in the comment section below.