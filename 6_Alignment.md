# The First Bioinformatics Problem: Alignment

#### Skill: More python and some knowledge of alignment methodology

Every bioinformatics tool needs to start somewhere, and beyond quality control the first step most tools require is to make sequences comparable by aligning them. Once the sequences have been aligned, you can start looking at which nucleotides differ, locate deletions/insertions, and much more. Today we will look at the classic pairwise alignment tool available from bioPython.

## Why does an alignment look like it does?

In order to see why alignments are useful on a larger scale, let us start by looking at them from a smaller scale. 

First, import the ```pairwise2``` module from the BioPython library and the ```format_alignment``` method from the ```pairwise2``` module. **HINT: look at part 5 to find the correct import syntax**

Now, define two small strings containing DNA sequences. I recommend using "TGCCTTAG" and "TGCTTGC" for an easy to look at example. Call the default pairwise alignment method, called 

```pairwise2.align.globalxx()``` 

on those two strings. The alignment method returns a list of the most high scoring(good) alignments. You can print those out by iterating through the alignments with a for-each loop and print them out one by one. In order to make the alignments look a little nicer, you can put them through a formatting method before printing:

```print(format_alignment(*alignment_name))```

What is that asteriks? In different languages an asteriks has different meanings, but in Python it denotes a variable quantity of arguments. In other words, methods that want this asteriks are capable of accepting either one, maybe two, or maybe more arguments(inputs). 

### What exactly is a good score? Why is one alignment better than another? 

Glad you asked! If you look at the score printed out below each alignment, you will notice that the score is coincidentially identical to the number of nucleotides that match between the two aligned sequences. The way we determine the alignment with the optimal score is beyond the scope of what I plan to discuss, but it is good to know that alignments are mostly determined by the way a program decides on alignment scores. The alignment we tried gives gaps, insertions, and deletions a score of zero and matches a score of one. Other alignments may have more complex behaviors, including negative scores for insertions/deletions, custom scores based on which nucleotide is mismatched with which, and more. If you want to explore how different scoring systems look like in alignment, take a look [over here.](http://biopython.org/DIST/docs/api/Bio.pairwise2-module.html)