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
- it should look like \*p*
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
- Tried \*in*. But it says we must use square bracket glob.
- Trying \*[in]* reveals many more useless files.
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

# Challenge 7: Exclusionary globbing
Sometimes, you want to filter out files in a glob! Luckily, [] helps you do just this. If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed. For example:

```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[!ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[^ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

Armed with this knowledge, go forth to /challenge/files and run /challenge/run with all files that don't start with p, w, or n!

NOTE: The ! character has a different special meaning in bash when it's not the first character of a [] glob, so keep that in mind if things stop making sense! ^ does not have this problem, but is also not compatible with older shells.

## Solution: 
- Enter the specified working directory.
- Use glob [!pwn]* as argument.

```sh
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{0pdLe066LE5Hl5VFFJ4J4C2wyg2.QX2IDO0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{0pdLe066LE5Hl5VFFJ4J4C2wyg2.QX2IDO0wCM2kjNzEzW}
```

### References:
- None.

### Notes:
- ! may cause errors when placed elsewhere, ^ does not.
- ^ doesn't work in old bash versions.

# Challenge 8: Tab completion
As tempting as it might be, using * to shorten what must be typed on the commandline can lead to mistakes. Your glob might expand to unintended files, and you might not spot it until the rm command is already running! No one is safe from this style of error.

A safer alternative when you are trying to specify a specific target is tab completion. If you hit tab in the shell, it'll try to figure out what you're going to type and automatically complete it. Auto-completion is super useful, and this challenge will explore its use in specifying files.

This challenge has copied the flag into /challenge/pwncollege, and you can freely cat that file. But you can't type the filename: we used some serious trickery to make sure that you must tab-complete it. Try it out!

```sh
hacker@dojo:~$ ls /challenge
DESCRIPTION.md  pwncollege
hacker@dojo:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@dojo:~$ cat /challenge/pwn<TAB>
pwn.college{HECK YEAH}
hacker@dojo:~$
```
When you hit that tab key, the name will expand and you'll be able to read the file. Good luck!

## Solution: 
- First enter the wroking directory.
- Then use tab to complete filename as shown.

```sh
hacker@globbing~tab-completion:~$ cd /challenge
hacker@globbing~tab-completion:/challenge$ cat /challenge/pwncollege​ 
pwn.college{MInv_CeJYpQNcEBolQ4pdw0QVEn.0FN0EzNxwCM2kjNzEzW}
```

## Flag:
```
pwn.college{MInv_CeJYpQNcEBolQ4pdw0QVEn.0FN0EzNxwCM2kjNzEzW}
```

### References:
- None.

### Notes:
- tab key autocompletes filenames and is safer than blind globbing.

# Challenge 9: Multiple options for tab completion
Consider the following situation:

```sh
hacker@dojo:~$ ls
flag  flamingo  flowers
hacker@dojo:~$ cat f<TAB>
```

There are multiple options! What happens?

What happens varies based on the specific shell and its options. By default bash will auto-expand until the first point when there are multiple options (in this case, fl). When you hit tab a second time, it'll print out those options. Other shells and configurations, instead, will cycle through the options.

This challenge has a /challenge/files directory with a bunch of files starting with pwncollege. Tab-complete from /challenge/files/p or so, and make your way to the flag!

## Solution: 
- Tab from /challenge/files/p shows the full list. Here, we can see the flag file.
- Catting this file shows the flag.

```sh
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwn
pwn                    pwncollege-family      pwncollege-flyswatter
pwn-college            pwncollege-flag        pwncollege-hacking
pwn-the-planet         pwncollege-flamingo    
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-flag
pwn.college{c6Jo8WJz5PGiCG8YccWFSqOWSbr.0lN0EzNxwCM2kjNzEzW}
```

## Flag:
```
pwn.college{c6Jo8WJz5PGiCG8YccWFSqOWSbr.0lN0EzNxwCM2kjNzEzW}
```

### References:
- None.

### Notes:
- When tab has multiple options, bash shows a list of availble options.

# Challenge 10: Tab completion on commands
Tab completion is for more than files! You can also tab-complete commands. This level has a command that starts with pwncollege, and it'll give you the flag. Type pwncollege and hit the tab key to auto-complete it!

NOTE: You can auto-complete any command, but be careful: callous auto-completes without double-checking the result can wreak havoc in your shell if you accidentally run the wrong commands!

## Solution: 
- As said, type pwncollege and tab autocomplete.

```sh
hacker@globbing~tab-completion-on-commands:~$ pwncollege-6165 
Correct! Here is your flag:
pwn.college{onaGhd5IF97CidGry_ialfntirb.0VN0EzNxwCM2kjNzEzW}
```

## Flag:
```
pwn.college{onaGhd5IF97CidGry_ialfntirb.0VN0EzNxwCM2kjNzEzW}
```

### References:
- None.

### Notes:
- Tab autocomplete is also useful for commands.
- Tab autocomplete can be dangerous if accidentally running wrong commands.
