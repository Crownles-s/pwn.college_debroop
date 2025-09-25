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


```sh

```

## Flag:
```

```

### References:
-

### Notes:

# Challenge 3: 

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

# Challenge 4: 

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

# Challenge 5: 

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

# Challenge 6: 

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
