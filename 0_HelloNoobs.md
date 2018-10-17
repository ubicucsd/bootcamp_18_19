# Well Hello There

#### Skills: A vague understanding of what Bioinformatics?? 

## The Big Picture

These activities are designed for people with zero to some programming experience and zero to some Bioinformatics experience. We want to give Bioinformatics novices some of the confidence, skills, and resources needed to apply to labs/internships and to give non-Bioinformaticians a handle on how the field works. You guys are the trial group, since we have never approached UBIC classes this way. We ask for everyone to be patient and tell us when we are screwing up. Thanks! 

## Getting a Computer Set Up

## Task 1: Make Accounts

In order to make sure everyone is on the same page at all times, we are going to have everyone use the same computer: a giant computer in the sky, EC2. We have an Ubuntu instance large enough to handle everyone's activities running in EC2, now we just need to have everyone make accounts. Please click [here](https://docs.google.com/spreadsheets/d/1M4S22RieI7GnJqGJZo_4flSU3FzP7ypCqrNSjZ-rf9w/edit?usp=sharing) and enter your name and UCSD user name. If you cannot open the link, make sure you are logged into your UCSD email account. I will create an EC2 account for everyone - your username will be your UCSD username. 

***Secure Shell(ssh):*** a protocol which creates a secure channel for two computers to communicate even over an unsecured network. This is how we will connect to EC2. 

**How to prepare for ssh:**

**Windows:** I do not like Windows terminals, you do not like Windows terminals, no one likes Windows terminals. Go to [this](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) website and download Putty. A GUI should appear to guide you through the installation. 

**Mac or Linux:** No preparation necessary, since you already have a native ssh client. 

## Task 2: Learn some biology

### The Alignment Problem

There are several very common and difficult problems in bioinformatics worth knowing, one of which is the problem of alignment. In order to understand why alignment is a problem, we need to undestand sequencing. You will have plenty of chances to memorize the steps of sequencing, and this is supposed to be about bioinformatics, so don't feel like you need to memorize them. I'll try to focus your attention on the problems that arise from sequencing (since that is where we, as bioinformaticists, step in). 

**Sanger Sequencing** 

This one is widely taught and known, but a little outdated. 

**1.** Lyse the cells and extract DNA. The DNA itself is fragmented and copied many many times over. 

**2.** Attach primers to the fragments and separate the experiment into 4 tubes. 

**3.** Each tube receives plenty DNA polymerase, plenty deoxynucleosidetriphosphates (dNTPs) and about 1/100th the amount of di-deoxynucleotidetriphosphates (ddNTPs). The issue with ddNTPs is that they don't have the 3'-OH group. Synthesis stops when it a ddNTP is attached, which haappens at various points on various fragments. 

**4.** DNA is negatively charged. Heat the DNA to separate it and put through a gel from pos->neg side, which separates fragments with a resolution of 1 nucleotide. 

**5.** The trick is that the ddNTPs are flourescent! You now have many many fragments whose lengths you know down to the nucleotide. Expose an x-ray film to the gel, and now you have 4 rows representing the 4 nucleotides and dark bands where each of the 4 nucleotides terminated a fragment. Here's a picture to clarify: 

![image of sanger gel](https://upload.wikimedia.org/wikipedia/commons/c/cb/Sequencing.jpg)

**Illumina Sequencing:** 

The most widely used method. This one is a bit harder to explain, so I recommend clicking [here](https://www.youtube.com/watch?v=fCd6B5HRaZ8) to watch a concise video on this topic. 

![graphic explaining illumina](http://www.3402bioinformaticsgroup.com/wp-content/uploads/2016/07/NGS.png)

***So, what does it matter?***

What do Sanger and Illumina sequencing have in common? Both produce ridiculous quantities of small DNA fragments. Illumina produces  300 million to 4 billion reads per run, with a selection of read lengths ranging from 50 base pairs to 300 base pairs. Meanwhile, Sanger produces 50000 sequences at lengths varying from 800 to 1000 base pairs. To give some perspective, the typical animal of interest is a human and those have 3.0×10^9 base pairs. Individual human genes range from 1148 to 37.7 kb (average length = 8446 bp,s.d. = 7124). 

These tiny reads overlap all over the place. If you imagine the true sequence these reads came from and place the reads where they came from, you will get many reads piled up over every base pair in the true sequence. The more reads pile up, the more accurately you can predict the actual sequence. A common measure that rates the robustness of an alignment is coverage:

![coverage](https://slideplayer.com/slide/5083621/16/images/4/Definition+of+Coverage.jpg)

Alignment allows us to find how two or two thousand sequences line up, allowing us to identify single mutations, reduce error rates, build original(de novo) sequences, and analyze homology to build evolutionary trees. 

TLDR: There are numerous complex applications of bioinformatics algorithms, from functional structure predictions to ancestral reconstructions. Alignment serves as the foundation for many of these algorithms, making basic sense of the incomprehensible mass of DNA that sequencing gives us. 

### The Clustering Problem 

The general idea behind clustering is the grouping of many elements so that the elements in a cluster are more similar to each other than they are to those in other groups. 

**Hierarchical Clustering:** 

Based on a system where elements that are closer together are more similar than those that are further apart. In this approach, elements which are close together will be combined into a cluster that is the hybrid location of both elements. So if we have an element a (0, 4) and another at (0, 2), the cluster is at (0, 3). The reason this is interesting to us is that it forms a tree of clusters, which can represent a tree of related genes which can be used to infer homology. Another example application is the finding of true sequences. Imagine you have a sequencing experiment that amplifies genes from an HIV sample, but you do not know how many successful mutations of HIV you have in the sample(infected people usually carry multiple versions because of how fast it mutates). After cleaning these sequences, clustering them together can reveal closely related groups. With the proper distance tweaking and statistical tricks, you can separate each real version of the virus into a cluster, revealing the prevalent mutations in the patient.

*Side Note:* As you will soon learn in your CSE classes, implementation is important and the state of the art alignment and clustering programs do their job quickly and accurately because they attempt to do the minimum amount of work possible. Fast alignment programs like mafft use fancy tricks like fourier tranforms and fast clustering algorithms often use simpler tricks like transforming into kmer representation. Bioinformatics has lots of data, so you should never attempt to solve a problem by going through all possible combinations or even the majority of all possible combinations. To give the classic stupid example, 80 sequences of length 1000 technically have over 1000^80 possible alignments which is a bit off from the 10^80 atoms in our universe. 

## Task 3: Explore your EC2

In your email, you should have a password from me. 

**Windows:** Open putty, paste ```ec2-18-191-97-249.us-east-2.compute.amazonaws.com``` into the Host Name section and select port 22 and SSH on that same page. Type a name under Saved Sessions and click the Save icon on the right. Now, press Open and type your username and password when prompted. 

**Mac or Linux:** Right click anywhere and click open terminal. You should see a prompt that looks something like  ```mchernys@mchernys-ThinkPad-T430:~/Desktop$```. Next, copy paste this command into the terminal and press enter ```ssh your-username@ec2-18-191-97-249.us-east-2.compute.amazonaws.com```. Note: use Ctrl-shift-V to paste into terminal. Please replace "your-username" with your actual username. Save the command you used somewhere so you can copy paste it in the future. 

You probably have your own password in mind for your account. Type ```passwd username``` and follow the prompts to set your own password. 

Discover your identity. Type `whoami` into the window that just opened up and hit `enter`. And just like that you're talking
with your computer, you bioinformatician, you.

