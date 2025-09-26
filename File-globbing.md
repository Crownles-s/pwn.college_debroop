# Challenge 1: Matching with *

The first glob we'll learn is *. When it encounters a * character in any argument, the shell will treat it as a "wildcard" and try to replace that argument with any files that match the pattern. It's easier to show you than explain:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_*
Look: file_a file_b file_c
```

Of course, though in this case, the glob resulted in multiple arguments, it can just as simply match only one. For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: file_*
Look: file_a
```
When zero files are matched, by default, the shell leaves the glob unchanged:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
```

The * matches any part of the filename except for / or a leading . character. For example:

```sh
hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
```

Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use globbing to keep the argument you pass to cd to at most four characters! Once you're there, run /challenge/run for the flag!

## Solution: 
- we must go to /challenge in less than 4 characters.
- cd /ch*

```sh
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /run
bash: /run: Is a directory
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{oZSLuDtqPXNvm2wKQofn0aIPbOx.QXxIDO0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{oZSLuDtqPXNvm2wKQofn0aIPbOx.QXxIDO0wCM2kjNzEzW}
```

### References:
- None.

### Notes:
- * globbing works everywhere, except leading / or leading .

# Challenge 2: Matching with ?
Next, let's learn about ?. When it encounters a ? character in any argument, the shell will treat it as a single-character wildcard. This works like *, but only matches one character. For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_cc
hacker@dojo:~$ ls
file_a	file_b	file_cc
hacker@dojo:~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:~$ echo Look: file_??
Look: file_cc
```

Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use the ? character instead of c and l in the argument to cd! Once you're there, run /challenge/run for the flag!

## Solution: 
- We replace all c and l in cd /challenge with ? globbing as directed.
- Doing so successfully gets us into /challenge, where we can run /challenge/run for the flag.

```sh
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{EbbJVOxbkhikwX-PrKojtxaNhJc.QXyIDO0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{EbbJVOxbkhikwX-PrKojtxaNhJc.QXyIDO0wCM2kjNzEzW}
```

### References:
- None.

### Notes:
- ? globbing works like * globbing except it gets only single characters while * gets multiple.

# Challenge 3: Matching with []

Next, we will cover []. The square brackets are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, or n. For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

Try it here! We've placed a bunch of files in /challenge/files. Change your working directory to /challenge/files and run /challenge/run with a single argument that bracket-globs into file_b, file_a, file_s, and file_h!

## Solution: 
- Change working directory as specified.
- Use the correct globbing, but I made an error in typing.
- Correcting the error gets the flag successfully.

```sh
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file[bash]
Your expansion did not expand to the requested files (file_a, file_b, file_h, 
and file_s). Instead, it expanded to:
file[bash]
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{QsomuY2lcLzqWhibuQCOxa_1STq.QXzIDO0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{QsomuY2lcLzqWhibuQCOxa_1STq.QXzIDO0wCM2kjNzEzW}
```

### References:
- None.

### Notes:
- [] globbing is like ? globbing in the sense that it matches single characters only.
- The difference is that we input it as [xyz] and x, y, z are the characters we need to glob.

# Challenge 4: Matching paths with []
Globbing happens on a path basis, so you can expand entire paths with your globbed arguments. For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: /home/hacker/file_[ab]
Look: /home/hacker/file_a /home/hacker/file_b
```

Now it's your turn. Once more, we've placed a bunch of files in /challenge/files. Starting from your home directory, run /challenge/run with a single argument that bracket-globs into the absolute paths to the file_b, file_a, file_s, and file_h files!

## Solution: 
- We need to run a command from home this time, ie no changing directory.
- Use path globbing to get the flag.

```sh
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{08AKNbxhPguzSYTGcN-upqLFxPm.QX0IDO0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{08AKNbxhPguzSYTGcN-upqLFxPm.QX0IDO0wCM2kjNzEzW}
```

### References:
- None.

### Notes:
- Globbing works inside paths.

# Challenge 5: Multiple globs
So far, you've specified one glob at a time, but you can do more! Bash supports the expansion of multiple globs in a single word. For example:

```sh
hacker@dojo:~$ cat /*fl*
pwn.college{YEAH}
hacker@dojo:~$
```

What happens above is that the shell looks for all files in / that start with anything (including nothing), then have an f and an l, and end in anything (including ag, which makes flag).

Now you try it. We put a few happy, but diversely-named files in /challenge/files. Go cd there and run /challenge/run, providing a single argument: a short (3 characters or less) globbed word with two * globs in it that covers every word that contains the letter p.

## Solution: 
- First, we need to cd to /challenge/files.
- Then, run/challenge/run with required length argument.
- it should look like *p*
- This works and gives the flag.

```sh
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{QPMmuBn1ZwBV1n1PK89SdW3YMKg.0lM3kjNxwCM2kjNzEzW}
```

## Flag:
```
pwn.college{QPMmuBn1ZwBV1n1PK89SdW3YMKg.0lM3kjNxwCM2kjNzEzW}
```

### References:
- None.

### Notes:
- Multiple globs also work properly.
- We can glob files containing phrases using this method. For example, *abc* gives files with names containing abc inside.

# Challenge 6: Mixing globs
Now, let's put the previous levels together! We put a few happy, but diversely-named files in /challenge/files. Go cd there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to /challenge/run) will match the files "challenging", "educational", and "pwning"!

## Solution: 
- Firstly we must cd to working directory.
- Then, there must be some common letters or features in these 3 words.
- The first similarity is that they contain i and n.
- Tried globbing [i*n]. Did not work.
- Tried *in*. But it says we must use square bracket glob.
- Trying *[in]* reveals many more useless files.
- Another observation is that none of the useless files start with c p or e. So, [cpe]* is an option. This worked.

```sh
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [i*n]
Your expansion did not expand to the requested files (challenging, educational, 
pwning). Instead, it expanded to:
[i*n]
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run *in*
Error: you did not use a square bracket glob...
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run *[in]*
Your expansion did not expand to the requested files (challenging, educational, 
pwning). Instead, it expanded to:
amazing beautiful challenging delightful educational fantastic incredible jovial kind laughing magical nice optimistic pwning queenly radiant splendid thrilling uplifting victorious wonderful xenial
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cpe]*
You got it! Here is your flag!
pwn.college{QQ9auXpfWLlmz3hpnFDD4pvssZE.QX1IDO0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{QQ9auXpfWLlmz3hpnFDD4pvssZE.QX1IDO0wCM2kjNzEzW}
```

### References:
- https://www.man7.org/linux/man-pages/man7/glob.7.html

### Notes:
- Mixing different globs can be difficult to pull off.

# Challenge 7: 

```sh

```

## Solution: 


```sh

```

## Flag:
```

```

### References:
-

### Notes:

# Challenge 8: 

```sh

```

## Solution: 


```sh

```

## Flag:
```

```

### References:
-

### Notes:

# Challenge 9: 

```sh

```

## Solution: 


```sh

```

## Flag:
```

```

### References:
-

### Notes:

# Challenge 10: 

```sh

```

## Solution: 


```sh

```

## Flag:
```

```

### References:
-

### Notes:
- 
