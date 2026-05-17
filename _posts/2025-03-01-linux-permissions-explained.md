---
title: "Linux Permissions Explained"
date: 2025-03-01 03:22:00 +0000
tags:
  - "Linux"
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhtrT1JRZIBua59MhY8XwvkDsUGVKfzEUwy7PN9jSt47Xc5WUJ_6cgaLZ-OegCP_XX3hQaqGrxzdrIoUQJUF4XG5WCLhWlNLmwOM9oY5DhA-PEF4ksrL7cW-rQXGzlTWlw20psXppwlpK5tBi5KWYy-7qsveSkZAhnug87L9OvzahK0TDqu4xiKfGd2bk7-/w640-h360/yxNrpKJ.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhtrT1JRZIBua59MhY8XwvkDsUGVKfzEUwy7PN9jSt47Xc5WUJ_6cgaLZ-OegCP_XX3hQaqGrxzdrIoUQJUF4XG5WCLhWlNLmwOM9oY5DhA-PEF4ksrL7cW-rQXGzlTWlw20psXppwlpK5tBi5KWYy-7qsveSkZAhnug87L9OvzahK0TDqu4xiKfGd2bk7-/s1400/yxNrpKJ.png)

## Reading File Permissions

Linux file permissions are broken down by User, Group, and Others. Permissions for read, write, and execute can be associated with each entity and are displayed as rwxrwxrwx.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgqtfxm0Zewmzn9jbldNprQysB29gJVeFAkQHD5-XCXcb9YnQbrc_D7CDLyhN0ta3tUwNYd7LE31HlErH11MjKCfjfy1W-7NIH7662Z2I9P2oYhKlVRbZMpLD7SfsxW7mhUD-Ldz5RhfcxhAGIj1c-6JK6VPSVX9GQd4pqQ3wiOnzPHZdprQepNy4BmNHVb/w640-h376/2025-02-17%2020_57_30-Post_%20Edit.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgqtfxm0Zewmzn9jbldNprQysB29gJVeFAkQHD5-XCXcb9YnQbrc_D7CDLyhN0ta3tUwNYd7LE31HlErH11MjKCfjfy1W-7NIH7662Z2I9P2oYhKlVRbZMpLD7SfsxW7mhUD-Ldz5RhfcxhAGIj1c-6JK6VPSVX9GQd4pqQ3wiOnzPHZdprQepNy4BmNHVb/s2071/2025-02-17%2020_57_30-Post_%20Edit.png)

  

As an example, take **alternatives.log** -- the first entry shown in the screenshot above. The file is owned by the root user and the root group. It's permissions are set as -rw-r--r--.

The first "-" we're going to ignore for now, and we'll focus on the **rw-r--r--** section.

The can be interpreted as root (the user) can read and write this file, but not execute. Root (the group) can only read this file. Finally, others, which means anyone not the user or group, can only read the file.

Now that we can check the file permissions, what if we need to change them? First we'll change the user and group that owns the file, then we'll come back to the permissions.

## Changing File Ownership

First, any given file or directory can have the owner user and group changed (assuming the account that's wants to do the changing has permission).

This can be accomplished by using the chown command.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg2kxOClGfYxMxSF6dEuskBIRaI-bnpejmlODWRZgJimhs8LfrV0Hs3AfbcnpRKwRTuWnS4Jo18LO5q9fDel1mDVZMBaTkDQlUBSdGtEcGSPgUxVtn6I5nkamMHM3UaXVClYRtrZjygI-S5NWyJ_b-TocmWEBQYvZG-S0u64k67cSLa2KKC4-lnoQajcbp0/w640-h110/2025-02-17%2021_10_21-Post_%20Edit.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg2kxOClGfYxMxSF6dEuskBIRaI-bnpejmlODWRZgJimhs8LfrV0Hs3AfbcnpRKwRTuWnS4Jo18LO5q9fDel1mDVZMBaTkDQlUBSdGtEcGSPgUxVtn6I5nkamMHM3UaXVClYRtrZjygI-S5NWyJ_b-TocmWEBQYvZG-S0u64k67cSLa2KKC4-lnoQajcbp0/s2740/2025-02-17%2021_10_21-Post_%20Edit.png)

I've created test.txt which is currently owned by the user **cody** and the group **cody**. I'm going to login as the **root** user and change the user that owns this file to **root**.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj5IODtIRu3Gd6HwqhzziURAXRDcWVJUMw-fRdSZW40NH6_GAZzyBs77O9iw44XjTNLZunPD3GqePzKt7YVy1lakZ6ByS_XAJUIuUbUjHwyNMNqJMhjuQi0oUp5wjnBrkPBBP6wAjoJ0gnruAUlupl2LR7HnrE4AlZRO7JgMDF0dBjjXJfHlv3fE5WDZ22e/w640-h120/2025-02-17%2021_13_03-Post_%20Edit.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj5IODtIRu3Gd6HwqhzziURAXRDcWVJUMw-fRdSZW40NH6_GAZzyBs77O9iw44XjTNLZunPD3GqePzKt7YVy1lakZ6ByS_XAJUIuUbUjHwyNMNqJMhjuQi0oUp5wjnBrkPBBP6wAjoJ0gnruAUlupl2LR7HnrE4AlZRO7JgMDF0dBjjXJfHlv3fE5WDZ22e/s2722/2025-02-17%2021_13_03-Post_%20Edit.png)

By running chown root test.txt the user that owns test.txt is now root, while the group is still **cody**. Alternatively, I could have run the command sudo chown root test.txt as the user **cody**, but I chose to login as the **root** user instead.

To change the group owner of the file you also use the chown command but instead in the following manner:

```bash
chown :newgroup filename
```

## Changing File Permissions

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhV44-6lqEKCJ__cS8rBaadIrGWJ3bGcl1F6Ja-zTBJwNj_MHtk7DK9nabBeL_V97gO9ne0qRwuzDy-sahm5VH_kSjja3THx6jsEV58jReWgoNoheaMnyAOJQz0rUJY1V7aC7N6MXroG7nEX63kAle9Q3ptRyIM-bXfXKOBcG40TGeUOaNGFQ3GM4IwTpFJ/w640-h112/2025-02-17%2021_26_52-Post_%20Edit.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhV44-6lqEKCJ__cS8rBaadIrGWJ3bGcl1F6Ja-zTBJwNj_MHtk7DK9nabBeL_V97gO9ne0qRwuzDy-sahm5VH_kSjja3THx6jsEV58jReWgoNoheaMnyAOJQz0rUJY1V7aC7N6MXroG7nEX63kAle9Q3ptRyIM-bXfXKOBcG40TGeUOaNGFQ3GM4IwTpFJ/s2721/2025-02-17%2021_26_52-Post_%20Edit.png)

  

We'll continue using the files under /var/tmp for now, but the same principles apply anywhere in the Linux filesystem.

Looking at test.txt as before, we see rw-r--r-- as the current file permissions. To change that, we have two options:

- Symbolic Mode
- Numeric Mode

### Symbolic Mode

Symbolic mode allows you to edit file permissions by specifying the user, group, or others, and then adding or removing the desired permissions. This is accomplished using the chmod command. For example:

```bash
chmod u+x test.txt  # adds execute permissions for the user
chmod g-r test.txt  # removes group permissions for the group
```

The same result can also be accomplished the following syntax:

```bash
chmod u=rwx,go= test.txt
```

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgzlbsdQOcMxBMDK9GhX3iDrkKKJ9lapA4h5_-NdFAHM8yQVWm2Af1ijQAD-NIQLhiMIsC1A3jWqp1uEhy9Cjmxg7sI0rE3dpEseR0etTQFo5P93UnpfqcpD_qnUVfda5Y_-Ee9tdDWpq-NkqeXzuBKOk0RfUC4tvs1Qton4gNlKe2CD2g_08ZFZkvKHRxv/w640-h342/2025-02-19%2019_39_38-cody@CR-LENOVO_%20_var_tmp.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgzlbsdQOcMxBMDK9GhX3iDrkKKJ9lapA4h5_-NdFAHM8yQVWm2Af1ijQAD-NIQLhiMIsC1A3jWqp1uEhy9Cjmxg7sI0rE3dpEseR0etTQFo5P93UnpfqcpD_qnUVfda5Y_-Ee9tdDWpq-NkqeXzuBKOk0RfUC4tvs1Qton4gNlKe2CD2g_08ZFZkvKHRxv/s2849/2025-02-19%2019_39_38-cody@CR-LENOVO_%20_var_tmp.png)

The benefit of modifying permissions this way is that there is no mistaking what permissions are being applied as the corresponding letters are present in the command.

### Numeric Mode

Numeric mode accomplishes the same task as far as modifying permissions go, but with the primary benefit of speed. The associated command is often shorter as shown below.

```bash
chmod 777 test.txt
```

This keeps user with read, write, and execute but also adds read, write, and execute for group and others.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjD7gN5C_-joBYvSTpU8HiOZTXf-wl7oToRlI5vXiZ0UH0QMkzD5UaURfpmGuJRNLKn66DxFjRz5UKVgyvkvvnUwmxIngmhxQgdcohbPrj_X58tsm_OUi9CHrLmf9o4hKlJVPfCIiaYdPRtxP7xqjRNZqmlS8Uj_iDIGOO-AU4YIQwsoDkm5DuxtufXsXd4/w640-h234/2025-02-19%2019_59_51-Post_%20Edit.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjD7gN5C_-joBYvSTpU8HiOZTXf-wl7oToRlI5vXiZ0UH0QMkzD5UaURfpmGuJRNLKn66DxFjRz5UKVgyvkvvnUwmxIngmhxQgdcohbPrj_X58tsm_OUi9CHrLmf9o4hKlJVPfCIiaYdPRtxP7xqjRNZqmlS8Uj_iDIGOO-AU4YIQwsoDkm5DuxtufXsXd4/s1307/2025-02-19%2019_59_51-Post_%20Edit.png)

  

This change is reflected in the updated permissions shown here. But what's special about the number 777 that makes this change?

Each digit in 777 is representative of a set of permissions -- user, group, others.

Read = 4, Write = 2, and Execute = 1

Add the values together to make the desired set of permissions. For example:

621 = User has rw- permissions, Group has -w- permissions, and User has --x permissions.

## File Type Indicator

You may remember that initial "-" we ignored at the beginning of this post. We ignored it because it's not necessarily permissions related, but it's good to keep an eye on especially if one of the less common indicators appears in its position. This tells you the file type you are dealing with. Let's look at our original screenshot.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgqtfxm0Zewmzn9jbldNprQysB29gJVeFAkQHD5-XCXcb9YnQbrc_D7CDLyhN0ta3tUwNYd7LE31HlErH11MjKCfjfy1W-7NIH7662Z2I9P2oYhKlVRbZMpLD7SfsxW7mhUD-Ldz5RhfcxhAGIj1c-6JK6VPSVX9GQd4pqQ3wiOnzPHZdprQepNy4BmNHVb/w640-h376/2025-02-17%2020_57_30-Post_%20Edit.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgqtfxm0Zewmzn9jbldNprQysB29gJVeFAkQHD5-XCXcb9YnQbrc_D7CDLyhN0ta3tUwNYd7LE31HlErH11MjKCfjfy1W-7NIH7662Z2I9P2oYhKlVRbZMpLD7SfsxW7mhUD-Ldz5RhfcxhAGIj1c-6JK6VPSVX9GQd4pqQ3wiOnzPHZdprQepNy4BmNHVb/s2071/2025-02-17%2020_57_30-Post_%20Edit.png)

Some of the most common indicators are:

- = regular file

d = directory

l = symbolic link

## The Sticky Bit

The "sticky bit" originated in Unix and was originally used as a mechanism for executable to load faster by being cached in memory.

As time has gone on and Linux adopted the sticky bit, it's purpose has become quite different -- specifically that of ensuring files can only be deleted or renamed by their owners (and root). The sticky bit is configured on a directory and all files in that directory subsequently have the sticky bit enabled.

Setting the sticky bit can be accomplished with the chmod +t command and is represented by a "t" at the end of the listed permissions. I've included an example below showing the /tmp/ directory with the sticky bit enabled. This is enabled by default for this directory on Ubuntu and other Linux distributions as well.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgTYdBzq-sRPuF2C_ghyphenhyphenz6I1YMJh8nsKBEsTeknn4wgdNsG3g52pF2SNdR8frRHVADx_eAdcAc6rdamhpdMaEe_FY3p_v7rvEy8ZWldUKd9StGkepIbGZY80o88ZAOl1L6gNnOhzqRMX5r9ebhwZECDBS2L09-DVxPuBdVS5M2JDSUY2vYqrBB1Q7K0CPkP/w640-h506/tmp-sticky.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgTYdBzq-sRPuF2C_ghyphenhyphenz6I1YMJh8nsKBEsTeknn4wgdNsG3g52pF2SNdR8frRHVADx_eAdcAc6rdamhpdMaEe_FY3p_v7rvEy8ZWldUKd9StGkepIbGZY80o88ZAOl1L6gNnOhzqRMX5r9ebhwZECDBS2L09-DVxPuBdVS5M2JDSUY2vYqrBB1Q7K0CPkP/s1684/tmp-sticky.png)

## Access Control Lists (ACLs)

Access Control Lists (ACLs) in Linux offer an additional method of viewing and modifying Linux file and directory permissions. These can be thought of not only an additional layer to the traditional permissions we've covered above, but the traditional permissions can also be modified using ACL related commands.

Two commands associated with ACLs are getfacl and setfacl. The former retrieving a file or directory's configured ACL, and the latter configuring the ACL. Here is what running getfacl on a test file I created looks like:

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEih7Lr4c9FFvpNgv6JYX5tHXASQVkBC1D5Jtimnj9gWrzk_DkAVYiqctRqZ4f0t-zWGiBk_PxqgJe4CzVzWiG8C4Gf5UFbBzqoDidd_9ID7Y4BTcwT47HGR6Mh9safy6eNTyYt4SAPvyN17O34qYKB7PzmFZtpuGJYd7Qai3sLB-SKdoe7ChV7_qF2_qEXz/w640-h334/getfacl.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEih7Lr4c9FFvpNgv6JYX5tHXASQVkBC1D5Jtimnj9gWrzk_DkAVYiqctRqZ4f0t-zWGiBk_PxqgJe4CzVzWiG8C4Gf5UFbBzqoDidd_9ID7Y4BTcwT47HGR6Mh9safy6eNTyYt4SAPvyN17O34qYKB7PzmFZtpuGJYd7Qai3sLB-SKdoe7ChV7_qF2_qEXz/s1241/getfacl.png)

  

You can see how the permissions of user, group, and owner in the ACL match that of the traditional permissions.

### Modifying Traditional Permissions with ACLs

Modifying the traditional permissions can be done with a command such as:

```bash
setfacl -m u::rw file_name
```

-m modifies the the ACL.

u::rw grants the User read and write access

file\_name is the file being modified

(You may be wondering -- why the double colon "::" in that command? We'll get to that in a moment).

This command can be changed slightly by replacing u with g or o for Group or Owner, and then the desired permissions.

### Granting Permissions to Specific Users or Groups

The primary benefit of ACLs is that additional layer of permissions I mentioned. ACLs allow you to add permissions for additional users and groups in addition to the owner user or group. This allows for various combinations of permissions to be set which can be good for customization, but can get complicated without proper management.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjPHkIXSnwDq3f4Gpax2JRjIbmUUu1x7KhlVAXoA81fqwPb677Vggg00jLqIP2hegsrjXUg97UGHbsR2SoDSAJpqqI0W0K2KhLb5qG0kiux52uxADMeYK3RF3s_wuszMALEjI6xbZNlHwlBwhKCDS-n6HXp3dy81e0GRlIMjHo3WrAFOruszU7suTG4gsdk/w640-h256/setfacl.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjPHkIXSnwDq3f4Gpax2JRjIbmUUu1x7KhlVAXoA81fqwPb677Vggg00jLqIP2hegsrjXUg97UGHbsR2SoDSAJpqqI0W0K2KhLb5qG0kiux52uxADMeYK3RF3s_wuszMALEjI6xbZNlHwlBwhKCDS-n6HXp3dy81e0GRlIMjHo3WrAFOruszU7suTG4gsdk/s1317/setfacl.png)

  
Using the same setfacl command we used earlier, but specifying a username between the double colons (::), we are now specifying a user to have these desired permissions. This goes beyond the traditional permissions and allows for a separate entry to be shown user:jack:rw- in the output of the ACL. Without the ACL, the only way to achieve these permissions for the user **jack** would be to make **jack** a part of the **cody** group, and assign the group read and write permissions.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjSlelFz-e4sK_LpMlitng0bxi0YE4L_4n1Irhj4l7DKn8rtTZS10DSJY1K5PaWg6g-hce7V0nix2qlx7l9Uac0_EOvpqFyIy1A_AnufH7X0nSrRfghgp1wSiHnUdGMg-Glr9klFyLyMZZR-DRec40FqPU74UzTR4rc3j55xm90qXJf0WTbHGfT4epzCqE7/w640-h264/remove-user-acl.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjSlelFz-e4sK_LpMlitng0bxi0YE4L_4n1Irhj4l7DKn8rtTZS10DSJY1K5PaWg6g-hce7V0nix2qlx7l9Uac0_EOvpqFyIy1A_AnufH7X0nSrRfghgp1wSiHnUdGMg-Glr9klFyLyMZZR-DRec40FqPU74UzTR4rc3j55xm90qXJf0WTbHGfT4epzCqE7/s1234/remove-user-acl.png)

If an ACL entry is no longer needed we just need our familiar setfacl command but with a slight twist.

```bash
setfacl -x u:jack test-file
```

We can see that the entry for **jack** in the ACL has been deleted.

### Mask and Effective Permissions

Lastly, you may have noticed the mask entry in the ACL after we added the **jack** user. mask is the maximum allowed permission for any user or group added to the ACL that isn't the owner user or group. In our case, mask originally received rw permissions because that is what the jack user was assigned in the ACL. If we were to add another user or increase permissions for **jack**, the mask permissions would have expanded as well.

The mask permissions can be set with the following command:

```bash
setfacl -m m::rwx test-file
```

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh3QL5mICIp25HiIXt8JRXEoL_jMI7-GzZVnLzT9KVKePgHqUTNom_8kVCSUWHnO_sS2Lexo5lBqVpBwFZ1m06t1XBSukkLw1vt6mb-OVktZD25NQzRDrpdFt0x3BHNpngE9sKmJQITPft00kDqeuVEHvUT1RY4CChjcJOLtmDddSGSpnpyIOB7rIZ2-am1/w640-h240/2025-02-28%2021_47_34-Post_%20Edit.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh3QL5mICIp25HiIXt8JRXEoL_jMI7-GzZVnLzT9KVKePgHqUTNom_8kVCSUWHnO_sS2Lexo5lBqVpBwFZ1m06t1XBSukkLw1vt6mb-OVktZD25NQzRDrpdFt0x3BHNpngE9sKmJQITPft00kDqeuVEHvUT1RY4CChjcJOLtmDddSGSpnpyIOB7rIZ2-am1/s1261/2025-02-28%2021_47_34-Post_%20Edit.png)

  
Notice here we are starting with a clean slate for an ACL, but have modified the mask to have rwx permissions. Any user or group that is now added to the ACL can have a maximum permission set of Read, Write, and Execute.

Let's see what happens if we add **jack** back to the ACL with rwx permissions, but *also* trim the mask permissions to just read.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgaz7qJMEmS6VlOPxPNyGHrwkX-JuE9rvKRC8ZCGEV89yFcDBvkO751EVy1ly5vx0w-rurS7KeiVeDWPtc7GhgYCeG2f1U3RCXx3_l1a03RK5sEnJ13wQgNo1mo_0qvDRWj4MeufxYIGi3BBn4pP_VS3Ifi0kmyLZzLk3PIqHJW0t6zIwxvIgRCFoJm1jAz/w640-h272/2025-02-28%2021_52_03-Post_%20Edit.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgaz7qJMEmS6VlOPxPNyGHrwkX-JuE9rvKRC8ZCGEV89yFcDBvkO751EVy1ly5vx0w-rurS7KeiVeDWPtc7GhgYCeG2f1U3RCXx3_l1a03RK5sEnJ13wQgNo1mo_0qvDRWj4MeufxYIGi3BBn4pP_VS3Ifi0kmyLZzLk3PIqHJW0t6zIwxvIgRCFoJm1jAz/s1325/2025-02-28%2021_52_03-Post_%20Edit.png)

  
We are now presented with Effective permissions. The **jack** user was assigned rwx permissions, but due to the mask permission set of r, **jack** actually only has r permissions.

### Recursive Permissions and Default ACLs

Some additional points:

- All of what we've done can be done on directories as well. Unless configured to do so, this does not mean the files in that directory inherit the ACL though.
- If you want to set an ACL permission recursively on a directory to affect all files and subdirectories, this can be accomplished with the following (assigning rwx permissions to **jack**):  
    
  ```bash
setfacl -R -m u:jack:rwx /tmp
```
- If you want new files in a directory to inherit the permissions of the ACL of that directory, you must set a default ACL on that directory. This can be done with the following command:  
    
  setfacl -d -m u:jack:rwx /tmp  
    
  This actually produces another set of ACL entries which can be seen using the getfacl command.

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEggkbooCBtItDEALUjlfRN4sUvXah9jknVqcW_p0NwihrcdkKaL_kUa6CNXXEIou7yFZ-DV4TniHRxN9slyrj3xAO8XSHdldNS2AHm4PpLp3ZIyPBuvS3AnmNKQ-oLDX6jN52aCzdsgnitl5g_iP6K5B8nlZR9T8pfZSPRM-9THYV3L863QQbepKzHzBXKl/w640-h346/2025-02-28%2022_11_27-Post_%20Edit.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEggkbooCBtItDEALUjlfRN4sUvXah9jknVqcW_p0NwihrcdkKaL_kUa6CNXXEIou7yFZ-DV4TniHRxN9slyrj3xAO8XSHdldNS2AHm4PpLp3ZIyPBuvS3AnmNKQ-oLDX6jN52aCzdsgnitl5g_iP6K5B8nlZR9T8pfZSPRM-9THYV3L863QQbepKzHzBXKl/s1372/2025-02-28%2022_11_27-Post_%20Edit.png)

## Conclusion

As we've seen, ACLs allow for much greater flexibility than standard Linux permissions alone. Not only is this convenient, but it allows for better security as well since users don't need to be added to owner groups just to have access to a particular file.

This does come with learning some nuances around implementing and reading these additional permissions, but conquering the learning curve is well worth the benefits of the feature.