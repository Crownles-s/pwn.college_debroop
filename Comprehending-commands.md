# Challenge 1: cat: not the pet, but the command!
One of the most critical Linux commands is cat. cat is most often used for reading out files, like so:

```sh
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
```

One of the most critical Linux commands is `cat`.
`cat` is most often used for reading out files, like so:
cat will concatenate (hence the name) multiple files if provided multiple arguments. For example:

```sh
hacker@dojo:~$ cat myfile
This is my file!
hacker@dojo:~$ cat yourfile
This is your file!
hacker@dojo:~$ cat myfile yourfile
This is my file!
This is your file!
hacker@dojo:~$ cat myfile yourfile myfile
This is my file!
This is your file!
This is my file!
```

Finally, if you give no arguments at all, cat will read from the terminal input and output it. We'll explore that in later challenges...

In this challenge, I will copy the flag to the flag file in your home directory (where your shell starts). Go read it with cat!

## Solution: 
The challenge is to use the cat command to read the flag file in home directory.

```sh
hacker@commands~cat-not-the-pet-but-the-command:~$ cat ~/flag
pwn.college{oj5a1UWuSfjd2Pn-jTmACCx4iXp.QXxcTN0wCM2kjNzEzW}
```

## Flag:
pwn.college{oj5a1UWuSfjd2Pn-jTmACCx4iXp.QXxcTN0wCM2kjNzEzW}

### References:
- None

### Notes:
- cat command concatenates 2 files.
- using only 1 file makes cat command read the file.

# Challenge 2: catting absolute paths
In the last level, you did cat flag to read the flag out of your home directory! You can, of course, specify cat's arguments as absolute paths:

```sh
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
```

In the last level, you did `cat flag` to read the flag out of your home directory!
You can, of course, specify `cat`'s arguments as absolute paths:
...
In this directory, I will not copy it to your home directory, but I will make it readable. You can read it with cat at its absolute path: /flag.

FUN FACT: /flag is where the flag always lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

## Solution: 
Following the inmstructions leads to the flag.

```sh
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{s5GKE12H3B5ALnN3vhQHl9IcODh.QX5ETO0wCM2kjNzEzW}
```

## Flag:
pwn.college{s5GKE12H3B5ALnN3vhQHl9IcODh.QX5ETO0wCM2kjNzEzW}

### References:
- None

### Notes:
- None

# Challenge 3: more catting practice
You can specify all sorts of paths as arguments to commands, and we'll practice some more with cat. In this 
level, I'll put the flag in some crazy directory, and I will not allow you to change directories with cd, so no cat flag for 
you. You must retrieve the flag by absolute path, wherever it is.

## Solution: 
- Entering terminal gave me the path. Normal cat command with the file path as the argument gave me the flag.

```sh
You cannot use the 'cd' command in this level, and must retrieve the flag by 
absolute path. Plus, I hid the flag in a different directory! You can find it 
in the file /usr/share/mysql/flag. Go cat it out **without** cding into that 
directory!
hacker@commands~more-catting-practice:~$ cat /usr/share/mysql/flag
pwn.college{gcWDG-9qoodf-4ysz6SDP_plaq8.QXwITO0wCM2kjNzEzW}
```

## Flag:
pwn.college{gcWDG-9qoodf-4ysz6SDP_plaq8.QXwITO0wCM2kjNzEzW}

### References:
- None

### Notes:
- cat command can read files from any absolute path regardless of user's presence in that directory.

# Challenge 4: grepping for a needle in a haystack
Sometimes, the files that you might cat out are too big. Luckily, we have the grep command to search for the contents we need! We'll learn it in this challenge.

There are many ways to grep, and we'll learn one way here:

```sh
hacker@dojo:~$ grep SEARCH_STRING /path/to/file
```

Invoked like this, grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

In this challenge, I've put a hundred thousand lines of text into the /challenge/data.txt file. grep it for the flag!                                                                                                                 

HINT: The flag always starts with the text pwn.college.

## Solution: 
- Running a normal grep command with pwn.college as the search string and the file path, both as arguments.

```sh
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{AptkdGfz5J2--5fN2kuArfr25LG.QX3EDO0wCM2kjNzEzW}
```

## Flag:
pwn.college{AptkdGfz5J2--5fN2kuArfr25LG.QX3EDO0wCM2kjNzEzW}

### References:
- None

### Notes:
- Grep command can search for lines containing a specific string within files and show them within the terminal.

# Challenge 5: comparing files
When looking for changes between similar files, eyeballing them might not be the most efficient approach! This is where the diff command becomes invaluable.

diff compares two files line by line and shows you exactly what's different between them. For example:

```sh
hacker@dojo:~$ cat file1
hello
world
hacker@dojo:~$ cat file2
hello
universe
hacker@dojo:~$ diff file1 file2
2c2
< world
---
> universe
```

The output tells us that line 2 changed (2c2), with world in the first file (<) being replaced by universe in the second file (>).

Sometimes, when new lines are added, you'll see something like:

```sh
hacker@dojo:~$ cat old
pwn
hacker@dojo:~$ cat new
pwn
college
hacker@dojo:~$ diff old new
1a2
> college
```

This tells us that after line 1 in the first file, the second file has an additional line (1a2 means "after line 1 of file1, add line 2 of file2").

Now for your challenge! There are two files in /challenge:

- /challenge/decoys_only.txt contains 100 fake flags
- /challenge/decoys_and_real.txt contains all 100 fake flags plus the one real flag

Use diff to find what's different between these files and get your flag!

## Solution: 
- First I entered the /challenge directory to get to the files.
- Next, the diff command immediately revealed the flag.

```sh
hacker@commands~comparing-files:~$ cd /challenge
hacker@commands~comparing-files:/challenge$ diff decoys_only.txt decoys_and_real.txt
41a42
> pwn.college{guOzJildrEY27XLLdgeeVStNaIC.01MwMDOxwCM2kjNzEzW}
```

## Flag:
pwn.college{guOzJildrEY27XLLdgeeVStNaIC.01MwMDOxwCM2kjNzEzW}

### References:
- None

### Notes:
- Diff command reveals any differences in files, and the location of those differences.

# Challenge 6: listing files
So far, we've told you which files to interact with. But directories can have lots of files (and other directories) inside them, and we won't always be here to tell you their names. You'll need to learn to list their contents using the ls command!

ls will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided. Observe:

```sh
hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$
```

In this challenge, we've named /challenge/run with some random name! List the files in /challenge to find it.

## Solution: 
- Using ls command showed us the new run file easily, to get the flag.

```sh
hacker@commands~listing-files:~$ ls /challenge
16717-renamed-run-18657  DESCRIPTION.md
hacker@commands~listing-files:~$ ^C
hacker@commands~listing-files:~$ /challenge/16717-renamed-run-18657
Yahaha, you found me! Here is your flag:
pwn.college{AjMGQsqk98YndlL93CnDGSFZQQP.QX4IDO0wCM2kjNzEzW}
```

## Flag:
pwn.college{AjMGQsqk98YndlL93CnDGSFZQQP.QX4IDO0wCM2kjNzEzW}

### References:
- None

### Notes:
- ls command lists all files in a directory.

# Challenge 7: touching files
Of course, you can also create files! There are several ways to do this, but we'll look at a simple command here. You can create a new, blank file by touching it with the touch command:

```sh
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ touch pwnfile
hacker@dojo:/tmp$ ls
pwnfile
hacker@dojo:/tmp$
```

It's that simple! In this level, please create two files: /tmp/pwn and /tmp/college, and run /challenge/run to get your flag!

## Solution: 
- Using touch command created the new files, and helped get the flag.

```sh
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ cd /
hacker@commands~touching-files:/$ /challenge/run
Success! Here is your flag:
pwn.college{skn9sN6XYzRkrJ9Xwa3bXHIPsj3.QXwMDO0wCM2kjNzEzW}
```

## Flag:
pwn.college{skn9sN6XYzRkrJ9Xwa3bXHIPsj3.QXwMDO0wCM2kjNzEzW}

### References:
- None

### Notes:
- touch command creates a new blank file.

# Challenge 8: removing files
Files are all around you. Like candy wrappers, there'll eventually be too many of them. In this level, we'll learn to clean up!

In Linux, you remove files with the rm command, as so:

```sh
hacker@dojo:~$ touch PWN
hacker@dojo:~$ touch COLLEGE
hacker@dojo:~$ ls
COLLEGE     PWN
hacker@dojo:~$ rm PWN
hacker@dojo:~$ ls
COLLEGE
hacker@dojo:~$
```

Let's practice. This challenge will create a delete_me file in your home directory! Delete it, then run /challenge/check, which will make sure you've deleted it and then give you the flag!

## Solution: 
- Using rm command deleted the required file, which helped get the flag.

```sh
hacker@commands~removing-files:~$ rm ~/delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{MHoC9wCBBMUc2oaLM000nSNCMlI.QX2kDM1wCM2kjNzEzW}
```

## Flag:
pwn.college{MHoC9wCBBMUc2oaLM000nSNCMlI.QX2kDM1wCM2kjNzEzW}

### References:
- None

### Notes:
- rm command deletes the file in the given path.

# Challenge 9: moving files
You can also move files around with the mv command. The usage is simple:

```sh
hacker@dojo:~$ ls
my-file
hacker@dojo:~$ cat my-file
PWN!
hacker@dojo:~$ mv my-file your-file
hacker@dojo:~$ ls
your-file
hacker@dojo:~$ cat your-file
PWN!
hacker@dojo:~$
```

This challenge wants you to move the /flag file into /tmp/hack-the-planet (do it)! When you're done, run /challenge/check, which will check things out and give the flag to you.

## Solution: 
- Using mv command to move the required file to the given destination, which helped get the flag.

```sh
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{sJ-Q7k-EcW_SLP1VZlEU83gjWeo.0VOxEzNxwCM2kjNzEzW}
```

## Flag:
pwn.college{sJ-Q7k-EcW_SLP1VZlEU83gjWeo.0VOxEzNxwCM2kjNzEzW}

### References:
- None

### Notes:
- mv command moves the target file to a target destination.

# Challenge 10: hidden files
Interestingly, ls doesn't list all the files by default. Linux has a convention where files that start with a . 
don't show up by default in ls and in a few other contexts. To view them with ls, you need to invoke ls with the -a flag, as so:

```sh
hacker@dojo:~$ touch pwn
hacker@dojo:~$ touch .college
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
hacker@dojo:~$
```

Now, it's your turn! Go find the flag, hidden as a dot-prepended file in /.

## Solution: 
- Using ls command with the -a argument to view hidden files.
- Using cat command to show the contents of the dot-prepended file. 

```sh
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv             bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-293042437024679  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ cat /.flag-293042437024679
pwn.college{8mDriZL_M_91DT6OAn1X-IQDuJR.QXwUDO0wCM2kjNzEzW}
```

## Flag:
pwn.college{8mDriZL_M_91DT6OAn1X-IQDuJR.QXwUDO0wCM2kjNzEzW}

### References:
- None

### Notes:
- ls -a command shows every file in a path, hidden or not.
- Dot-prepended file names make the file hidden.

# Challenge 11: An Epic Filesystem Quest
With your knowledge of cd, ls, and cat, we're ready to play a little game!

We'll start it out in /. Normally:

```sh
hacker@dojo:~$ cd /
hacker@dojo:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  dev        flag  lib   lib64  media   opt  root  sbin  sys  usr
```

That's a lot of contents! One day, you will be quite familiar with them, but already, you might recognize the flag file and the challenge directory.

In this challenge, I have hidden the flag! Here, you will use ls and cat to follow my breadcrumbs and find it! Here's how it'll work:

0. Your first clue is in /. Head on over there.
1. Look around with ls. There'll be a file named HINT or CLUE or something along those lines!
2. cat that file to read the clue!
3. Depending on what the clue says, head on over to the next directory (or don't!).
4. Follow the clues to the flag!
Good luck!

## Solution: 
- This challenge consisted of following clues.
- Self destructing clues should be found using ls and read by cat. No cd is nallowed
- Normal clues can be read by cd or the above method both.
- Case sensitivity must be kept in mind.

```sh
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
TRACE  boot       dev  flag  lib    lib64   media  nix  proc  run   srv  tmp  var
bin    challenge  etc  home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~an-epic-filesystem-quest:/$ cat /TRACE
Lucky listing!
The next clue is in: /usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/Gyre-Termes/Arrows/Regular

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/$ ^C
hacker@commands~an-epic-filesystem-quest:/$ ls -a /usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/Gyre-Termes/Arrows/Regular
.  ..  EVIDENCE-TRAPPED  Main.js
hacker@commands~an-epic-filesystem-quest:/$ cat /usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/Gyre-Termes/Arrows/Regular/EVIDENCE-TRAPPED
Lucky listing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/setuptools/_vendor/jaraco

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/$ cd ^C
hacker@commands~an-epic-filesystem-quest:/$ cd /usr/local/lib/python3.8/dist-packages/setuptools/_vendor/jaraco
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/setuptools/_vendor/jaraco$ ls
SNIPPET  __pycache__  collections  context.py  functools  text
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/setuptools/_vendor/jaraco$ cat SNIPPET
Yahaha, you found me!
The next clue is in: /usr/local/lib/python3.8/dist-packages/IPython/testing/plugin

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/setuptools/_vendor/jaraco$ ^C
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/setuptools/_vendor/jaraco$ cd  /usr/local/lib/python3.8/dist-packages/IPython/testing/plugin
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ ls
INFO        __init__.py  dtexample.py  pytest_ipdoctest.py  simple.py      test_combo.txt    test_exampleip.txt  test_refs.py
README.txt  __pycache__  ipdoctest.py  setup.py             simplevars.py  test_example.txt  test_ipdoctest.py
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ cat INFO
Congratulations, you found the clue!
The next clue is in: /usr/local/lib/python3.8/dist-packages/cle/backends/elf/__pycache__
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ ^C
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ ls -a /usr/local/lib/python3.8/dist-packages/cle/backends/elf/__pycache__
.                        compilation_unit.cpython-38.pyc  lsda.cpython-38.pyc        symbol.cpython-38.pyc
..                       elf.cpython-38.pyc               metaelf.cpython-38.pyc     symbol_type.cpython-38.pyc
BLUEPRINT                elfcore.cpython-38.pyc           regions.cpython-38.pyc     variable.cpython-38.pyc
__init__.cpython-38.pyc  hashtable.cpython-38.pyc         subprogram.cpython-38.pyc  variable_type.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ cat /usr/local/lib/python3.8/dist-packages/cle/backends/elf/__pycache__/BLUEPRINT
Yahaha, you found me!
The next clue is in: /usr/share/gtksourceview-4/styles
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ ^C
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ ls -a /usr/share/gtksourceview-4/styles
.  ..  LEAD  classic.xml  cobalt.xml  kate.xml  oblivion.xml  solarized-dark.xml  solarized-light.xml  styles.rng  tango.xml
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ cat /usr/share/gtksourceview-4/styles/LEAD
Great sleuthing!
The next clue is in: /opt/linux/linux-5.4/include/uapi/mtd

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ ^C
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ ls -a /opt/linux/linux-5.4/include/uapi/mtd
.  ..  CLUE-TRAPPED  inftl-user.h  mtd-abi.h  mtd-user.h  nftl-user.h  ubi-user.h
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ cat /opt/linux/linux-5.4/include/uapi/mtd/CLUE-TRAPPED
Congratulations, you found the clue!
The next clue is in: /usr/lib/jvm/java-11-openjdk-amd64/legal/java.management

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ ^C
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ ls -a /usr/lib/jvm/java-11-openjdk-amd64/legal/java.management
.  ..  ASSEMBLY_EXCEPTION  MEMO-TRAPPED
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ cat /usr/lib/jvm/java-11-openjdk-amd64/legal/java.management/MEMO-TRAPPED
Yahaha, you found me!
The next clue is in: /usr/share/perl/5.30.0/unicore/lib/Hyphen

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ ^C
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ ls -a /usr/share/perl/5.30.0/unicore/lib/Hyphen
.  ..  .CUE  T.pl
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$ cat /usr/share/perl/5.30.0/unicore/lib/Hyphen/.CUE
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{UKZ4uevSrZ428EjMKPFcBkDgff7.QX5IDO0wCM2kjNzEzW}
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/IPython/testing/plugin$
```

## Flag:
pwn.college{UKZ4uevSrZ428EjMKPFcBkDgff7.QX5IDO0wCM2kjNzEzW}

### References:
- None

### Notes:
- None
