# The First Bioinformatics Problem: Alignment

#### Skill: More python and some knowledge of alignment methodology

Every bioinformatics tool needs to start somewhere, and beyond quality control the first step most tools require is to make sequences comparable by aligning them. Once the sequences have been aligned, you can start looking at which nucleotides differ, locate deletions/insertions, and much more. Today we will look at the classic pairwise alignment tool available from bioPython.

## Why does an alignment look like it does?

In order to see why alignments are useful on a larger scale, let us start by looking at them from a smaller scale. 

### Global Alignment

In this case, the word "global" just means that the entire first string is aligned as best as possible to the entire second string. 

First, make a file called ```aligners.py``` and import the ```pairwise2``` module from the BioPython library and the ```format_alignment``` method from the ```pairwise2``` module. **HINT: look at part 5 to find the correct import syntax**

Now, define two small strings containing DNA sequences. I recommend using ```TGCCTTAG``` and ```TGCTTGC``` for an easy to look at example. Call the default pairwise alignment method, called 

```pairwise2.align.globalxx()``` 

on those two strings. The alignment method returns a list of the most high scoring(good) alignments. You can print those out by iterating through the alignments with a for-each loop and print them out one by one. In order to make the alignments look a little nicer, you can put them through a formatting method before printing:

```print(format_alignment(*alignment_name))```

What is that asteriks? In different languages an asteriks has different meanings, but in Python it denotes a variable quantity of arguments. In other words, methods that want this asteriks are capable of accepting either one, maybe two, or maybe more arguments(inputs). 

### What exactly is a good score? Why is one alignment better than another? 

Glad you asked! If you look at the score printed out below each alignment, you will notice that the score is coincidentially identical to the number of nucleotides that match between the two aligned sequences. The way we determine the alignment with the optimal score is beyond the scope of what I plan to discuss, but it is good to know that alignments are mostly determined by the way a program decides on alignment scores. The alignment we tried gives gaps, insertions, and deletions a score of zero and matches a score of one. Other alignments may have more complex behaviors, including negative scores for insertions/deletions, custom scores based on which nucleotide is mismatched with which, and more. There are several modes of alignment available on BioPython, each with customizable scoring. Look [over here] (http://biopython.org/DIST/docs/api/Bio.pairwise2-module.html) if you want to see the range of what BioPython has to offer.

### Local Alignment

The word "local" means the best alignment between two *subsequences*. This method can be used when looking for a conserved gene between two otherwise very different organisms. Aligning the messy differences between two different species is not useful, but finding two subsequences (two genes) that the species have in common without aligning the whole sequences can be very useful. 

Open up ```aligners.py``` and create strings ```ATGCGGCCATTATAAGCGGTCTCT``` and ```GATTATAATT```. Now, let's compare how these strings align with globally vs locally. The point is best illustrated when gaps and mismatches are penalized, so indicate the scoring system of the alignment like this: 

```pairwise2.align.localms(str1, str2, 1, -1, -1, -1)```
```pairwise2.align.globalms(str1, str2, 1, -1, -1, -1)```

The numbers at the end indicate +1 for matches, -1 for mismatches, -1 for opening a gap, and -1 for extending a gap. 

Looking at the matching nucleotides in global and local alignments of these string, which one makes more sense? Does it make sense to care about the matches the global alignment has at the very end of the sequences? 

## Multiple Sequence alignment 

Multiple sequence alignment aligns multiple sequences, but its inner workings are bit complicated (my way of saying I do not know them well enough to teach them) so we are just going to look at them from a distance. This type of alignment is used on a large number of more or less related sequences in order to infer homology and build evolutionary trees. My multiple sequence aligner of choice is mafft, which we will be using in the challenge below. 

## Codon Alignment - A bit more hands on

There has been much explaining and not much doing, so this section is for you to get your hands wet with alignment. One thing that biologists care a lot about is the way amino acids change through time. This is found by sequencing DNA at several timepoints, codon aligning various timepoints, and comparing timepoints to see which amino acids change at what time. Picking this topic is no coincidence, if you want to see the application my lab has made for this type alignment head [over here](http://flea.murrell.group/view/P018/sequences/). The sequences shown here are from an HIV envelope. If you click on on amino acid index, you can see a graph showing how the amino acid in that position evolved over time. You can explore the site - I recommend the tree section because it is pretty. I did not make this specific page, I am currently finishing up a webapp that will generate these pages from datasets automatically. 

I made a fake fasta of sequences that need to be codon aligned over at ```/srv/Python2/not_codon_aligned.fasta```. I will number the issues that need to be solved to get a codon alignment in order to keep things organized:

**PLEASE NOTE:** A good programmer is good at finding mistakes, test each step to find yours. Also, I underestimated the volume of work in this challenge - I tried to provide as much help as possible without giving the exercise away. Do not worry if you don't finish all the steps, working on this will definitely get you hands on in Python. 

**1.** Align with mafft and replace initial gaps with n's. Mafft is already installed on EC2, but it is useful to know how to call command line software from inside a python script - look up the subprocess module. 

<details>
  <summary>Can't figure out the correct syntax to call mafft? click here</summary>
  
```python
subprocess.call(["mafft", "--out", "nuc_aligned.fasta", in_file])
````
</details>


  **a.** Go through each of the sequences in the mafft aligned file, see part 5 for how to do this
  
  **b.** Count the number of initial gaps on each sequence
  
  **c.** Degap each sequence and place it into a Seq object
  
<details>
  <summary>Running into type issues? This one is a bit of a pain, so let me give you this</summary>
  
```python
#This line converts the sequence to a string, replaces gaps with empty strings, and placed the result into a Seq object
sequence=Seq.Seq(str(seq_record.seq).replace("-", ""))
````
</details></br>
  
  
  **d.** Prepend each sequence with n's. The number of n's should be equal to the number of initial gaps that sequence had.


  
**2.** Pick a reading frame. Real sequences have deletions, and deletions make it impossible to figure out the correct codons. A robust way of making the choice between starting each sequence from the first, second, or third nucleotide by seeing which one results in the longest total distance between stop codons. In the interest of time, you can also do a simpler version by finding which indices give mutliples of 3. More detailed steps:


**3.** Translate the DNA into amino acids. This should be simple, I will leave this exercise up to you with one hint - google translating DNA with BioPython.


4. Back translate



