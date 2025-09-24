# Challenge 1: Learning From Documentation
The typical need you'll have for documentation is just to figure out how to use all these dang programs, and a specific case of that is figuring out what arguments to specify on the command line. This module will mostly dig into that concept, as a proxy for figuring out how to use the programs in general. Through the rest of the module, you'll go through various ways of asking the environment for help for the programs, but first, we'll dig into the concept of reading documentation.

The correct usage of programs depends, in a large part, on the proper specification of arguments to them. Recall the -a of ls -a in the hidden files challenge of the Basic Commands module: that -a was an argument that told ls to list out hidden files as well as non-hidden files. Because we wanted to list out hidden files, invoking ls with the -a argument was the correct way to use it in our scenario.

The program for this challenge is /challenge/challenge, and you'll need to invoke it properly in order for it to give you the flag. Let's pretend that this is its documentation:

```
Welcome to the documentation for /challenge/challenge! To properly run this program, you will need to pass it the argument of --giveflag. Good luck!
```

Given that knowledge, go get the flag!

## Solution: 
- We need to invoke the /challenge/challenge command with the proper argument of --giveflag.
- This gives the flag.

```sh
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{ECknFjeTG1d261rPMfI8xX5kNA_.QX0ITO0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{ECknFjeTG1d261rPMfI8xX5kNA_.QX0ITO0wCM2kjNzEzW}
```

### References:
- None

### Notes:
- Commands must be invoked with proper arguments.

# Challenge 2: Learning Complex Usage
While using most commands is straightforward, the usage of some commands can get quite complex. For example, the arguments to commands like sed and awk, which we're definitely not getting into right now, are entire programs in an esoteric programming language! Somewhere on the spectrum between cd and awk are commands that take arguments to their arguments...

This sounds crazy, but you've already encountered this with the find level in Basic Commands. find has a -name argument, and the -name argument itself takes an argument specifying the name to search for. Many other commands are analogous.

Here is this level's documentation for /challenge/challenge:

```
Welcome to the documentation for /challenge/challenge! This program allows you to print arbitrary files to the terminal, when given the --printfile argument. The argument to the --printfile argument is the path of the flag to read. For example, /challenge/challenge --printfile /challenge/DESCRIPTION.md will print out the description of the level!
```

Given that documentation, go get the flag!

## Solution: 
- This documentation tells us the usage of --printfile argument to print the files from a filepath.
- Doing the above steps on /flag as an experiment gave me the flag immediately.

```sh
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{ISztu9qMWs8U_G2dwJ1xpom-qlq.QX1ITO0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{ISztu9qMWs8U_G2dwJ1xpom-qlq.QX1ITO0wCM2kjNzEzW}
```

### References:
- None

### Notes:
- --printfile argument prints files on the given file path.

# Challenge 3: Reading Manuals
This level introduces the man command. man is short for manual, and will display (if available) the manual of the command you pass as an argument. For example, let's say we wanted to learn about the yes command (yes, this is a real command):

```sh
hacker@dojo:~$ man yes
```

This will display the manual page for yes, which will look something like this:

```
YES(1)                           User Commands                          YES(1)

NAME
       yes - output a string repeatedly until killed

SYNOPSIS
       yes [STRING]...
       yes OPTION

DESCRIPTION
       Repeatedly output a line with all specified STRING(s), or 'y'.

       --help display this help and exit

       --version
              output version information and exit

AUTHOR
       Written by David MacKenzie.

REPORTING BUGS
       GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
       Report any translation bugs to <https://translationproject.org/team/>

COPYRIGHT
       Copyright  ©  2020  Free Software Foundation, Inc.  License GPLv3+: GNU
       GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This is free software: you are free  to  change  and  redistribute  it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       Full documentation <https://www.gnu.org/software/coreutils/yes>
       or available locally via: info '(coreutils) yes invocation'

GNU coreutils 8.32               February 2022                          YES(1)
```

The important sections are:

```
NAME(1)                           CATEGORY                          NAME(1)

NAME
	This gives the name (and short description) of the command or
	concept discussed by the page.

SYNOPSIS
	This gives a short usage synopsis. These synopses have a standard
	format. Typically, each line is a different valid invocation of the
	command, and the lines can be read as:

	COMMAND [OPTIONAL_ARGUMENT] SINGLE_MANDATORY_ARGUMENT
	COMMAND [OPTIONAL_ARGUMENT] MULTIPLE_ARGUMENTS...

DESCRIPTION
	Details of the command or concept, with detailed descriptions
	of the various options.

SEE ALSO
	Other man pages or online resources that might be useful.

COLLECTION                        DATE                          NAME(1)
```

You can scroll around the manpage with your arrow keys and PgUp/PgDn. When you're done reading the manpage, you can hit q to quit.

Manpages are stored in a centralized database. If you're curious, this database lives in the /usr/share/man directory, but you never need to interact with it directly: you just query it using the man command. The arguments to the man command aren't file paths, but just the names of the entries themselves (e.g., you run man yes to look up the yes manpage, rather than man /usr/bin/yes, which would be the actual path to the yes program but would result in man displaying garbage).

The challenge in this level has a secret option that, when you use it, will cause the challenge to print the flag. You must learn this option through the man page for challenge!

## Solution: 
- Opening man page for challenge gives us this:

```
CHALLENGE(1)                     Challenge Commands                     CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --wqzpcc NUM
              print the flag if NUM is 650

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The  repository  for this dojo: <https://github.com/pwncollege/linux-luminar‐
       ium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                           May 2024                          CHALLENGE(1)
```
- It says we need to run /challenge/challenge.
- The hiddden agrument is --wqzpcc 650.
- Using the argument after pressing q to quit gives us the flag.

```sh
hacker@man~reading-manuals:~$ man challenge
hacker@man~reading-manuals:~$ /challenge/challenge --wqzpcc 650
Correct usage! Your flag: pwn.college{wMqPZRJRAFz6pABOc5chQRpazaX.QX0EDO0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{wMqPZRJRAFz6pABOc5chQRpazaX.QX0EDO0wCM2kjNzEzW}
```

### References:
- man page for "challenge" command.
- https://man7.org/linux/man-pages/

### Notes:
- man command gives us the documentation for any command that is stored in the above refernced link.

# Challenge 4: 


```sh

```



## Solution: 
-

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
-

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
-

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
-

```sh

```

## Flag:
```

```

### References:
- 

### Notes:
- 
