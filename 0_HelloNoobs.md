# Well Hello There
#### Skills: How to: Not be a noob

#### By: Sabeel Mansuri and Mark Chernyshev

## The Big Picture

These activities are designed for people with zero to some programming experience and zero to some Bioinformatics experience. We want to give Bioinformatics freshmen some of the confidence, skills, and resources needed to apply to labs/internships and to give non-Bioinformaticians a handle on how the field works. 

## Getting a Computer Set Up

Fire up that computer! If you're asked *Windows* or *Linux*, choose **LINUX**. Linux based systems are usually what you're 
going to use in bioinformatics.

## Task 1: Make EC2 do your work!

This (might be) your first time using a Linux device. Don't worry, they'e
super easy to use (expecially for what we're doing!). Trust us, you do not want to have everyone in the room using their own computers. It gets messy. 

In order to make sure everyone is on the same page at all times, we are going to have everyone use the same computer: a giant computer in the sky, called the Amazon Elastic Cloud (EC2). Click [here](https://portal.aws.amazon.com/billing/signup?nc2=h_ct&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start) and fill out the form to create your own AWS account using your @ucsd.edu email. Once you have confirmed your email, sign into your AWS account and look at all the great resources at your fingertips. Click on All Services->Compute->EC2 and notice that it will give you a page asking you to wait. EC2 accounts take some time to set up(mine took 4 hours). Unfortunately, it looks like we'll have to come back to setting up our computers next time :'( . Trust me, this is the most time consuming step.

## Task 2: Putty

Putty is a file transfer application we will use to connect to EC2. Since EC2 does not work yet, we might as well get everything else up. 

**Windows:** I do not like Windows terminals, you do not like Windows terminals, no one likes Windows terminals. Go to [this](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) website and download Putty. A GUI should appear to guide you through the installation. 

**Mac:** Right click and press the option to open a terminal. Dowload Homebrew: ```ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"``` and use homebrew to get Putty: ```brew install putty```

**Linux:** Congrats, you are already on Linux! However, we need you to get the Linux image containing all of our software onto EC2 so you will have to get Putty anyways. If you are using Ubuntu or Debian, copy ```apt-get install putty``` into the terminal and press enter. For RedHat, CentOS, or Fedora use ```yum install putty```. If you are still not sure, ask us and we will Google it together. 


## Task 3: Setting Up Your EC2 Instance

Now that the account is set up, let's get to work. Go to Services->Compute->EC2, press Launch Instance. 

- go thru tutorial, select default security grp

- change security grp to accept all IP's. 

- copy paste remote ssh line given by amazon 

Discover your identity. Type `whoami` into the window that just opened up and hit `enter`. And just like that you're talking
with your computer, you bioinformatician, you.
