# Well Hello There

#### Skills: A vague understanding of what Bioinformatics is

## The Big Picture

These activities are designed for people with zero to some programming experience and zero to some Bioinformatics experience. We want to give Bioinformatics freshmen some of the confidence, skills, and resources needed to apply to labs/internships and to give non-Bioinformaticians a handle on how the field works. 

## Getting a Computer Set Up

Open up your laptops and go [here](www.awseducate.com/registration?refid=xr0Lxh7HpxP72qFKW8ygIpfSP6vTXyof). If you do not have an AWS account, please fill out that form with your UCSD account - it is free for you and I get free money. Thanks!

## Task 1: Make EC2 do your work

In order to make sure everyone is on the same page at all times, we are going to have everyone use the same computer: a giant computer in the sky, EC2. We have an Ubuntu instance large enough to handle everyone's activities running in EC2, now we just need to have everyone make accounts. Please click [here](https://docs.google.com/spreadsheets/d/1M4S22RieI7GnJqGJZo_4flSU3FzP7ypCqrNSjZ-rf9w/edit?usp=sharing) and enter your name and UCSD user name. If you cannot open the link, make sure you are logged into your UCSD email account. I will create an EC2 account for everyone - your username will be your UCSD username. 

***Secure Shell(ssh):*** a protocol which creates a secure channel for two computers to communicate even over an unsecured network. This is how we will connect to EC2. 

**How to prepare for ssh:**

**Windows:** I do not like Windows terminals, you do not like Windows terminals, no one likes Windows terminals. Go to [this](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) website and download Putty. A GUI should appear to guide you through the installation. 

**Mac or Linux:** No preparation necessary, since you already have a native ssh client. 

## Task 2: Learn some biology

### The Alignment Problem

There are several very common and difficult problems in bioinformatics worth knowing, one of which is the problem of alignment. In order to understand why alignment is a problem, we need to undestand sequencing. 

- clustering stuff from my lab

**Sanger Sequencing** 

While it is widely taught and known, it is also a little outdated so let's go through it quickly. 

Steps:
1. Lyse the cells and extract DNA. The DNA itself is fragmented and copied many many times over. 
2. Attach primers to the fragments and separate the experiment into 4 tubes. 
3. Each tube receives plenty DNA polymerase, plenty deoxynucleosidetriphosphates (dNTPs) and about 1/100th the amount of di-deoxynucleotidetriphosphates (ddNTPs). The issue with ddNTPs is that they don't have the 3'-OH group. Synthesis stops when it a ddNTP is attached, which haappens at various points on various fragments. 
4. DNA is negatively charged. Heat the DNA to separate it and put through a gel from pos->neg side, which separates fragments with a resolution of 1 nucleotide. 
5. The trick is that the ddNTPs are flourescent! Tou now have many many fragments whose lengths you know down to the nucleotide. Expose an x-ray film to the gel, and now you have 4 rows representing the 4 nucleotides and dark bands where each of the 4 nucleotides terminated a fragment. Here's a picture to clarify: 
![image of sanger gel](https://upload.wikimedia.org/wikipedia/commons/c/cb/Sequencing.jpg)

**Illumina Sequencing:** 


## Task 3: Explore your EC2

In your email, you should have a password from me. 

**Windows:** Open putty, paste ```ec2-18-191-97-249.us-east-2.compute.amazonaws.com``` into the Host Name section and select port 22 and SSH on that same page. Type a name under Saved Sessions and click the Save icon on the right. Now, press Open and type your username and password when prompted. 

**Mac or Linux:** Right click anywhere and click open terminal. You should see a prompt that looks something like  ```mchernys@mchernys-ThinkPad-T430:~/Desktop$```. Next, copy paste this command into the terminal and press enter ```ssh your-username@ec2-18-191-97-249.us-east-2.compute.amazonaws.com```. Note: use Ctrl-shift-V to paste into terminal. Please replace "your-username" with your actual username. Save the command you used somewhere so you can copy paste it in the future. 

You probably have your own password in mind for your account, so make it! Type ```passwd username``` and follow the prompts to set your own password. 

Discover your identity. Type `whoami` into the window that just opened up and hit `enter`. And just like that you're talking
with your computer, you bioinformatician, you.

