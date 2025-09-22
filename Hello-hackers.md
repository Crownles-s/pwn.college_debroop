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
- commands are read and run linewise.
- commands are fully case sensitive.

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
- any command can have one or multiple arguments.
- echo command works like a print and shows your arguments.



