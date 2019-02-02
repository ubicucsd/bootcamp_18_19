# Bioinformatics x Python

### 🔸 If this is your first time here, please check in with Mark to get an AWS account. Then, a board member can help you connect (SSH) to the cluster

### 🔸 Please fill out this sign-in sheet: https://goo.gl/forms/kOZMaXwCW4PAWRY42

### 🔸 The cluster is live on: [username]@ec2-13-58-151-200.us-east-2.compute.amazonaws.com

## Introduction

This lesson is a continuation of our previous lesson, Intro to Python, located [here](https://github.com/sabeelmansuri/binf_crash_course/blob/master/3_Python.md). If you're having trouble following this tutorial, are new to Python, or just want a refresher, check that lesson out first.

## Setup

We're going to start by using a Python package called [Biopython](https://biopython.org/) to perform a few common bioinformatic tasks. We'll need to install Biopython (note: some of you will have done this last time, you can still run the following command again to be safe):

```shell
pip install biopython
```

Confirm that you've successfully downloaded the package by creating a file (remember your .py extension!), adding `from Bio.Blast import NCBIWWW` as the first line, and running the program via the command line. If nothing prints out, you're good. If you get a "traceback error," something is amiss.

## Sequences

### Seq objects

The first thing you think of when you hear "genetic data" is probably a sequence of DNA, which is a string of nucleotides (A's C's G's and T's). Let's use Biopython to work with sequences. Create a file to work in.

First, import the Seq package:

```python
 from Bio.Seq import Seq
 ```
 
 Next, create a Seq object (think of that as a sequence) and assign it to a dna variable:
 ```python
 dna = Seq("AGTACACTGGT")
 ```
 
 Now, print out that variable:
 ```python
 print dna
 ```
 
 ### Loading sequences
 
 In reality, you're probably not going to be typing in your A-G-C-T's--you'll be using a fasta file containing them. To do this, we can load a fasta file to work with. Create a new file and import the SeqIO package:
 
 ```python
from Bio import SeqIO
for seq_record in SeqIO.parse("ls_orchid.fasta", "fasta"):
   print(seq_record.id)
   print(repr(seq_record.seq))
   print(len(seq_record))
```
 
 
 

check with user input ex

not much of a walkthrough... why? -> background is in [Python lesson](https://github.com/sabeelmansuri/binf_crash_course/blob/master/3_Python.md), rest is up to you to figure out. this doc provides you with examples and guidelines on stuff we haven't covered (ie bioinformatics basics, unfamiliar python concepts, etc). 

parse fasta file

parse fastq file

connect to ncbi database... what does this mean? parse output

challenges

## Credits

Exercises are adapted from the official [Biopython tutorial textbook](http://biopython.org/DIST/docs/tutorial/Tutorial.pdf)
