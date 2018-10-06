# Well Hello There

#### Skills: A vague understanding of what Bioinformatics?? 

## The Big Picture

These activities are designed for people with zero to some programming experience and zero to some Bioinformatics experience. We want to give Bioinformatics freshmen some of the confidence, skills, and resources needed to apply to labs/internships and to give non-Bioinformaticians a handle on how the field works. You guys are the trial group, since we have never approached UBIC classes this way. We ask for everyone to be patient and tell us when we are screwing up. Thanks! 

## Getting a Computer Set Up

Open up your laptops and go [here](https://www.awseducate.com/registration?refid=xr0Lxh7HpxP72qFKW8ygIpfSP6vTXyof). If you do not have an AWS account, please fill out that form with your UCSD account - it is free for you and I get free money. Thanks!

## Task 1: Make Accounts

In order to make sure everyone is on the same page at all times, we are going to have everyone use the same computer: a giant computer in the sky, EC2. We have an Ubuntu instance large enough to handle everyone's activities running in EC2, now we just need to have everyone make accounts. Please click [here](https://docs.google.com/spreadsheets/d/1M4S22RieI7GnJqGJZo_4flSU3FzP7ypCqrNSjZ-rf9w/edit?usp=sharing) and enter your name and UCSD user name. If you cannot open the link, make sure you are logged into your UCSD email account. I will create an EC2 account for everyone - your username will be your UCSD username. 

***Secure Shell(ssh):*** a protocol which creates a secure channel for two computers to communicate even over an unsecured network. This is how we will connect to EC2. 

**How to prepare for ssh:**

**Windows:** I do not like Windows terminals, you do not like Windows terminals, no one likes Windows terminals. Go to [this](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) website and download Putty. A GUI should appear to guide you through the installation. 

**Mac or Linux:** No preparation necessary, since you already have a native ssh client. 

## Task 2: Learn some biology

### The Alignment Problem

There are several very common and difficult problems in bioinformatics worth knowing, one of which is the problem of alignment. In order to understand why alignment is a problem, we need to undestand sequencing. You will have plenty of chances to memorize the steps of sequence. Since this is supposed to be about bioinformatics, I'll try to focus your attention on the problems that arise from sequencing(since that is where we step in). 

#### **Sanger Sequencing** 

This one is widely taught and known, but a little outdated. 

**Steps:**
**1.** Lyse the cells and extract DNA. The DNA itself is fragmented and copied many many times over. 
**2.** Attach primers to the fragments and separate the experiment into 4 tubes. 
**3.** Each tube receives plenty DNA polymerase, plenty deoxynucleosidetriphosphates (dNTPs) and about 1/100th the amount of di-deoxynucleotidetriphosphates (ddNTPs). The issue with ddNTPs is that they don't have the 3'-OH group. Synthesis stops when it a ddNTP is attached, which haappens at various points on various fragments. 
**4.** DNA is negatively charged. Heat the DNA to separate it and put through a gel from pos->neg side, which separates fragments with a resolution of 1 nucleotide. 
**5.** The trick is that the ddNTPs are flourescent! Tou now have many many fragments whose lengths you know down to the nucleotide. Expose an x-ray film to the gel, and now you have 4 rows representing the 4 nucleotides and dark bands where each of the 4 nucleotides terminated a fragment. Here's a picture to clarify: 

![image of sanger gel](https://upload.wikimedia.org/wikipedia/commons/c/cb/Sequencing.jpg)

####**Illumina Sequencing:** 

The most widely used method. This one is a bit harder to explain, so I recommend clicking [here](https://www.youtube.com/watch?v=fCd6B5HRaZ8) to watch a concise video on this topic. 

![graphic explaining illumina](http://www.3402bioinformaticsgroup.com/wp-content/uploads/2016/07/NGS.png)

#### So, what does it matter? 

What do Sanger and Illumina sequencing have in common? Both produce ridiculous quantities of small DNA fragments. Illumina produces  300 million to 4 billion reads per run, with a selection of read lengths ranging from 50 base pairs to 300 base pairs. Meanwhile, Sanger produces 50000 sequences at lengths varying from 800 to 1000 base pairs. To give some perspective, the typical animal of interest is a human and those have 3.0×10^9 base pairs. Individual human genes range from 1148 to 37.7 kb (average length = 8446 bp,s.d. = 7124). 




## Task 3: Explore your EC2

In your email, you should have a password from me. 

**Windows:** Open putty, paste ```ec2-18-191-97-249.us-east-2.compute.amazonaws.com``` into the Host Name section and select port 22 and SSH on that same page. Type a name under Saved Sessions and click the Save icon on the right. Now, press Open and type your username and password when prompted. 

**Mac or Linux:** Right click anywhere and click open terminal. You should see a prompt that looks something like  ```mchernys@mchernys-ThinkPad-T430:~/Desktop$```. Next, copy paste this command into the terminal and press enter ```ssh your-username@ec2-18-191-97-249.us-east-2.compute.amazonaws.com```. Note: use Ctrl-shift-V to paste into terminal. Please replace "your-username" with your actual username. Save the command you used somewhere so you can copy paste it in the future. 

You probably have your own password in mind for your account, so make it! Type ```passwd username``` and follow the prompts to set your own password. 

Discover your identity. Type `whoami` into the window that just opened up and hit `enter`. And just like that you're talking
with your computer, you bioinformatician, you.

