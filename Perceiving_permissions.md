# Challenge 1: Changing File Ownership
First things first: file ownership. Every file in Linux is owned by a user on the system. Most often, in your day-to-day life, that user is the user you log in as every day.

On a shared system (such as in a computer lab), there might be many people with different user accounts, all with their own files in their own home directories. But even on a non-shared system (such as your personal PC), Linux still has many "service" user accounts for different tasks.

The two most important user accounts are:

1. Your user account! On pwn.college, this is the hacker user, regardless of what your username is.
2. root. This is the administrative account and, in most security situations, the ultimate prize. If you take over the root user, you've almost certainly achieved your hacking objective!

So what? Well, it turns out that the way that we prevent you from just doing cat /flag is by having /flag owned by the root user, configure its permissions so that no other user can read it (you will learn how to do that later), and configure the actual challenge to run as the root user (you will learn how to do this later as well). The result is that when you do cat /flag, you get:

```sh
hacker@dojo:~$ ls -l /flag
-r-------- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$ cat /flag
cat: /flag: Permission denied
hacker@dojo:~$
```

Here, you can see that the flag is owned by the root user (the first root in that line) and the root group (the second root in that line). When we try to read it as the hacker user, we are denied. However, if we were root (a hacker's dream!), we would have no problem reading this file:

```sh
root@dojo:~# cat /flag
pwn.college{demo_flag}
root@dojo:~#
```

Interestingly, we can change the ownership of files! This is done via the chown (change owner) command:

```
chown [username] [file]
```

Typically, chown can only be invoked by the root user. Let's pretend that we're root again (that never gets old!), and watch a typical use of chown:

```sh
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chown hacker college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 hacker root    0 May 22 13:42 college_file
drwxr-xr-x 2 root   root 4096 May 22 13:42 pwn_directory
root@dojo:~#
```

college_file's owner has been changed to the hacker user, and now hacker can do with it whatever root had been able to do with it! If this was the /flag file, that means that the hacker user would be able to read it!

In this level, we will practice changing the owner of the /flag file to the hacker user, and then read the flag. For this challenge only, I made it so that you can use chown to your heart's content as the hacker user (again, typically, this requires you to be root). Use this power wisely and chown away!

## Solution: 
- Change ownership using chown.
- Read flag.

```sh
hacker@permissions~changing-file-ownership:~$ chown hacker /flag
hacker@permissions~changing-file-ownership:~$ cat /flag
pwn.college{wA3aAGdywnIkR9AgXcooFsx6Jfr.QXxEjN0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{wA3aAGdywnIkR9AgXcooFsx6Jfr.QXxEjN0wCM2kjNzEzW}
```

### References:
- None

### Notes:
- chown changes ownership of any file.
- Usually accessed by root user only.

# Challenge 2: Groups and Files
Sharing is caring, and sharing is built into Linux's design. Files have both an owning user and group. A group can have multiple users in it, and a user can be a member of multiple groups.

You can check what groups you are part of with the id command:

```sh
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@dojo:~$
```

Here, the hacker user is only in the hacker group. The most common use-case for groups is to control access to different system resources. For example, "Practice Mode" in pwn.college grants you root access to allow better debugging and so on. This is handled by giving you an extra group when you launch in practice mode:

```sh
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker),27(sudo)
hacker@dojo:~$
```

A typical main user of a typical Linux desktop has a lot of groups. For example, this is Zardus' desktop:

```sh
zardus@yourcomputer:~$ id
uid=1000(zardus) gid=1000(zardus) groups=1000(zardus),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),106(netdev),114(bluetooth),117(lpadmin),120(scanner),995(docker)
zardus@yourcomputer:~$
```

All these groups give Zardus the ability to read CDs and floppy disks (who does that anymore?), administer the system, play music, draw to the video monitor, use bluetooth, and so on. Often, this access control happens via group ownership on the filesystem! For example, graphical output can be done via the special /dev/fb0 file:

```sh
zardus@yourcomputer:~$ ls -l /dev/fb0
crw-rw---- 1 root video 29, 0 Jun 30 23:42 /dev/fb0
zardus@yourcomputer:~$
```

This file is a special device file (type c means it is a "character device"), and interacting with it results in changes to the display output (rather than changes to disk storage, as for a normal file!). Zardus' user account on his machine can interact with it because the file has a group ownership of video, and Zardus is a member of the video group.

No such luck for the /flag file in the dojo, though! Consider the following:

```sh
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@dojo:~$ ls -l /flag
-r--r----- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$ cat /flag
cat: /flag: Permission denied
hacker@dojo:~$
```

Here, the flag file is owned by the root user and the root group, and the hacker user is neither the root user nor a member of the root group, so the file cannot be accessed. Luckily, group ownership can be changed with the chgrp (change group) command! Unless you have write access to the file and membership in the new group, this typically requires root access, so let's check it out as root:

```sh
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chgrp hacker college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 root root   4096 May 22 13:42 pwn_directory
root@dojo:~#
```

In this level, I have made the flag readable by whatever group owns it, but this group is currently root. Luckily, I have also made it possible for you to invoke chgrp as the hacker user! Change the group ownership of the flag file, and read the flag!

## Solution: 
- Change group that can access flag.
- Read flag.

```sh
hacker@permissions~groups-and-files:~$ chgrp hacker /flag
hacker@permissions~groups-and-files:~$ cat /flag
pwn.college{gtA7JWilPuhp6MILGbLLmFXwU7D.QXxcjM1wCM2kjNzEzW}
```

## Flag:
```
pwn.college{gtA7JWilPuhp6MILGbLLmFXwU7D.QXxcjM1wCM2kjNzEzW}
```

### References:
- https://www.geeksforgeeks.org/linux-unix/chgrp-command-in-linux-with-examples/

### Notes:
- chgrp changes file access for a group.
- Usually accessible by root or sudo.

# Challenge 3: Fun with Groups Names
In the previous levels, you may have noticed that your hacker user is a member of the hacker group, and that zardus is a member of the zardus group. There is a convention in Linux that every user has their own group, but this does not have to be the case. For example, many computer labs will put all of their users into a single, shared users group.

The point is, you've used hacker for the group before, but in this level, that is not going to work. I'll still allow you to use chgrp, but I have randomized the name of the group that your user is in. You will need to use the id command to figure that name out, then chgrp to victory!

## Solution: 
- Use id to know name of my group.
- chgrp file to my group.
- cat the flag.

```sh
hacker@permissions~fun-with-groups-names:~$ id
uid=1000(hacker) gid=1000(grp14019) groups=1000(grp14019)
hacker@permissions~fun-with-groups-names:~$ chgrp grp14019 /flag
hacker@permissions~fun-with-groups-names:~$ cat /flag
pwn.college{4M--Wa__qFVH8zYYFW00uoop_wK.QXycjM1wCM2kjNzEzW}
```

## Flag:
```
pwn.college{4M--Wa__qFVH8zYYFW00uoop_wK.QXycjM1wCM2kjNzEzW}
```

### References:
- None

### Notes:
- id command shows us the groups user is part of.

# Challenge 4: Chamging Permissions
So now we're well-versed in ownership. Let's talk about the other side of the coin: file permissions. Recall our example:

```sh
hacker@dojo:~$ mkdir pwn_directory
hacker@dojo:~$ touch college_file
hacker@dojo:~$ ls -l
total 4
-rw-r--r-- 1 hacker hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 hacker hacker 4096 May 22 13:42 pwn_directory
hacker@dojo:~$
```

As a reminder, the first character there is the file type. The next nine characters are the actual access permissions of the file or directory, split into 3 characters denoting permissions for the owning user (now you understand this!), 3 characters denoting the permissions for the owning group (now you understand this as well!), and 3 characters denoting the permissions that all other access (e.g., by other users and other groups) has to the file.

Each character of the three represent permission for a different type:

- r - user/group/other can read the file (or list the directory)
- w - user/group/other can modify the files (or create/delete files in the directory)
- x - user/group/other can execute the file as a program (or can enter the directory, e.g., using `cd`)
- - - nothing 

For college_file above, the rw-r--r-- permissions entry decodes to:

- r: the user that owns the file (user hacker) can read it
- w: the user that owns the file (user hacker) can write to it
- -: the user that owns the file (user hacker) cannot execute it
- r: users in the group that owns the file (group hacker) can read it
- -: users in the group that owns the file (group hacker) cannot write to it
- -: users in the group that owns the file (group hacker) cannot execute it
- r: all other users can read it
- -: all other users cannot write to it
- -: all other users cannot execute it
- 
Now, let's look at the default permissions of /flag:

```sh
hacker@dojo:~$ ls -l /flag
-r-------- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$
```

Here, there is only one bit set: the read permission for the owning user (in this case, root). Members of the owning group (the root group) and all other users have no access to the file.

You might be wondering how the chgrp levels worked, if there is no group access to the file. Well, for those levels, I set the permissions differently:

```sh
hacker@dojo:~$ ls -l /flag
-r--r----- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$
```

The group had access! That is why chgrping the file enabled you to read the file.

Anyways! Like ownership, file permissions can also be changed. This is done with the chmod (change mode) command. The basic usage for chmod is:

```
chmod [OPTIONS] MODE FILE
```

You can specify the MODE in two ways: as a modification of the existing permissions mode, or as a completely new mode to overwrite the old one.

In this level, we will cover the former: modifying an existing mode. chmod allows you to tweak permissions with the mode format of WHO+/-WHAT, where WHO is user/group/other and WHAT is read/write/execute. For example, to add read access for the owning user, you would specify a mode of u+r. write and execute access for the group and the other (or all the modes) are specified the same way. More examples:

u+r, as above, adds read access to the user's permissions
g+wx adds write and execute access to the group's permissions
o-w removes write access for other users
a-rwx removes all permissions for the user, group, and world

So:

```sh
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chmod go-rwx *
root@dojo:~# ls -l
total 4
-rw------- 1 hacker root    0 May 22 13:42 college_file
drwx------ 2 root   root 4096 May 22 13:42 pwn_directory
root@dojo:~#
```

In this challenge, you must change the permissions of the /flag file to read it! Typically, you need to have write access to the file in order to change its permissions, but I have made the chmod command all-powerful for this level, and you can chmod anything you want even though you are the hacker user. This is an ultimate power. The /flag file is owned by root, and you can't change that, but you can make it readable. Go and solve this!

## Solution: 
- Add reading permissions to everyone.
- Read flag

```sh
hacker@permissions~changing-permissions:~$ chmod ugo+r /flag
hacker@permissions~changing-permissions:~$ cat /flag
pwn.college{MIiFL6IJWFfEWUqBNe4vq9oRPJX.QXzcjM1wCM2kjNzEzW}
```

## Flag:
```
pwn.college{MIiFL6IJWFfEWUqBNe4vq9oRPJX.QXzcjM1wCM2kjNzEzW}
```

### References:
- None

### Notes:
- chmod changes permissions.

# Challenge 5: Executable Files
So far, you have mostly been dealing with read permissions. This makes sense, because you have been making the /flag file readable to read it. In this level, we will explore execute permissions.

When you invoke a program, such as /challenge/run, Linux will only actually execute it if you have execute-access to the program file. Consider:

```sh
hacker@dojo:~$ ls -l /challenge/run
-rwxr-xr-x 1 root root    0 May 22 13:42 /challenge/run
hacker@dojo:~$ /challenge/run
Successfully ran the challenge!
hacker@dojo:~$
```

In this case, /challenge/run runs because it is executable by the hacker user. Because the file is owned by the root user and root group, this requires that the execute bit is set on the other permissions. If we remove these permissions, the execution will fail!

```sh
hacker@dojo:~$ chmod o-x /challenge/run
hacker@dojo:~$ ls -l /challenge/run
-rwxr-xr-- 1 root root    0 May 22 13:42 /challenge/run
hacker@dojo:~$ /challenge/run
bash: /challenge/run: Permission denied
hacker@dojo:~$
```

In this challenge, the /challenge/run program will give you the flag, but you must first make it executable! Remember your chmod, and get /challenge/run to tell you the flag!

## Solution: 
- Add execution permission using chmod.
- Execute /challenge/run for flag.

```sh
hacker@permissions~executable-files:~$ chmod ugo+x /challenge/run
hacker@permissions~executable-files:~$ /challenge/run
Successful execution! Here is your flag:
pwn.college{sTl4rPYEsTc3dAnOZXMxZbHH3Jb.QXyEjN0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{sTl4rPYEsTc3dAnOZXMxZbHH3Jb.QXyEjN0wCM2kjNzEzW}
```

### References:
- None

### Notes:
- None.

# Challenge 6: Permission Tweaking Practice
You think you can chmod? Let's practice!

This challenge will ask you to change the permissions of the /challenge/pwn file in specific ways a few times in a row. If you get the permissions wrong, the game will reset and you can try again. If you get the permissions right eight times in a row, the challenge will let you chmod /flag to make it readable for yourself :-) Launch /challenge/run to get started!

## Solution: 
- Correctly set all permissions for 8 rounds.
- Get read permission for flag.
- Read flag.
- Solution code below has been shortened.

```sh
hacker@permissions~permission-tweaking-practice:~$ /challenge/run
Round 1 of 8!

Current permissions of "/challenge/pwn": rw-r--r--

Needed permissions of "/challenge/pwn": rw-rw-r--
hacker@permissions~permission-tweaking-practice:~$ chmod g+w /challenge/pwn
You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": rw-rw-r--

Needed permissions of "/challenge/pwn": r--r--r--
hacker@permissions~permission-tweaking-practice:~$ chmod ug-w /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": r--r--r--

Needed permissions of "/challenge/pwn": r--r-xr--
hacker@permissions~permission-tweaking-practice:~$ chmod g+x /challenge/pwn
You set the correct permissions!
Round 4 of 8!

Current permissions of "/challenge/pwn": r--r-xr--

Needed permissions of "/challenge/pwn": rwxr-xrwx
hacker@permissions~permission-tweaking-practice:~$ chmod uo+wx /challenge/pwn
You set the correct permissions!
Round 5 of 8!

Current permissions of "/challenge/pwn": rwxr-xrwx

Needed permissions of "/challenge/pwn": rw-r--rw-
hacker@permissions~permission-tweaking-practice:~$ chmod ugo-x /challenge/pwn
You set the correct permissions!
Round 6 of 8!

Current permissions of "/challenge/pwn": rw-r--rw-

Needed permissions of "/challenge/pwn": rwxr-xrw-
hacker@permissions~permission-tweaking-practice:~$ chmod ug+x /challenge/pwn
You set the correct permissions!
Round 7 of 8!

Current permissions of "/challenge/pwn": rwxr-xrw-
Needed permissions of "/challenge/pwn": rw-r-xrw-
hacker@permissions~permission-tweaking-practice:~$ chmod u-x /challenge/pwn
You set the correct permissions!
Round 8 of 8!

Current permissions of "/challenge/pwn": rw-r-xrw-

Needed permissions of "/challenge/pwn": -w-r-x-w-
hacker@permissions~permission-tweaking-practice:~$ chmod uo-r /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod ugo+r /flag
hacker@permissions~permission-tweaking-practice:~$ cat /flag
pwn.college{wJYrTitCBMttYRHOeXkvrT8OvI1.QXwEjN0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{wJYrTitCBMttYRHOeXkvrT8OvI1.QXwEjN0wCM2kjNzEzW}
```

### References:
- None

### Notes:
- None.

# Challenge 7: Permissions Setting Practice
In addition to adding and removing permissions, as in the previous level, chmod can also simply set permissions altogether, overwriting the old ones. This is done by using = instead of - or +. For example:

- u=rw sets read and write permissions for the user, and wipes the execute permission
- o=x sets only executable permissions for the world, wiping read and write
- a=rwx sets read, write, and executable permissions for the user, group, and world!

But what if you want to change user permissions in a different way as group permissions? Say, you want to set rw for the owning user, but only r for the owning group? You can achieve this by chaining multiple modes to chmod with ,!

- chmod u=rw,g=r /challenge/pwn will set the user permissions to read and write, and the group permissions to read-only
- chmod a=r,u=rw /challenge/pwn will set the user permissions to read and write, and the group and world permissions to read-only

Additionally, you can zero out permissions with -:

chmod u=rw,g=r,o=- /challenge/pwn will set the user permissions to read and write, the group permissions to read-only, and the world permissions to nothing at all
Keep in mind, that -, appearing after = is in a different context than if it appeared directly after the u, g, or o (in which case, it would cause specific bits to be removed, not everything).

This level extends the previous level by requesting more radical permission changes, which you will need = and ,-chaining to achieve. Good luck!

## Solution: 
- Correctly set permissions.

```sh
hacker@permissions~permissions-setting-practice:~$ /challenge/run
Round 1 of 8!

Current permissions of "/challenge/pwn": rw-r--r--

Needed permissions of "/challenge/pwn": -w-r-xrwx
hacker@permissions~permissions-setting-practice:~$ chmod u=w,g=rx,o=rwx /challenge/pwn
You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": -w-r-xrwx

Needed permissions of "/challenge/pwn": r---w-rwx
hacker@permissions~permissions-setting-practice:~$ chmod u=r,g=w /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": r---w-rwx

Needed permissions of "/challenge/pwn": ---rwx---
hacker@permissions~permissions-setting-practice:~$ chmod u=-,g=rwx,o=- /challenge/pwn
You set the correct permissions!
Round 4 of 8!

Current permissions of "/challenge/pwn": ---rwx---

Needed permissions of "/challenge/pwn": ---r--r-x
hacker@permissions~permissions-setting-practice:~$ chmod g=r,o=rx /challenge/pwn
You set the correct permissions!
Round 5 of 8!

Current permissions of "/challenge/pwn": ---r--r-x

Needed permissions of "/challenge/pwn": -w---x-wx
hacker@permissions~permissions-setting-practice:~$ chmod u=w,g=x,o=wx /challenge/pwn
You set the correct permissions!
Round 6 of 8!

Current permissions of "/challenge/pwn": -w---x-wx

Needed permissions of "/challenge/pwn": -w-rw-r--
hacker@permissions~permissions-setting-practice:~$ chmod g=rw,o=r /challenge/pwn
You set the correct permissions!
Round 7 of 8!

Current permissions of "/challenge/pwn": -w-rw-r--

Needed permissions of "/challenge/pwn": --xrw-rwx
hacker@permissions~permissions-setting-practice:~$ chmod u=x,g=rw,o=rwx /challenge/pwn
You set the correct permissions!
Round 8 of 8!

Current permissions of "/challenge/pwn": --xrw-rwx

Needed permissions of "/challenge/pwn": -----xr--
hacker@permissions~permissions-setting-practice:~$ chmod u=-,g=x,o=r /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod ugo+r /flag
hacker@permissions~permissions-setting-practice:~$ cat /flag
pwn.college{cXG0YHq_OH_gurRSgyz-Sw_wdPI.QXzETO0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{cXG0YHq_OH_gurRSgyz-Sw_wdPI.QXzETO0wCM2kjNzEzW}
```

### References:
- None

### Notes:
- chmod a=b overwrites permission b for a.

# Challenge 8: The SUID Bit
As you explored in the previous module, there are many cases in which non-root users need elevated access to do certain system tasks. The system admin can't be there to give them the password every time a user wanted to do a task that only root/sudoers can do. Instead, the "Set User ID" (SUID) permissions bit allows the user to run a program as the owner of that program's file.

This is actually the exact mechanism used to let the challenge programs you run read the flag or, outside of pwn.college, to enable system administration tools such as su, sudo, and so on. The permissions of a file with SUID look like this:

```sh
hacker@dojo:~$ ls -l /usr/bin/sudo
-rwsr-xr-x 1 root root 232416 Dec 1 11:45 /usr/bin/sudo
hacker@dojo:~$
```

The s part in place of the executable bit means that the program is executable with SUID. It means that, regardless of what user runs the program (as long as they have executable permissions), the program will execute as the owner user (in this case, the root user).

As the owner of a file, you can set a file's SUID bit by using chmod:
```
chmod u+s [program]
```
But be careful! Giving the SUID bit to an executable owned by root can give attackers a possible attack vector to become root. You will learn more about this in the Program Misuse module.

Now, we are going to let you add the SUID bit to the /challenge/getroot program in order to spawn a root shell for you to cat the flag yourself!

## Solution: 
- Use chmod to give suid to users.
- Get root.
- Read flag.

```sh
hacker@permissions~the-suid-bit:~$ chmod ugo+s /challenge/getroot
hacker@permissions~the-suid-bit:~$ /challenge/getroot
SUCCESS! You have set the suid bit on this program, and it is running as root! 
Here is your shell...
root@permissions~the-suid-bit:~# cat /flag
pwn.college{gmM1bqUdIIm7ta6CtZ8mrtLZL1b.QXzEjN0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{gmM1bqUdIIm7ta6CtZ8mrtLZL1b.QXzEjN0wCM2kjNzEzW}
```

### References:
- None

### Notes:
- chmod a-s gives suid access to a. This can help a run a program as root/owner.
