# Phylogenetics
#### Skills: Biopython, phylogenetic analysis

#### SSH: 

Today's lesson is going to cover basic phylogenetic motifs as well as phylogenetic analysis in a Python environment. Let's get started!

## The Basics
### What is Phylogenetics?

At its core, phylogenetics is the study of finding evolutionary relationships between organisms. How, you ask? By looking for similarities (in our case, on the DNA level). Let's pose one such problem:

Imagine you're given five distinct organisms and are told to figure out how they're evolutionarily related (that is, how they evolved from one another). Two questions pop into your head: Why? and How?

### Why Do I Care?

The answer is twofold:

1. On a broader scale, an understanding of phylogenetics

### How Does it Work?

We need some shared, conserved mechanism of comparing the organisms... something like DNA! There are sequences in DNA that are highly conserved between organisms (usually sequences that code for absolutely essential parts of life) that are excellent candidates for comparison. For example, imagine you have three organisms with the following sequence of DNA in a conserved region:

```
1. ACGTG
2. ACGTC
3. ACGCC
```

We can compare the nucleotides at each position and find that 1 and 2 differ by one nucleotide, 2 and 3 differ by one nucleotide, but 1 and 3 differ by **two nucleotides**. This might lead you to conclude that the relationship between organisms 1 and 3 is the most evolutionarily distant.

*Note: In reality, these conserved sequences are much, much longer, and the analysis is far more robust than counting of a few nucleotides.*

## Biopython

If you're not familiar with Biopython, please skim our previous lesson [here](https://github.com/sabeelmansuri/binf_crash_course/blob/master/4_Biopython.md). You'll need to have Biopython installed to continue. Confirm by running a Python program with the following:

```python
from Bio import Phylo
```

If nothing shows up during execution, you're good to go!

## XML



## Working with Trees



## So, Um, Why Do I Care?



## The Challenge

## Acknowledgements
Many data and algorithms are adatpted from the offical Biopython textbook.
