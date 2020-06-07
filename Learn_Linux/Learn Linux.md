# Learn Linux

A guided room designed to teach you the Linux basics!

IP for Room:  10.10.244.202


## SSH
Command to SSH
`ssh <user>@<host>`

Login as shiba1 with the password shiba1

`ssh shiba1@10.10.244.202`

## Basic Commands

#### Echo

`echo` This command is used to show your input echoed back to you within the dispaly this can be good for sending text to files.

#### Man

`man` This command is used to show the types of flags that can be used with a certain command 
1)
How would you output hello without a newline
``
echo -n hello
``

#### ls

`ls` This is the lsit command that can display files within a directory
`ls -a` Displays all files/directories including ones that start with .

1) 	
What flag outputs all entries
``
-A
``
2)
What flag outputs things in a "long list" format 
``
-l
``

#### Cat

`cat` Outputs the contents of files to the console

1)

What flag numbers all output lines?   
`-n` 

#### Touch

`touch` creates files

#### Runing a binary

`.` Current Directory
`..` Directory before the current directory
`~` The user's home directory

1)
How would you run a binary called hello using the directory shortcut . ?
``
./hello
``
2)
How would you run a binary called hello in your home directory using the shortcut ~ ?
``
~/hello
``
3)
How would you run a binary called hello in the previous directory using the shortcut .. ?
``
../hello
``

### Binary Shiba1
1)
What's the password for shiba2
``
pinguftw
``

#### SU

`su` command that allows you to change the user
1)
How do you specify which shell is used when you login?
``
-s
``

## Linux Operators

#### `>`
`>` output redirection, redirect the output of any command to a file

If you were to use this operator on a file that already exists, it would completely erase the contents of that file and replace it with the output from your command

1) 	
How would you output twenty to a file called test
``
echo twenty > test
``

#### `>>`

`>>` appends the output of a command to a file

#### &&

`&&` allows you to execute a second command after the first one has executed successfully.

#### &

`&` is a background operator. 

#### $

`$` denote environment variables

1)
How would you set nootnoot equal to 1111
``
export nootnoot==1111
``

2)
What is the value of the home environment variable
``
/home/shiba2
``

#### |

`|` also known as pipe. Allows you to take the output of a command and use it as input for a second command.

#### ;

`;` works a lot like &&, however it does not require the first command to execute successfully.

### Binary Shiba2
1)
What is shiba3's password
`happynootnoises`

### Advanced File Operations

#### chmod

`chmod` allows you to set the different permissions for a file, and control who can read it.

Digit	Meaning													rwx
1		That file can be executed								x
2		That file can be written to 							w
3		That file can be executed and written to 				wx
4		That file can be read 									r
5		That file can be read and executed						rx
6		That file can be written to and read 					rw
7		That file can be read, written to, and executed 		rwx

1st digit user that owns the file
2nd digit group that owns the file
3rd digit everyone else.

1)
What permissions mean the user can read the file, the group can read and write to the file, and no one else can read, write or execute the file?
``
460
``

2)
What permissions mean the user can read, write, and execute the file, the group can read, write, and execute the file, and everyone else can read, write, and execute the file.
``
777
``

#### chown

`chown` allows us to change the user and group for any file.
`chown user:group file`
You can only use chown if you are "above" that other user, meaning that chown is best done with the root(administrator) user.

1)
How would you change the owner of file to paradox
``
chown paradox file
``
2)
What about the owner and the group of file to paradox   
``
chown paradox:paradox file
``

3)
What flag allows you to operate on every file in the directory at once?    
``
-R
``

#### rm

`rm` means remove.
1)
What flag deletes every file in a directory
``
-r
``

2)
How do you suppress all warning prompts
``
-f
``
#### mv

`mv` allows you to move files from one place to another.

1)
How would you move file to /tmp
``
mv file /tmp
``
#### cp

`cp` instead of moving the file it duplicates(copies) it.

#### cd && mkdir

`cd` change the location of the current directory.

`mkdir` make a new directory to store files in

1)
Using relative paths, how would you cd to your home directory.
``
cd ~
``

2)
Using absolute paths how would you make a directory called test in /tmp
``
mkdir tmp/test
``

#### ln

`ln` has 2 operations:
	hard linking, which completely duplicates the file, and links the duplicate to the original copy. `ln source destination`
	symbolic linking(symlink) has no data in it at all, it's just a reference to another file. `ln -s <file> <destination>`
ls even shows that its a symbolic link with the arrow pointing to what the link is referencing.

1)
How would I link /home/test/testfile to /tmp/test
``
ln /home/test/testfile /tmp/test
``

#### find

`find` allows you to find files. find is recursive. 
`find /` list every file on the OS
`find dir -user` list every file owned by a specific user
`find dir -group` list every file owned by a specific group

1)
How do you find files that have specific permissions?
``
-perm
``

2)
How would you find all the files in /home
``
find /
``

3)
How would you find all the files owned by paradox on the whole system
``
find / -user paradox
``

#### grep

`grep` allows user to find data inside of data. 
`grep <string> <file>`
`grep <regular expression> <file>`
1)
What flag lists line numbers for every string found?
``
-n
``

2)
How would I search for the string boop in the file aaaa in the directory /tmp
``
grep boop /tmp/aaaa
``

### Binary Shiba3
1)
What is shiba4's password
``
test1234
``

## Miscellaneous 

#### Sudo and Whoami

`sudo` Linux's run as administrator button
`whoami` command that states your current user.


1)
How do you specify which user you want to run a command as.
``
-u
``

2)
How would I run whoami as user jen?
``
sudo -u jen whoami
``

3)
How do you list your current sudo privileges(what commands you can run, who you can run them as etc.) 
``
-l
``

#### Adding users and groups 

`adduser` 	only root has permissions to add users
`addgroup`  only root has permissions to add groups

`usermod -a -G <groups seperated by commas> <user>` adds a user to a group
`id` is a command that allows you to view basic information about a user

1)
How would I add the user test to the group test
``
sudo usermod -a -G test test
``

#### Nano

`nano <file you want to write to>` 
`^<key>` the `^` means control

#### Shell Scripting

`bash <file_name>.sh` runs shell script
The shebang MUST be in the beginning of the file

#####Shebang

the character sequence consisting of the characters number sign and exclamation mark (#!) at the beginning of a script

bash 		`#!/bin/bash`, `#!/usr/bin/env bash`
JavaScript 	`#!/usr/bin/env jsc`, `#!/usr/bin/env node`
Perl		`#!/usr/bin/env perl`, `#!/usr/bin/perl`
PHP			`#!/usr/bin/php` , `#!/usr/bin/env php`
python		`#!/usr/bin/env python`
python3		`#!/usr/bin/env python3`
Ruby 		`#!/usr/bin/env ruby`, `#!/usr/bin/ruby`

#### Important Files and Directories

`/etc/passwd`    - Stores user information - Often used to see all the users on a system
`/etc/shadow`    - Has all the passwords of these users
`/tmp`		     - Every file inside it gets deleted upon shutdown - used for temporary files
`/etc/sudoers`   - Used to control the sudo permissions of every user on the system
`/home` 	     - The directory where all your downloads, documents etc are
`/root`          - The root user's home directory
`/usr`           - Where all your software is installed
`/bin and /sbin` - Used for system critical files - DO NOT DELETE
`$PATH`          - Stores all the binaries you're able to run

#### Process

`ps` user created processes can be viewed
`ps -ef` View a list of all system processes
`kill <PID>`  stop processes

### root.txt

Finish this room off! What is the root.txt flag
``
ad91979868d06e19d8e8a9c28be56e0c
``