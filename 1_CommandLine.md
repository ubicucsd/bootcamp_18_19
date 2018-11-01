# Your favorite rectangle: the terminal

#### Skill: UNIX/Command Line

The previous doc we went over included some information on alignment. This lesson will teach command line skills which will allow us to use alignment software. There are an endless number of commands, each with a ridiculous amount of options, so **do NOT attempt to memorize on the first try**. Use the commands listed below as a reference to look at. Actually learning (or memorizing) the commands comes from repeated use of the terminal. Same goes for the tool installation process we will go through. This course is supposed to be all about these tools, so we will have much more practice with handling them. Think of this as an introduction, a reference sheet, and generalized example.


## But first... EC2

I set up accounts for everyone based on the usernames from last time. Click [here](https://docs.google.com/spreadsheets/d/1M4S22RieI7GnJqGJZo_4flSU3FzP7ypCqrNSjZ-rf9w/edit?usp=sharing) for the list of usernames.

**Windows:** Open putty, paste ```my_username@ec2-52-15-126-191.us-east-2.compute.amazonaws.com``` into the Host Name section and select port 22 and SSH on that same page. Type a name under Saved Sessions and click the Save icon on the right. Now, press Open and type your username and password when prompted. 

**Mac or Linux:** Right click anywhere and click open terminal. You should see a prompt that looks something like  ```mchernys@mchernys-ThinkPad-T430:~/Desktop$```. Next, copy paste this command into the terminal and press enter ```ssh my_username@ec2-52-15-126-191.us-east-2.compute.amazonaws.com```. Note: use Ctrl-shift-V to paste into terminal. Please replace "your-username" with your actual username. Save the command you used somewhere so you can copy paste it in the future. 

---

### TODO

Right now, everyone's passowrd is ubic2018 but you probably have your own password in mind for your account. Type ```passwd username``` and follow the prompts to set your own password. 

---

Discover your identity. Type `whoami` into the window that just opened up and hit `enter`. And just like that you're talking
with your computer, you bioinformatician, you.

## Why should I learn this?

Quoting Mark's PI: "ja, true, you need that shit."

Other reasons: It is the fastest way to deal with XXL sized files, much of the software in bioinformatics has no Graphical User Interface (GUI), and any programmer should have a healthy relationship with their system.  

## How do I see what a command does?

Anytime you need a refresh on what a command does, type the command line with the --help option like so: ```ls --help```. If that does not work, try ```man ls```. I will go over why different commands have different help syntax in a bit. 

## Navigation, manipulation, and permission

In order to get started, we need to be able to do the same thing we do in a file explorer in the command line. You may find it inconvenient at first, but with time these commands become faster and more versatile than the file explorer's interface. 

The forward slashes in a terminal console represent directories, with the home directory being a ```~```. Your default folder on EC2 is your use folder, which is ```~/username```. This means the folder named after your username is a subfolder of the home folder, which is represented by ```~```. 

```cd```(change directory) Type cd followed by the directory's path to navigate a terminal to that directory. ```.``` is current directory and ```..``` is the parent of the current directory. 

```ls```(list files) prints out the contents of a directory. There are tons of options for this command - my favorite is ```ls -lah``` , since it prints the directory contents in list format(```-l```), includes hidden files/folders(```-a```), and makes the storage sizes more readable for humans(```-h```). 


```mkdir```(make directory) Creates a directory with the same name as the argument you give it. 

---

### TODO: Make a Software Folder

Navigate your terminal to your home directory (the directory named after your UCSD username) using ```cd```. Type ```mkdir software``` and press enter. Type ```ls``` to see the changes you have made. The reason for a software folder is to... keep your software in it. 

*Note: Usually, you would place executables in the /bin system folder, but you are not the admin so you cannot access that folder :( . This is often the case when you ssh into a system, so get used to having a dedicated software folder.*

---

```cp```(copy) copies the file in the first argument to the directory in the second argument. ```cp file1.txt file2.txt``` makes a copy of file1.txt called file2.txt in the same location. ```cp file1.txt ..``` places a copy of file1.txt (called file1.txt) into the parent directory. 

```rm```(remove) deletes a file. Careful with this one, there is no convenient command to remove files from the trash on linux. Once deleted, gone forever. ```rm file.txt```

```mv```(move) like copy, but the original file disappears. 

```wc```(word count) counts things like lines, words, and characters. ```wc -l file.txt``` prints the number of lines in file.txt. 

```chmod``` In order to execute files, you need permission to do so. When looking at the output of ```ls -lah``` , you will see something on the order of ```-rwxrw-r--```. This indicates that the owner has read, write, and execute permissions. The next three characters are group permissions, and the last three are permissions for everyone else. Change permissions with ```chmod XXX filename``` where each X is a number 1 through 7 (first for owner, second for group, third for everyone else).

***Permission	rwx	Binary***
7	read, write and execute	rwx	111
6	read and write	rw-	110
5	read and execute	r-x	101
4	read only	r--	100
3	write and execute	-wx	011
2	write only	-w-	010
1	execute only	--x	001
0	none	---	000

```scp```(secure copy) is a command used to copy files from one machine to another. The first argument is the source location, while the second argument is the destination. 

## Downloading

```curl``` Will download stuff for you. The most simple and relevant combination of options is ```curl -L https://examplelink.com -outdir .``` which will download from https://examplelink.com into the current directory (indicated by the dot). 

```apt-get```Handles packages from the apt library for Debian based systems. However, this installs packages system-wide so you are not going to be able to use it on EC2. The mac equivalent is homebrew. ```sudo apt-get install google-chrome-stable``` will install chrome. 

---

### TODO: Get Mafft

One of the gold standard alignment programs available today is called mafft. Let's download it into your software directory. First, you will need to find the download page online. Google search for mafft (any profession nowadays has plenty of googling, I am sure you are used to it). Right click on the download link and press "copy link address." Next, use the format presented in the curl example to download the contents of that link. 

---

## Unpackaging

Much of the data people want to download is large, but they want it fast. That's why things like .zip, .tar, .gz and such exist. Those are the file extensions of compressed data. In order to make software work, it must be unpackaged.

```tar```(tape archive) Is the command linux uses to package and unpackage stuff. This command has an incomprehensible amount of confusing options, so let me just copy paste the ones you should care about. ```tar -xvf file.tar.gz -C .``` unpacks a .tar.gz file into the current directory and ```tar -xvf -C .``` unpacks a .tar file into the current directory. The -C option indicates the files' destination.

---

### TODO: Unpackage and explore your Mafft software

---

## Compilation

What is compilation? It is the conversion of one programming language into another. Typically, it is a conversion of what's known as a high-level language (C, Java, Python, etc) to a low level language (binary, assembly). CPUs understand only very very very basic logic, so a super smart program called a compiler has to convert your convoluted and messy code into the simple delicious porridge that the CPU can eat(execute).

**shell scripts and python files** do not need compilation.

**java** compiles by ```javac filename.java```

**C** ```gcc -c filename.c``` to compile and assemble. 

Note: Much of the time, software you download online is already in binary form so there is no need to compile. This is not always the case!

## Execution

**/bin**(binaries) contains your executable files and shells. The computer has a list of folders it searches through to find executables when you type a command and the /bin directory is one of them. When you download software, you should place the executable file or a symbolic link into the /bin directory.

**shell script** a simple ```./executable``` will suffice to execute a script. 

**python** will automatically compile for you before executing with the command ```python filename.py```. 

**java** can be executed with ```java compiledfilename```

**C** is executed like a shell script ```./out```

## Tying It All Together 

### Piping 

Piping is stringing multiple commands together to perform some larger task. You can string commands together using the `|` symbol like so:

```
cat file.txt | grep "hello"
```

This will first perform the `cat` command: it will attempt to print everything inside file.txt to the terminal, but the pipe symbol `|` will stop it. Instead, everything from file.txt will get pushed through the `grep` command, which will print out any line that contains "hello". The result is only the lines containing "hello" in file.txt will be printed out.

## Getting yer feet wet

Here are a quick batch of tasks/exercises using the command line (and different commands) in roughly increasing order of difficulty:

##### (0.) Copy-paste the following command into your terminal and hit enter. Use `ls` to see the new directory it creates: `CP COMMAND HERE` 

##### 1. Enter the new directory (hint: use `cd`)

##### 2. Name all of the files (not other directories!) inside this directory. How many are there? (hint: use `ls`)

##### 3. How many lines are in file1.txt? (hint: use `wc`)

##### 4. Do any lines inside file2.txt contain the word "boop"? (hint: use `grep`)

##### 5. How many lines inside file2.txt contain the word "boop"? (hint: use a pipe of `grep` and `wc`)

##### 6. (Challenge 1) Read mystery.txt. There's a hidden message somewhere! Follow the instructions to find it.

##### 7. (Challenge 2) Attempt to delete the directory you downloaded in step 0. This directory is called "parent".
