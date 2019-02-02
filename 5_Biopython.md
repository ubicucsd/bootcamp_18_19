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
 
 In reality, you're probably not going to be typing in your A-G-C-T's--you'll be using a fasta file containing them. 
 
 
Now to parse, we can load a fasta file to work with. Create a new file and import the SeqIO package:
 
 ```python
from Bio import SeqIO
for seq_record in SeqIO.parse("ls_orchid.fasta", "fasta"):
   print(seq_record.id)
   print(repr(seq_record.seq))
   print(len(seq_record))
```

 Before you run this program, take a guess what will print (confirm with a neighbor!). Were you right? If not, what printed and why?
 

## Complements and Transcription

You've probably heard of complement strands and transcription. If you haven't, here are two excellent sources: [transcription](https://www.khanacademy.org/science/biology/gene-expression-central-dogma/transcription-of-dna-into-rna/a/overview-of-transcription) and [complements](https://en.wikipedia.org/wiki/Complementarity_(molecular_biology)). Biopython can perform these actions too!

### Complements

Create a new file and import the Seq package again. Create a Seq object with a DNA strand of your choosing (A's C's G's and T's only!). Call the `complement()` method on your Seq object. What do you expect will print out? Does it?

### Transcription

**Make sure you understand transcription before moving on**

Copy and paste the following into a new file:

```python
from Bio.Seq import Seq
template_dna = Seq("ATGGCCATTGTAATGGGCCGCTGAAAGGGTGCCCGATAG")
```
You've been given a template DNA strand. Can you turn this into the transcribed RNA strand? 

**Hint: You'll need the `reverse_complement()` before you `transcribe()`**

## NCBI BLAST

We connected to the BLAST database last time (take a look if you haven't already!). The output, however, wasn't very nice. Biopython can clear that up for us. Let's get a new fasta file to BLAST. While you're inside your working directory type:

```shell
cp ~/../smansuri/NC_005816.fna .
```

Now, we'll run the BLAST:

```python
from Bio.Blast import NCBIWWW
from Bio.Blast import NCBIXML
result_handle = NCBIWWW.qblast("blastn", "nt", "8332116")
blast_record = NCBIXML.read(result_handle)
for alignment in blast_record.alignments:
  for hsp in alignment.hsps:
    if hsp.expect < 8.02643e-114:
      print("****Alignment****")
      print("sequence:", alignment.title)
      print("length:", alignment.length)
      print("e value:", hsp.expect)
      print(hsp.query[0:75] + "...")
      print(hsp.match[0:75] + "...")
      print(hsp.sbjct[0:75] + "...")
```
Run the program. You should look through this code and see why what prints, prints.

### 🔸 At this point, you've completed the first part of today's lesson. Move on to the next part on alignment located [here](TODO).



## Credits

Exercises are adapted from the official [Biopython tutorial textbook](http://biopython.org/DIST/docs/tutorial/Tutorial.pdf)
