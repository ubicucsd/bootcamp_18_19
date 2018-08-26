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

In order to make sure everyone is on the same page at all times, we are going to have everyone use the same computer: a giant computer in the sky, called the Amazon Elastic Cloud (EC2). We have an Ubuntu instance large enough to handle everyone's activities running in EC2, now we just need to have everyone make accounts. Please click [here]() and enter your name and UCSD user name. I will create an account for everyone - your username will be your UCSD username. 

***Secure Shell(ssh):*** a protocol which creates a secure channel for two computers to communicate even over an unsecured network. This is how we will connect to EC2. 

**How to prepare for ssh:**


**Windows:** I do not like Windows terminals, you do not like Windows terminals, no one likes Windows terminals. Go to [this](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) website and download Putty. A GUI should appear to guide you through the installation. 

**Mac or Linux:** No preparation necessary, since you already have a native ssh client. 

While I am busy creating your accounts, my partner will introduce some biology you should know in order to do bioinformatics.

## Task 2: Learn some biology

### I need some time to set up accounts, so maybe introduce sequencing here? Or do icebreakers? idk


## Task 3: Explore your EC2

In your email, you should have a .pem file named after your username. Download this file and place it into your Desktop folder. Now, open your account on the EC2 instance: 

**Windows:** Open putty, paste ```ec2-18-191-97-249.us-east-2.compute.amazonaws.com``` into the Host Name section and select port 22 and SSH on that same page. Now go to Connection->SSH->Auth and click Browse. Find your .ppk file and select it. Go back your home page, type a name under Saved Sessions and click the Save icon to the left. Now, press Open and type your username when prompted. 

**Mac or Linux:** Right click anywhere and click open terminal. You should see a prompt that looks something like  ```mchernys@mchernys-ThinkPad-T430:~/Desktop$```. If you do not have Desktop at the end, go [here]() and learn about ls and cd. Or just ask me to do it. Next, copy paste this command into the terminal and press enter ```ssh -i "your-usernamekeypair.pem" your-username@ec2-18-191-97-249.us-east-2.compute.amazonaws.com```. Note: use Ctrl-shift-V to paste into terminal. Please replace "your-username" with your actual username. Save the command you used somewhere so you can copy paste it in the future. 



Discover your identity. Type `whoami` into the window that just opened up and hit `enter`. And just like that you're talking
with your computer, you bioinformatician, you.
