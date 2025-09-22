# CHallenge 1: The Root
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
