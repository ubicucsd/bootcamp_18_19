# Your favorite rectangle: the terminal

#### Skill: Command line use

## Why should I learn this?

Quoting my PI: "ja, true, you need that shit."

Quoting the Linux book I read recently: "GUIs make easy tasks easy, while command line interfaces make difficult tasks possible"

Other reasons: It is the fastest way to deal with XXL sized files, much of the software in bioinformatics has no GUI, and any programmer should have a healthy relationship with their system. 

## How do I see what a command does?

Anytime you need a refresh on what a command does, type the command line with the --help option like so: ```ls --help```. If that does not work, try ```man ls```. I will go over why different commands have different help syntax in a bit. 

## Navigation, manipulation, and permission

In order to get started, we need to be able to do the same thing we do in a file explorer in the command line. You may find it inconvenient at first, but with time these commands become faster and more versatile than the file explorer's interface. 

The forward slashes in a terminal console represent directories, with the home directory being a ```~```. Your default folder on EC2 is your user folder, which is ```~/username```. This means the folder named after your username is a subfolder of the home folder, which is represented by ```~```. 

```mkdir```(make directory

```cd```(change directory) Type cd followed by the directory's path to navigate a terminal to that directory. ```.``` is current directory and ```..``` is the parent of the current directory. 

```ls```list files) prints out the contents of a directory. There are tons of options for this command - my favorite is ```ls -lah``` , since it prints the directory contents in list format(```-l```), includes hidden files/folders(```-a```), and makes the storage sizes more readable for humans(```-h```). 

```cp```copy) copies the file in the first argument to the directory in the second argument

```rm```remove) deletes a file. 

```mv```move) like copy, but the original file disappears. 

```grep``` looks for patterns in the text you feed it and returns the matches it finds. It can look through text files, the list of files in a repository and much much more. 

```wc```word count) counts things like lines, words, and characters

```chmod``` In order to execute files, you need permission to do so. When looking at the output of ```ls -lah``` , you will see something on the order of ```-rwxrw-r--```. This indicates that the owner has read, write, and execute permissions. The next three characters are group permissions, and the last three are permissions for everyone else. Change permissions with ```chmod XXX filename``` where each X is a number 1 through 7(first for owner, second for group, third for everyone else). 

***Permission	rwx	Binary***
7	read, write and execute	rwx	111
6	read and write	rw-	110
5	read and execute	r-x	101
4	read only	r--	100
3	write and execute	-wx	011
2	write only	-w-	010
1	execute only	--x	001
0	none	---	000

### Let's Get Some Random Software Working for us...

## Downloading 

# TODO: 
wait for EC2 to load in order to figure out which OS we're going to use. Based on that, go through the downloading utilities (curl/wget/apt-get). 

find an easy to install software package for bioinfo to make an example of. 

## Compilation

**shell scripts and python files** do not need compilation.

**java** compiles by ```javac filename.java```

**C** ```gcc -c filename.c``` to compile and assemble. 


## Execution

**/bin**(binaries) contains your executable files and shells. The computer has a list of folders it searches through to find executables when you type a command and the /bin directory is one of them. When you download software, you should place the executable file or a symbolic link into the /bin directory.

**shell script** a simple ```./executable``` will suffice to execute a script. 

**python** will automatically compile for you before executing with the command ```python filename.py```. 

**java** can be executed with ```java compiledfilename```

**C** is executed like a shell script ```./out```












