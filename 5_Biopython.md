# Bioinformatics x Python

### 🔸 If this is your first time here, please check in with Mark to get an AWS account. Then, a board member can help you connect (SSH) to the cluster

### 🔸 Please fill out this sign-in sheet: https://goo.gl/forms/kOZMaXwCW4PAWRY42

### 🔸 The cluster is live on: [username]@TODO

## Introduction

This lesson is a continuation of our previous lesson, Intro to Python, located [here](https://github.com/sabeelmansuri/binf_crash_course/blob/master/3_Python.md). If you're having trouble following this tutorial, are new to Python, or just want a refresher, check that lesson out first.

## Setup

We're going to start by using a Python package called [Biopython](https://biopython.org/) to perform a few common bioinformatic tasks. We'll need to install Biopython (note: some of you will have done this last time, you can still run the following command again to be safe):

```
pip install biopython
```

Confirm that you've successfully downloaded the package by creating a file (remember your .py extension!), adding `from Bio.Blast import NCBIWWW` as the first line, and running the program via the command line. If nothing prints out, you're good. If you get a "traceback error," something is amiss.

## 

check with user input ex

not much of a walkthrough... why? -> background is in [Python lesson](https://github.com/sabeelmansuri/binf_crash_course/blob/master/3_Python.md), rest is up to you to figure out. this doc provides you with examples and guidelines on stuff we haven't covered (ie bioinformatics basics, unfamiliar python concepts, etc). 

parse fasta file

parse fastq file

connect to ncbi database... what does this mean? parse output

challenges

## Credits

Exercises are adapted from the official [Biopython tutorial textbook](http://biopython.org/DIST/docs/tutorial/Tutorial.pdf)