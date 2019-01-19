# Intro to Python
#### Skill: Python

## The Big Picture

So far, we've been working with bioinformatic data only on the command line. However, you'll often want to do more than the command line easily allows. Today, we're going to be learning the basics of one of the most popular languages for doing that: Python.

(Side note: If you know a bit about Python, you'll know that there are two commonly used versions: python2 and python3. **They are VERY similar.** You're going to run into programs written for/in either version, so being familiar with both is important. For this lesson, however, we're going to be using python2 because... well... we are.)

## Getting Started

Create a new directory (remmber: mkdir) wherever you are saving your work. Call it "pydir". Enter the directory.

Python should already be installed on your workstations. Let's make sure: Type the following on the command line:
```shell
python
```
You should see something that looks like this (note that this lesson was created on a Mac, so your output might differ slightly):
```shell
Python 2.7.10 (default, Oct  6 2017, 22:29:07) 
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.31)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

If you do not see something similar to this, let one of us know.   
If you do, you're ready to roll. Type exit(), and move on.

## How to Python

### Hello World!
We're going to start by taking a quick look at how Python code is written. Create a file called Hello.py. The ".py" extension signals that you will be writing in python. Inside the file put:
```python
print "Hello World"
```

Great! Now save + close the file, and run your newly-written program by typing the following on the command line:
```shell
python Hello.py
```

##### vim-hint: If you're using vim, press "i" to enter insert mode, type your code, press "esc" to exit insert mode (and enter command mode), and type ":x" to save and close. 

Because the "print" statement in Python outputs whatever follows it to the command line, you'll see your program print "Hello World". That was pretty trivial... let's try something more interesting.

### Basic syntax

You'll need to obtain a file I've written and add it to your "pydir" directory. Using the `cp` command, and knowing that the file is currently located in `~/../smansuri/syntax.py`, copy the file into your "pydir" directory.

Now, open the syntax.py file and take a look inside.

Make sure you understand what's happening. Follow the comments closely, and ask one of us if you have any questions.

Now, run the code the same way we ran "Hello.py". You should see "Bioinformatics is Cool". Can you edit line 14 to make the program print: "is Bioinformatics Cool"?

##### vim-hint: navigate to a specific line in vim by going into command mode and typing ```:14```

At this point, you can remove the "#" from the start of the last line (this is called uncommenting). Your Python senses should tell you that this line will now print out myString. Take a look at how myString is defined above and take a guess about what should be printed when you run the program. Once you're ready, run the program.

What if you only wanted to print *part* of your string, not the whole thing? Remember that a string is like a list (with the first character at index 0). So, what if we wanted to print just "Hello"? We can use specify a range of indexes to print from like so:

``` python
print myString[0:5]
```

Note that the first number is the position of the first character printed (0 = 'H'), while the second number is **PAST** the last character printed (5 = ' ', but we only print up to index 4).

## Indentation 

Indentation in Python **matters**. Try adding a second print statement your "Hello.py" file so it looks like this:
``` python
print "Hello World"
    print "Indented line"
```

Now, try to run "Hello.py". Python will complain that there's a problem with your indentation (there was no need to indent, but you did anyways). You'll learn more about when to indent in the next section. Speaking of which, it's time for some bioinformatics.

## Loop-D-Loop

Say I have a fasta file that has some number of reads (make sure you remember fasta format or you'll have trouble with this exercise!). I want to write a Python program that ONLY outputs the header lines (the ones that start with ">"). How can I do it? Think about how you might start before continuing.

```
-check every line-
  -if it starts with a ">"-
    -print the line-
```
This is one simple **representation** of how you could achieve this task. The **implementation** in Python, as we shall see, uses a loop. Which one of the three pseudocode lines above suggests we will need a loop?

First, however, let's get a sample fasta file. Use the following command to download it straight in your working directory:

```shell
cp /srv/Winter19/gencode.vM17.lncRNA_transcripts_subsampled.fasta . 
```

Check the contents of your directory. You should see a file called "test.fasta". 

Let's make a Python program that reads from this file. Create a new file called "Loop.py" and add this as the first line:
```python
file = open("test.fasta", "r")
```

This will open the file (test.fasta) for "r"eading, and give you access to test.fasta in a variable called "file". Now let's use a loop to look at every line in the file:
```python
file = open("test.fasta", "r")

for line in file:
```

That last line is the syntax for starting a for loop in Python. Next, looking back at our pseudocode, we see that we need to check if a line starts with a ">". Luckily, lines in a file are stored as strings! Remember that strings are indexed, meaning individual characters from them can be extracted using brackets (you might remember we did something similar above with!). 
```
file = open("test.fasta", "r")

for line in file:
  if line[0] == ">":
```

Pay close attention to the indentation here. **You can think of everything that's indented after the `for` as being "inside" of the for loop** (it looks a bit like that too!). In our example, that means the `if` code is executed for every line in the file.

Finally, we just specify that we want the line printed if the line does start with ">". We indent the next line so Python knows it's part of the "if" statement, and...

```
file = open("test.fasta", "r")

for line in file:
  if line[0] == ">":
    print line
```

Run Loop.py and see what happens. Voila

## Your turn! (Part I)

Here's a warm up. You're going to print your name using the alphabet. Declare a variable that holds a string containing
all 26 letters of the alphabet (just use the declaration provided below for simplicity). Then, on the next line use one print statement that accesses letters in the alphabet variable to print out your name.

```
"ABCDEFGHIJKLMNOPQRSTUVWXYZ "
```

## Your turn! (Part II)

That was easy, let's try something a little more challenging. Grab a sample fastq file using

```shell
wget or curl [TODO]
```

Now, write a program that outputs **ONLY** the lines containing actual genetic sequences (remember loops!). There are various ways to implement this, pick any that works for you.

#### Challenge 1

Try finding the total number of bases (A/T/C/G) that are in this file. Again, many implementations are possible--pick any that works for you.


#### Challenge 2



## What You've Learned

Skills developed + next steps. Applications.

## Credits and Citations
