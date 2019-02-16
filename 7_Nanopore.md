# Tutorial: Nanopore Analysis Pipeline

## Introduction

### Lesson plan

This is a bit of a bonus lesson. Nanopore is an experimental, new sequencing technique that I (Sabeel) just happen to work on. This lesson/tutorial is an attempt to familiarize you with nanopore.

### What's Nanopore?

Nanopore sequencing is a new and developing technique in bioinformatics that you can read about [here](https://nanoporetech.com/applications/dna-nanopore-sequencing) from one of the leading companies in the field, Oxford Nanopore. If you're not interested in the details, here's a summary: Nanopore uses super small holes to run DNA through, measures current changes to determine which base pair is at that position, and reports it as output.

### So... why?

Nanopore sequencing is getting a bunch of attention because it allows for longer reads. A lot longer. In the sample fastq files we've provided before, you'll notice that each read (or each "entry") was around 200 base pairs long. Nanopore reads have been frequently observed around 10,000 base pairs, and even up to 100,000 base pairs in extreme circumstances.

### No really... why?

Longer reads intuitively seem like a good thing, but why exactly is that? Remember that alignment is, essentially, finding overlaps in reads to fit them together. And, the longer the reads, the easier alignment is. For example, try to assemble the following message using reads of size 3 and reads of size 6:
```
[at!],[u a],[ re],[gre],[You],[ ar],[eat],[e g]
```

```
[great!],[re gre],[You ar]
```

Again, the longer the reads, the easier (and, as you'll have found, the faster) the alignment.

## Software

This tutorial will require the following softwares. They are all already installed. *DO NOT INSTALL THEM AGAIN!*

Click each of the links to understand what they do. This step is critical to understanding the rest of the tutorial.

##### Aside: It's totally possible to complete this tutorial (and most of our lessons) without reading about the softwares. This isn't a good idea. Not only will reading the documentation familiarize you with a particular software, it will familiarize you with (1) the idea behind softwares similar to it and, much more importantly, (2) how to parse documentation effectively so you don't waste your time. Don't underestimate how much time you'll spend reading documentation--if you're a bioinformatician, it's practically your job.

### Canu

[Canu Assembler](https://canu.readthedocs.io/en/latest/) 

Canu is a packaged correction, trimming, and assembly program that is forked from the Celera assembler codebase. What does all of this mean? Read the documentation (and ask us!) until you understand.

### Prokka

[Prokka](https://github.com/tseemann/prokka)

Prokka is a gene annotation program. What does this mean? Read the documentation (and ask us!) until you understand.

### Barrnap

[Barrnap](https://github.com/tseemann/barrnap)

Barrnap is an rRNA prediction software used by Prokka. What does this mean? Read the documentation (and ask us!) until you understand.


## Dataset
There is a nanopore dataset located at the following location on the cluster:
```
TODO
```

This data is from an isolate from a sample taken from a local saline lake at [South Bay Salt Works](https://en.wikipedia.org/wiki/South_Bay_Salt_Works) near San Diego, California.


## Assembly
Canu can be used directly on the data without any preprocessing. The only additional information needed is an estimate of the genome size of the sample. For saline isolates, we can safely estimate 3,000,000 base pairs based on previous data. 

Now, simply use the folliowing Canu command to assemble our data:

```
canu -nanopore_raw -p test_canu -d test_canu runs_fastq/*.fastq genomeSize=3000000 gnuplotTested=true
```

A quick description of all flags and parameters: 
-nanopore_raw - specifies data is Oxford Nanopore with no data preprocessing
-p - specifies prefix for output files, use “test_canu” as default
-d - specifies directory to run test and output files in, use “test_canu” as default
genomeSize - estimated genome size of isolate
gnuplotTested - setting to true will skip gnuplot testing; gnuplot is not needed for this pipeline

Running this command will output various files into the test_canu directory. The assembled contigs are located in the test.contigs.fasta file. These contigs can be better visualized using Bandage.


## Assembly Visualization
There's a GUI program called [Bandage](https://rrwick.github.io/Bandage/) that allows you to visualize assemblies. We're not going to  over using Bandage, but if you opened of the files in the test_canu directory using Bandage, you would see the folliwng: O

<br /><img src="https://github.com/sabeelmansuri/bowman_archive/blob/master/Bandage.png" width="300"><br />

This suggests that one of our assembled pieces ("contigs") appears to be a whole circular chromosome!

This happens to be Contig 1. We extract only this sequence from the contigs file to examine further. Note that the first contig takes up the first 38,673 lines of the file, so use `head`:

```
head -n38673 test_canu/test_canu.contigs.fasta >> test_canu/contig1.fasta 
```

## NCBI BLAST
We can now blast this Contig using NCBI’s nucleotide BLAST database (linked [here](https://blast.ncbi.nlm.nih.gov/Blast.cgi)) with all default options. (**Challenge: can you BLAST using Biopython?**) The top hit is:

```
Hit: Halomonas sp. hl-4 genome assembly, chromosome: I  
Organism: Halomonas sp. hl-4  
Phylogeny: Bacteria/Proteobacteria/Gammaproteobacteria/Oceanospirillales/Halomonadaceae/Halomonas  
Max score: 65370  
Query cover: 72%  
E value: 0.0  
Ident: 87%  
```

It appears this chromosome is the genome of an organism in the genus *Halomonas*. Google *Halomonas*. Sanity check: Does it make sense that we'd find *Halomonas* at South Bay Saltworks?

We may now be interested in the gene annotation of this genome.


## Gene Annotation
Prokka will take care of gene annotation, the only required input is the contig1.fasta file.

```
prokka --outdir circular --prefix test_prokka test_canu/contig1.fasta
```

The newly created circular directory contains various files with data on the gene annotation. Take a look inside test_prokka.txt for a quick summary of the annotation. 


## Summary
The analysis above has taken Oxford Nanopore sequenced data, assmebled contigs, identified the closest matching
organism, and annotated its genome.

## Credits
Adapted from my [Bowman Lab Tutorial](https://www.polarmicrobes.org/tutorial-nanopore-analysis-pipeline/)
