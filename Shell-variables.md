# Challenge 1: 
Let's start with printing variables out. The /challenge/run program will not, and cannot, give you the flag, but that's okay, because the flag has been put into the variable called "FLAG"! Just have your shell print it out!

You can accomplish this using a number of ways, but we'll start with echo. This command just prints stuff. For example:

```sh
hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
```

You can also print out variables with echo, by prepending the variable name with a $. For example, there is a variable, PWD, that always holds the current working directory of the current shell. You print it out as so:

```sh
hacker@dojo:~$ echo $PWD
/home/hacker
```

Now it's your turn. Have your shell print out the FLAG variable and solve this challenge!

## Solution: 
- The challenge is simply to use echo command to print a variable called FLAG as per the given instructions.

```sh
hacker@variables~printing-variables:~s echo $FLAG
pwn.college{squhdWbJnZ8pkXFSehXNbGrkAM9.QX3UTN0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{squhdWbJnZ8pkXFSehXNbGrkAM9.QX3UTN0wCM2kjNzEzW}
```

### References:
- None

### Notes:
- We can print variables.
- Use $var to point a variable called var.

# Challenge 2: Setting Variables
Naturally, as well as reading values stored in variables, you can write values to variables. This is done, as with many other languages, using =. To set variable VAR to value 1337, you would use:

```sh
hacker@dojo:~$ VAR=1337
```

Note that there are no spaces around the =! If you put spaces (e.g., VAR = 1337), the shell won't recognize a variable assignment and will, instead, try to run the VAR command (which does not exist).

Also note that this uses VAR and not $VAR: the $ is only prepended to access variables. In shell terms, this prepending of $ triggers what is called variable expansion, and is, surprisingly, the source of many potential vulnerabilities (if you're interested in that, check out the Art of the Shell dojo when you get comfortable with the command line!).

After setting variables, you can access them using the techniques you've learned previously, such as:

```sh
hacker@dojo:~$ echo $VAR
1337
```

To solve this level, you must set the PWN variable to the value COLLEGE. Be careful: both the names and values of variables are case-sensitive! PWN is not the same as pwn and COLLEGE is not the same as College.

## Solution: 
- Assign COLLEGE value to variable PWN.
- This gives the flag.

```sh
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{Ey9hHvPV7M-Hh0CBLiVn5QiOO0W.QX5UTN0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{Ey9hHvPV7M-Hh0CBLiVn5QiOO0W.QX5UTN0wCM2kjNzEzW}
```

### References:
- None

### Notes:
- Again, everything is case sensitive.

# Challenge 3: Multi-word Variables
In this level, you will learn about quoting. Spaces have special significance in the shell, and there are places where you can't use them spuriously. Recall our variable setting:

```sh
hacker@dojo:~$ VAR=1337
```

That sets the VAR variable to 1337, but what if you wanted to set it to 1337 SAUCE? You might try the following:

```sh
hacker@dojo:~$ VAR=1337 SAUCE
```

This looks reasonable, but it does not work, for similar reasons to needing to have no spaces around the =. When the shell sees a space, it ends the variable assignment and interprets the next word (SAUCE in this case) as a command. To set VAR to 1337 SAUCE, you need to quote it:

```sh
hacker@dojo:~$ VAR="1337 SAUCE"
```

Here, the shell reads 1337 SAUCE as a single token, and happily sets that value to VAR. In this level, you'll need to set the variable PWN to COLLEGE YEAH. Good luck!

## Solution: 
- Set varianble PWN to "COLLEGE YEAH".
- Get the flag.

```sh
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{AAeIg3BS7wTM-0EMVShmsvVSe3i.QXwYTN0wCM2kjNzEzW}
```

## Flag:
```
pwn.college{AAeIg3BS7wTM-0EMVShmsvVSe3i.QXwYTN0wCM2kjNzEzW}
```

### References:
- None

### Notes:
- Using double quotes allows usage of spaces when defining variables.

# Challenge 4: Exporting Variables
By default, variables that you set in a shell session are local to that shell process. That is, other commands you run won't inherit them. You can experiment with this by simply invoking another shell process in your own shell, like so:

```sh
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ echo "VAR is: $VAR"
VAR is: 1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is:
```

In the output above, the $ prompt is the prompt of sh, a minimal shell implementation that is invoked as a child of the main shell process. And it does not receive the VAR variable!

This makes sense, of course. Your shell variables might have sensitive or weird data, and you don't want it leaking to other programs you run unless it explicitly should. How do you mark that it should? You export your variables. When you export your variables, they are passed into the environment variables of child processes. You'll encounter the concept of environment variables in other challenges, but you'll observe their effects here. Here is an example:

```sh
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ export VAR
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```

Here, the child shell received the value of VAR and was able to print it out! You can also combine those first two lines.

```sh
hacker@dojo:~$ export VAR=1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```

In this challenge, you must invoke /challenge/run with the PWN variable exported and set to the value COLLEGE, and the COLLEGE variable set to the value PWN but not exported (e.g., not inherited by /challenge/run). Good luck!

## Solution: 
- Set value of COLLEGE to PWN.
- Set and export value of PWN to COLLEGE.
- Run the command as given.

```sh
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great 
job! Here is your flag:
pwn.college{keiuurcLH0bp7SPVhAlMdmPgFQZ.QXyYTN0wCM2kjNzEzW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
```

## Flag:
```
pwn.college{keiuurcLH0bp7SPVhAlMdmPgFQZ.QXyYTN0wCM2kjNzEzW}
```

### References:
- None

### Notes:
- Export a variable cannecled var by using export var.
- This helps it be defined for all child cells too.

# Challenge 5: Printing Exported Variables
There are multiple ways to access variables in bash. echo was just one of them, and we'll now learn at least one more in this challenge.

Try the env command: it'll print out every exported variable set in your shell, and you can look through that output to find the FLAG variable!

## Solution: 
- Use env to print exported command.
- This gives a block of code.
- Manually searched for the flag.

```sh
hacker@variables~printing-exported-variables:~$ env
```
(Not including the entire block of useless things.)

## Flag:
```
pwn.college{U_v9qdFueZo71RA3YOcxhAs-Oat.QX4UTN0wCM2kjNzEzW}
```

### References:
- None

### Notes:
- env command potions all exported variables of a shell.

# Challenge 6: Storing Command Output
In the course of working with the shell, you will often want to store the output of some command into a variable. Luckily, the shell makes this quite easy using something called Command Substitution! Observe:

```sh
hacker@dojo:~$ FLAG=$(cat /flag)
hacker@dojo:~$ echo "$FLAG"
pwn.college{blahblahblah}
hacker@dojo:~$
```

Neat! Now, you practice. Read the output of the /challenge/run command directly into a variable called PWN, and it will contain the flag!

Trivia: You can also use backticks instead of $(): FLAG=`cat /flag` instead of FLAG=$(cat /flag) in the example above. This is an older format, and has some disadvantages (for example, imagine if you wanted to nest command substitutions. How would you do $(cat $(find / -name flag)) with backticks? The official stance of pwn.college is that you should use $(blah) instead of `blah`.

## Solution: 


```sh

```

## Flag:
```

```

### References:
- None

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
- None

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
- None

### Notes:
