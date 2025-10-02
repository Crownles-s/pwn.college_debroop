# Challenge 1: Translating characters
One of the purposes of piping data is to modify it. Many Linux commands will help you modify data in really cool ways. One of these is tr, which translates characters it receives over standard input and prints them to standard output.

In its most basic usage, tr translates the character provided in its first argument to the character provided in its second argument:

```sh
hacker@dojo:~$ echo OWN | tr O P
PWN
hacker@dojo:~$
```

It can also handle multiple characters, with the characters in different positions of the first argument replaced with associated characters in the second argument.

```sh
hacker@dojo:~$ echo PWM.COLLAGE | tr MA NE
PWN.COLLEGE
hacker@dojo:~$
```

Now, you try it! In this level, /challenge/run will print the flag but will swap the casing of all characters (e.g., A will become a and vice-versa). Can you undo it with tr and get the flag?

## Solution: 
- Use tr to replace caps with normal and normal with caps.
- During execution, accidentally used extra spaces, which gave us an error.
- Removing spaces gives the flag.

```sh
hacker@data~translating-characters:~$ /challenge/run | tr abcdefghijklmnopqrstuvwxyz ABCDEFGHIJKLMNOPQRSTUVWXYZ ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz
tr: extra operand ‘ABCDEFGHIJKLMNOPQRSTUVWXYZ’
Try 'tr --help' for more information.
/challenge/run: line 3: echo: write error: Broken pipe
tr: write error: Broken pipe
/challenge/run: line 5: echo: write error: Broken pipe
hacker@data~translating-characters:~$ /challenge/run | tr abcdefghijklmnopqrstuvwxyzABC
DEFGHIJKLMNOPQRSTUVWXYZ ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz
yOUR CASE-SWAPPED FLAG:
pwn.college{w2RRqlImB5xte2ZcTM7yVmaa6XX.01MxEzNxwCM2kjNzEzW}
```

## Flag:
```
pwn.college{w2RRqlImB5xte2ZcTM7yVmaa6XX.01MxEzNxwCM2kjNzEzW}
```

### References:
- None

### Notes:
- tr is used for replacing characters.

# Challenge 2: Deleting characters
tr can also translate characters to nothing (i.e., delete them). This is done via a -d flag and an argument of what characters to delete:

```sh
hacker@dojo:~$ echo PAWN | tr -d A
PWN
hacker@dojo:~$
```

Pretty simple! Now you give it a try. I'll intersperse some decoy characters (specifically: ^ and %) among the flag characters. Use tr -d to remove them!

## Solution: 
- Delete the decoy commands as shown.
- Shows the flag.

```sh
hacker@data~deleting-characters:~$ /challenge/run | tr -d ^%
Your character-stuffed flag:
pwn.college{ct3xSugq1syI4nyYG0TAd5xx887.0FNxEzNxwCM2kjNzEzW}
```

## Flag:
```
pwn.college{ct3xSugq1syI4nyYG0TAd5xx887.0FNxEzNxwCM2kjNzEzW}
```

### References:
- None

### Notes:
- tr can also delete characters using -d.

# Challenge 3: Deleting newlines
A common class of characters to remove is a line separator. This happens when you have a stream of data that you want to turn into a single line for further processing. You can specify newlines almost like any other character, by escaping them:

```sh
hacker@dojo:~$ echo "hello_world!" | tr _ "\n"
hello
world!
hacker@dojo:~$
```

Here, the backslash (\) signifies that the character that follows it is a standin for a character that's hard to input into the shell normally. The newline, of course, is hard to input because when you typically hit Enter, you'll run the command itself. \n is a standin for this newline, and it must be in quotes to prevent the shell interpreter itself from trying to interpret it and pass it to tr instead.

Now, let's combine this with deletion. In this challenge, we'll inject a bunch of newlines into the flag. Delete them with tr's -d flag and the escaped newline specification!

Fun fact! Want to actually replace a backslash (\) character? Because \ is the escape character, you gotta escape it! \\ will be treated as a backslash by tr. This isn't relevant to this challenge, but is a fun fact nonetheless!

## Solution: 
- Deleting newlines as shown.
- Gives the flag.

```sh
hacker@data~deleting-newlines:~$ /challenge/run | tr -d "\n"
Your line-split flag: pwn.college{wOZ3HN1SYA-Qj2-vjN51VdGJWsI.0VNxEzNxwCM2kjNzEzW}
```

## Flag:
```
pwn.college{wOZ3HN1SYA-Qj2-vjN51VdGJWsI.0VNxEzNxwCM2kjNzEzW}
```

### References:
- None

### Notes:
- tr can delete newlines by -d "\n"

# Challenge 4: Extracting the first lines with head
In your Linux journey, you'll experience situations where you need to grab just the early output of very verbose programs. For this, you'll reach for head! The head command is used to display the first few lines of its input:

```sh
hacker@dojo:~$ cat /something/very/long | head
this
is
just
the
first
ten
lines
of
the
file
hacker@dojo:~$
```

By default, it shows the first 10 lines, but you can control this with the -n option:

```sh
hacker@dojo:~$ cat /something/very/long | head -n 2
this
is
hacker@dojo:~$
```

This challenge's /challenge/pwn outputs a bunch of data, and you'll need to pipe it through head to grab just the first 7 lines and then pipe them onwards to /challenge/college, which will give you the flag if you do this right! Your solution will be a long composite command with two pipes connecting three commands. Good luck!

## Solution: 
- Use head -n 7 after first pipe to get the flag.
- Pipe again to given location to get the output.
- Flag is the output.

```sh
hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n 7 | /challenge/college
Congratulations, you piped the right codes!
pwn.college{82SVFCSIvs59FT5NbD32_3VZF7s.0lNxEzNxwCM2kjNzEzW}
```

## Flag:
```
pwn.college{82SVFCSIvs59FT5NbD32_3VZF7s.0lNxEzNxwCM2kjNzEzW}
```

### References:
- None

### Notes:
- head -n k shows the first k lines of output.

# Challenge 5: Extracting specific sections of text
Sometimes, you want to grab specific columns of data, such as the first column, the third column, or the 42nd column. For this, there's the cut command.

For example, imagine that you have the following data file:

```sh
hacker@dojo:~$ cat scores.txt
hacker 78 99 67
root 92 43 89
hacker@dojo:~$
```

You could use cut to extract specific columns:

```sh
hacker@dojo:~$ cut -d " " -f 1 scores.txt
hacker
root
hacker@dojo:~$ cut -d " " -f 2 scores.txt
78
92
hacker@dojo:~$ cut -d " " -f 3 scores.txt
99
43
hacker@dojo:~$
```

The -d argument specifies the column delimiter (how columns are separated). In this case, it's a space character. Of course, it has to be in quotes here so that the shell knows that the space is an argument rather than a space separating other arguments! The -f argument specifies the field number (which column to extract).

In this challenge, the /challenge/run program will give you a bunch of lines with random numbers and single characters (characters of the flag) as columns. Use cut to extract the flag characters, then pipe them to tr -d "\n" (like the previous level!) to join them together into a single line. Your solution will look something like /challenge/run | cut ??? | tr ???, with the ??? filled out.

## Solution: 
- First,the code i tried gave a lot of errors. 

```sh
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d " " | tr -d "\n"
cut: you must specify a list of bytes, characters, or fields
Try 'cut --help' for more information.
/challenge/run: line 4: echo: write error: Broken pipe
```


-So, I tried the help command.

```sh
hacker@data~extracting-specific-sections-of-text:~$ cut --help
Usage: cut OPTION... [FILE]...
Print selected parts of lines from each FILE to standard output.

With no FILE, or when FILE is -, read standard input.

Mandatory arguments to long options are mandatory for short options too.
  -b, --bytes=LIST        select only these bytes
  -c, --characters=LIST   select only these characters
  -d, --delimiter=DELIM   use DELIM instead of TAB for field delimiter
  -f, --fields=LIST       select only these fields;  also print any line
                            that contains no delimiter character, unless
                            the -s option is specified
  -n                      (ignored)
      --complement        complement the set of selected bytes, characters
                            or fields
  -s, --only-delimited    do not print lines not containing delimiters
      --output-delimiter=STRING  use STRING as the output delimiter
                            the default is to use the input delimiter
  -z, --zero-terminated   line delimiter is NUL, not newline
      --help        display this help and exit
      --version     output version information and exit

Use one, and only one of -b, -c or -f.  Each LIST is made up of one
range, or many ranges separated by commas.  Selected input is written
in the same order that it is read, and is written exactly once.
Each range is one of:

  N     N'th byte, character or field, counted from 1
  N-    from N'th byte, character or field, to end of line
  N-M   from N'th to M'th (included) byte, character or field
  -M    from first to M'th (included) byte, character or field

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Report any translation bugs to <https://translationproject.org/team/>
Full documentation <https://www.gnu.org/software/coreutils/cut>
or available locally via: info '(coreutils) cut invocation'
```

Using this and some resources, I used another command.

```sh
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d' ' -f2 | tr -d '\n'
pwn.college{wsJi4ierdxuohPVOzIVarFT4Vtb.01NxEzNxwCM2kjNzEzW}
```

## Flag:
```
pwn.college{wsJi4ierdxuohPVOzIVarFT4Vtb.01NxEzNxwCM2kjNzEzW}
```

### References:
- https://www.gnu.org/software/coreutils/manual/
- https://tldp.org/

### Notes:
- None.

# Challenge 6: Sorting data
Files (or output lines of commands) aren't always in the order you need them! The sort command helps you organize data. It reads lines from input (or files) and outputs them in sorted order:

```sh
hacker@dojo:~$ cat names.txt
  hack
  the
  planet
  with
  pwn
  college
hacker@dojo:~$ sort names.txt
  college
  hack
  planet
  pwn
  the
  with
hacker@dojo:~$
```

By default, sort orders lines alphabetically. Arguments can change this:

- -r: reverse order (Z to A)
- -n: numeric sort (for numbers)
- -u: unique lines only (remove duplicates)
- -R: random order!
  
In this challenge, there's a file at /challenge/flags.txt containing 100 fake flags, with the real flag mixed among them. When sorted alphabetically, the real flag will be at the end (we made sure of this when generating fake flags). Go get it!

## Solution: 
- Use sort like given.
- Last flag is real.

```sh
hacker@data~sorting-data:~$ sort /challenge/flags.txt 
ovm.cnklege{4ZFa0y9NyK1uP8K0HHIHbcelJvj.0FM0MDOxvCM2kjNzEyW}
ovn.cokkdge{4ZFa0x9MyL1tP8K0IIIIbcfkJvi.0FL0MDNwvBM2jjMzEzW}
ovn.colkege{4ZEb0y9NxL1uP9L0IIIIbcelJvj.0FM0MDOwwCM1jiNyEzV}
ovn.colldgd{3ZFb0x9NyL1uO9L1IIHHbbflIvj.0EM0MDNxvBM2jiNzEyW}
.
.
.
pwn.college{4ZFb0y9NyL1uP9L1IIIIbcflJvj.0FM0MDOxwCM2kjNzEzW}
pwn.college{4ZFb0y9NyL1uP9L1IIIIbcflJvj.0FM0MDOxwCM2kjNzEzW}
```

## Flag:
```
pwn.college{4ZFb0y9NyL1uP9L1IIIIbcflJvj.0FM0MDOxwCM2kjNzEzW}
```

### References:
- None

### Notes:
- sort commands READS things in given order.
