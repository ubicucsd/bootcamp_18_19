# Let's Talk Snake
#### Skill: Python

## The Big Picture

The command line can only take you so far when you're working with bioinformatic data. You'll often want to do more than the command line easily allows you to, which means it's time to write some code. This week, we're going to be doing that via a popular scripting language called Python. Let's get started.

(Side note: If you know a bit about Python, you'll know that there are two commonly used versions: python2 and python3. **They are VERY similar.** If you spend enough time doing bioinformatics, you're going to run into programs written for both versions, so being familiar with both is important. For this lesson, however, we're going to be using python2 because... well... we are.)

## Getting Started

Create a new directory (remmber: mkdir) wherever you are saving your work. Call it "week3". Enter the directory.

Python *should* already be installed on your workstations. Let's make sure: Type the following on the command line:
```shell
python
```
You should see something that looks like this (note that this was done on a Mac, so your output might differ slightly):
```shell
Python 2.7.10 (default, Oct  6 2017, 22:29:07) 
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.31)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

If you do not see this, let one of us know.   
If you do, you're ready to roll. Type exit(), and move on to the next section.

## How to Python

Before we get into the bioinformatics of Python, we're going to take a quick look at how Python code is written. Create a file called Hello.py. The ".py" extension signals that you will be writing in python. Inside the file put:
```python
print "Hello World"
```

Great! Now save + close the file, and run your newly-written program by typing the following on the command line:
```shell
python Hello.py
```

Because the "print" statement in Python outputs whatever follows it to the command line, you'll see your program saying "Hello world". That was boring... let's try something more interesting. Skim through the following program:
```python
# This is a comment in Python! Anything after a "#" in Python is ignored when executing.

# Here are two common data structures. They just store data together:

# 1. A list. This is a simple collection of items that's very similar to an array.
#    The first item ("Cool") is at index 0.
myList = ["Cool", "is", "Bioinformatics"]

# 2. A dictionary. This is a data structure that assigns a "key" to each "value".
#    The "key" here is before the colon, and the "value" comes after it.
myDictionary = {
    "first student": "Mary",
    "second student": "James",
    "third student": "Phil",
    "student count": 3
}

# Now, let's use our list to print "Bioinformatics is Cool".
print myList[2], myList[1], myList[0]

# Great! Let's print out the dictionary. 
# print myDictionary
```

Woah! That's a lot to take in. Make sure you really understand what's happening here. Follow the comments closely, and ask one of us if you have any questions. Copy-paste this code into a new file called "Data.py" and run the code the same way we ran "Hello.py". You should see "Bioinformatics is Cool".

At this point, you can remove the "#" from the start of the last line (this is called uncommenting). Your Python senses should tell you that this line will now print out myDictionary. Take a look at how myDictionary is defined above and make a guess about what should be printed when you run the program. Once you're ready, run the program.

Is this what you expected? Probably not! Your dictionary is out of order! This is because dictionaries in Python are unordered, so you can't access elements by doing `myDictionary[0]` like we did with myList. Instead, we need to use the name of the "key" inside the square brackets. Let's try this. On the line after `print myDicitonary` add:
```python
myDictionary["first student"]
```

What do you expect this will print? Run the program to check your answer. (Hint: It's "Mary").  

One last thing: indentation in Python **matters**. You'll have to apply this in the next exercise, so keep that in mind. Now, it's time for some bioinformatics.

## Loops, Loops, Loops

Say I have a fasta file that has some number of reads (make sure you remember fasta format or you'll have trouble with this exercise!). I want to write a Python program that ONLY outputs the header lines (the ones that start with ">"). How can I do it? Think about how you might start before moving forward.

```
-check every line-
  -if it starts with a ">"-
    -print the line-
```
This is one simple representation of how you could achieve this task. The real implementation, as we shall see, uses a loop.

First, however, we need to get our fasta file. Use the following command to get a sample fasta file in your working directory:

```shell

```

You'll notice this file is called "test.fasta". We can use this information to tell our Python program to read from the file. Let's do that: create a file called "Loop.py" and add this as the first line:
```python
file = open("test.fasta", "r")
```

This will open the file for "r"eading, and save that in a variable name called "file". Now let's use a loop to look at every line in the file:
```python
file = open("test.fasta", "r")

for line in file:
```

That last line is the syntax for starting a for loop in Python. Next, looking back at our pseudocode, we see that we need to check if a line starts with a ">". Luckily, Strings (which is how lines are stored) are indexed, meaning individual characters from them can be extracted using brackets (you might remember we did something similar above with lists!). 
```
file = open("test.fasta", "r")

for line in file:
  if line[0] == ">":
```

Pay close attention to the indentation here.

## Subsection for tasks

--

## What You've Learned

Skills developed + next steps. Applications.

## Credits and Citations
