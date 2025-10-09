# Challenge 1: The PATH Variable
t turns out that the answer to "How does the shell find ls?" is fairly simple. There is a special shell variable, called PATH, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands. If you blank out the variable, things go badly:

```sh
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ PATH=""
hacker@dojo:~$ ls
bash: ls: No such file or directory
hacker@dojo:~$
```

Without a PATH, bash cannot find the ls command.

In this level, you will disrupt the operation of the /challenge/run program. This program will DELETE the flag file using the rm command. However, if it can't find the rm command, the flag will not be deleted, and the challenge will give it to you! Thus, you must make it so that /challenge/run also can't find the rm command!

Keep in mind: /challenge/run will be a child process of your shell, so you must apply the concepts you learned in Shell Variables to mess with its PATH variable! If you don't succeed, and the flag gets deleted, you will need to restart the challenge to try again!

## Solution: 
- Set the path variable blank.
- Run /challenge/run.

```sh
hacker@path~the-path-variable:~$ PATH=""
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{EEaUuXeu4KI_6iSJV4ZXto220E6.QX2cDM1wCM2kjNzEzW}
```

## Flag:
```
pwn.college{EEaUuXeu4KI_6iSJV4ZXto220E6.QX2cDM1wCM2kjNzEzW}
```

### References:
- None

### Notes:
- PATH variable helps store paths of everything.
- Setting it blank can mess up file and command recognition.

# Challenge 2: Setting PATH
Okay, so things break when you blank out PATH. But what about doing something useful with PATH?

Let's explore how we would, for example, add a new directory of programs to our command repertoire. Recall that PATH stores a list of directories to find commands in and, for commands in nonstandard places, we must typically execute them via their path:

```sh
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ goodscript
bash: goodscript: command not found
hacker@dojo:~$ /home/hacker/scripts/goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

If you maintain useful scripts that you want to be able to launch by bare name, this is annoying. However, by adding directories to or replacing directories in this list, you can expose these programs to be launched using their bare name! For example:

```sh
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

Let's practice. This level's /challenge/run will run the win command via its bare name, but this command exists in the /challenge/more_commands/ directory, which is not initially in the PATH. The win command is the only thing that /challenge/run needs, so you can just overwrite PATH with that one directory. Good luck!

## Solution: 
- Add the more commands directory tO PATH.
- Run /challenge/run for flag.
  
```sh
hacker@path~setting-path:~$ PATH=/challenge/more_commands/
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{gv7Xd76q8UhsnelOPbuulMOCMvx.QX1cjM1wCM2kjNzEzW}
```

## Flag:
```
pwn.college{gv7Xd76q8UhsnelOPbuulMOCMvx.QX1cjM1wCM2kjNzEzW}
```

### References:
- None

### Notes:
- We can add directories to path to make them easier to invoke.

# Challenge 3: Finding Commands
When you type the name of a command, something inside one of the many directories listed in your $PATH variable is what actually gets executed (of course, unless the command is a builtin!). But which file, precisely? You can find out with the aptly-named which command:

```sh
hacker@dojo:~$ which cat
/bin/cat
hacker@dojo:~$ /bin/cat /flag
YEAH
hacker@dojo:~$
```

Mirroring what the shell does when searching for commands, which looks at each directory in $PATH in order and prints the first file it finds whose name matches the argument you passed.

In this challenge, we added a win command somewhere in your $PATH, but it won't give you the flag. Instead, it's in the same directory as a flag file that we made readable by you! You must find win (with the which command), and cat the flag out of that directory!

## Solution: 
- Use which command to find location of win command.
- cat the flag in that directory.

```sh
hacker@path~finding-commands:~$ which win
/challenge/paths/26910/win
hacker@path~finding-commands:~$ cat /challenge/paths/26910/flag
pwn.college{UW8S9GGMIN5UEhxSGsxBeicqeoc.01NzEzNxwCM2kjNzEzW}
```

## Flag:
```
pwn.college{UW8S9GGMIN5UEhxSGsxBeicqeoc.01NzEzNxwCM2kjNzEzW}
```

### References:
- None

### Notes:
- which command finds path of a command stored in PATH.

# Challenge 4: Adding Commands
Recall our example from the previous level:

```sh
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

What we see here, of course, is the hacker making the shell more useful for themselves by bringing their own commands to the party. Over time, you might amass your own elegant tools. Let's start with win!

Previously, the win command that /challenge/run executed was stored in /challenge/more_commands. This time, win does not exist! Recall the final level of Chaining Commands, and make a shell script called win, add its location to the PATH, and enable /challenge/run to find it!

Hint: /challenge/run runs as root and will call win. Thus, win can simply cat the flag file. Again, the win command is the only thing that /challenge/run needs, so you can just overwrite PATH with that one directory. But remember, if you do that, your win command won't be able to find cat.

You have three options to avoid that:

Figure out where the cat program is on the filesystem. It must be in a directory that lives in the PATH variable, so you can print the variable out (refer to Shell Variables to remember how!), and go through the directories in it (recall that the different entries are separated by :), find which one has cat in it, and invoke cat by its absolute path.
Set a PATH that has the old directories plus a new entry for wherever you create win.
Use read (again, refer to Shell Variables) to read /flag. Since read is a builtin functionality of bash, it is unaffected by PATH shenanigans.
Now, go and win!

## Solution: 
- Make a win shell script.

```
#!/bin/bash
/run/dojo/bin/cat /flag
```

- Make it executable, set PATH and run 

```sh
hacker@path~adding-commands:~$ chmod a+x /home/hacker/win
hacker@path~adding-commands:~$ PATH=/home/hacker
hacker@path~adding-commands:~$ /challenge/run
bash: sed: command not found
Invoking 'win'....
pwn.college{oBJeybT1OFlP3A_9hoUOrV46QYw.QX2cjM1wCM2kjNzEzW}
```

## Flag:
```
pwn.college{oBJeybT1OFlP3A_9hoUOrV46QYw.QX2cjM1wCM2kjNzEzW}
```

### References:
- https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix
- https://www.ionos.com/digitalguide/server/configuration/linux-cat-command/
- https://www.linuxjournal.com/content/how-set-or-modify-path-variable-linux

### Notes:
- If PATH is overwritten, use absolute command paths.
- win.sh file will not be run if system tries to run win. So we need to use a shebang.

# Challenge 5: Hijacking Commands
Armed with your knowledge, you can now carry out some shenanigans. This challenge is almost the same as the first challenge in this module. Again, this challenge will delete the flag using the rm command. But unlike before, it will not print anything out for you.

How can you solve this? You know that rm is searched for in the directories listed in the PATH variable. You have experience creating the win command when the previous challenge needed it. What else can you create?

## Solution: 
- The name suggests hijacking another flag.
- Since the rm command is run with root, name the file rm
- Save and change PATH to /home/hacker.
- /challenge/flag gives the flag instead of deleting.

```sh
hacker@path~hijacking-commands:~$ chmod a+x /home/hacker/rm
hacker@path~hijacking-commands:~$ PATH=/home/hacker
hacker@path~hijacking-commands:~$ /challenge/run
bash: sed: command not found
Trying to remove /flag...
pwn.college{AYC6rjafQg38JgjyBGcE2n77Yuf.QX3cjM1wCM2kjNzEzW}
```

## Flag:
```
pwn.college{AYC6rjafQg38JgjyBGcE2n77Yuf.QX3cjM1wCM2kjNzEzW}
```

### References:
- None

### Notes:
- We can hijack commands by changing path to different ones.

