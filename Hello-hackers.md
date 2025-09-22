# Challenge 1: Intro to Commands
In this challenge, you will invoke your first command! When you type a command and hit enter, the command will be invoked, as so:

```sh
hacker@dojo:~$ whoami
hacker
hacker@dojo:~$
```
Here, the user executed the whoami command, which simply prints the username (hacker) to the terminal. When the command terminates, the shell once again displays the prompt, ready for the next command.

In this level, invoke the hello command to get the flag! Keep in mind: commands in Linux are case sensitive: hello is different from HELLO.

## Solution: 
The challenge is to simply run a hello command in the terminal, and keep the lowercase in mind.

```sh
$ hello
Success! Here is your flag:
pwn.college{MF8NODijojPsDwj00GZywt8sF0k.QX3YjM1wCM2kjNzEzW}
```
## Flag:
pwn.college{MF8NODijojPsDwj00GZywt8sF0k.QX3YjM1wCM2kjNzEzW}

### References:
- None

### Notes:
- whoami command displays the role/name of the user.
- Commands are read and run linewise.
- Commands are fully case sensitive.

# Challenge 2: Intro to Arguments
Let's try something more complicated: a command with arguments, which is what we call additional data passed to the command. When you type a line of text and hit enter, the shell actually parses your input into a command and its arguments. The first word is the command, and the subsequent words are arguments. Observe:

```sh
hacker@dojo:~$ echo Hello
Hello
hacker@dojo:~$
```
In this case, the command was echo, and the argument was Hello. echo is a simple command that "echoes" all of its arguments back out onto the terminal, like you see in the session above.

Let's look at echo with multiple arguments:

```sh
hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
hacker@dojo:~$
```
In this case, the command was echo, and Hello and Hackers! were the two arguments to echo. Simple!

In this challenge, to get the flag, you must run the hello command (NOT the echo command) with a single argument of hackers. Try it now!

## Solution: 
This challenge consists of running a hello command with one single argument called hackers.

```sh
$ hello hackers
Success! Here is your flag:
pwn.college{MtxeIUivyJruS7d407EqG3_MPmn.QX4YjM1wCM2kjNzEzW}
```

## Flag:
pwn.college{MtxeIUivyJruS7d407EqG3_MPmn.QX4YjM1wCM2kjNzEzW}

### References:
- None

### Notes:
- Any command can have one or multiple arguments.
- Echo command works like a print and shows your arguments.

# Challenge 3: Command History
You're going to type a lot of commands, and typing everything from scratch can be annoying. Luckily, the shell saves a history of every command you invoke.

You can scroll through those saved commands with the up/down arrow keys, and we'll practice that in this challenge. This challenge will inject the flag into your history. Bring up a terminal, hit the up arrow, and grab it! In other challenges, the history will contain the log of the commands you've run, so if you need to run a similar command again, you can use the arrow keys to scroll through and find it!

## Solution:
We simply need to enter the terminal and click "Up Arrow". Doing so immediately reveals the flag without any more code.

```sh
$ the flag is pwn.college{4pYqUT_bm_zhN-O-4l5FwcsQhh1.0lNzEzNxwCM2kjNzEzW}
```

## Flag:
pwn.college{4pYqUT_bm_zhN-O-4l5FwcsQhh1.0lNzEzNxwCM2kjNzEzW}

### References:
- None

### Notes:
- Any command typed is saved into a command history within the terminal.
- Previous commands can be navigated using arrow keys.
  


