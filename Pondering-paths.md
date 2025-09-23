# Challenge 1: The Root
Alright, so the filesystem starts at /. Under that, there are a whole mess of other directories, configuration files, programs, and, most importantly, flags. In this level, we've added a program right in /, called pwn, that will give you the flag. All you need to do for this level is to invoke this program!
You can invoke a program by providing its path on the command line. In this case, you'll be giving the exact path, starting from /, so the path would be /pwn. This style of path, one that starts with the root directory, is referred to as an "absolute path".
Start the challenge, launch a terminal, invoke the pwn program using its absolute path, and Capture that Flag! Good luck!

## Solution: 
Although the challenge was to run the /pwd command, I ran the pwd command. 
This gave an error and pointed me onto the correct command.

```sh
~$ pwn
It looks like you invoked 'pwn' instead of the absolute path ('/pwn'). You'll 
learn more about how this is different later, but suffice it to say: you ran 
the wrong thing. Use the absolute path, instead!
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{IG8cxFVsJuWj2HWLP6m3L31n9TU.QX4cTO0wCM2kjNzEzW}
```

## Flag:
pwn.college{IG8cxFVsJuWj2HWLP6m3L31n9TU.QX4cTO0wCM2kjNzEzW}

### References:
- None

### Notes:
- Absolute paths must start with / which is the root.
- Trying an absolute path without root shows an error.

# Challenge 2: Program and absolute paths
Let's explore a slightly more complicated path! Except for in the previous level, challenges in pwn.college are in the challenge directory and the challenge directory is, in turn, right in the root directory (/). The path to the challenge directory is, thus, /challenge. The name of the challenge program in this level is run, and it lives in the /challenge directory. Thus, the path to the run challenge program is /challenge/run.

This challenge again requires you to execute it by invoking its absolute path. You'll want to execute the run file that is in the challenge directory that is, in turn, in the / directory. If you invoke the challenge correctly, it will give you the flag. Good luck!

## Solution:
This challenge requires us to enter the challenge directory using an absolute path /challenge. Also, use the /run path to start the challenge.

```sh
$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{UqAvSqBrha1zreqe4m6YaVlsPV4.QX1QTN0wCM2kjNzEzW}
```

## Flag:
pwn.college{UqAvSqBrha1zreqe4m6YaVlsPV4.QX1QTN0wCM2kjNzEzW}

### References:
- None

### Notes:
- All challenges live in the root and challenge directory.
- use /challenge to enter challenge directory from this challenge onwards.

# Challenge 3: Position thy self 
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

```sh
hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
```

This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ~ was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

## Solution:
-This requires us to run a cd command to change the working directory. The cd command must have your destination directory as an argument. 
- We must first get the working directory.
- Tried to run /challenge/run to get the error, and get the terminal to reveal the working directory.

```sh
~$ /challenge/run
Incorrect...
You are not currently in the /proc/138 directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-thy-self:~$ cd /proc/138
hacker@paths~position-thy-self:/proc/138$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{YZjo7clhY3y8Aog9WFNyLoEqnuS.QX2QTN0wCM2kjNzEzW}
```
- Terminal revealed the correct directory successfully.

## Flag:
pwn.college{YZjo7clhY3y8Aog9WFNyLoEqnuS.QX2QTN0wCM2kjNzEzW}

### References:
- None

### Notes:
- All commands must be run from the correct working directory.
- Running commands in the wrong directory may throw an error.
