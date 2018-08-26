# Good ol' Git(Hub)
#### Skills: Version Control, Collaborative Coding

## The Big Picture

All of the lectures so far have been availableon GitHub, but what even is GitHub? Although you've used GitHub primarily for getting assignments, that isn't GitHub's intended use (though it does do a good job of holding our material!). GitHub is primarly 
focused on allowing one or more users to store and collaborate on projects. There's two main parts to how GitHub does this: 
1. version control ("Git")   
2. collaborative coding ("Hub")

Today, we explore the hidden power of GitHub.

## Getting Started

Create a new directory for this week. Enter that directory. Visit www.github.com. Sign up for a GitHub account using your UCSD email (even if you already have one!).

Tip: Use an all-lowercase username. There's only a few places where this matters, but it'll just make your life easier.

## The Git in GitHub

Git is a program that allows you to track changes you make to one or more files, a feature called *version control*. 

Imagine you're working on a big bioinformatics project called Toby. You have a bunch of files saved under a `Toby/` directory--everything's going swell until you accidentally delete all your files using `rm *`. This is why *version control* exists: you have a way of getting those files back.

Of course, this is the worst case situation--in practice, version control has many other uses, such as tracking progress, creating various versions of the same project, and much more. We'll get you started with the basics now:

#### Note: You don't need GitHub to use Git! Think of GitHub as an extended feature of Git. To drive this home, the rest of this section will not use GitHub at all, just Git. We'll see what GitHub is good for in the *next* section.

Create and enter a new directory called `week3`. Create 3 empty files called `file1`, `file2`, and `file3`. Now, let's tell Git you want to track changes in this directory. Type:

```shell
git init
```

By deafult Git won't track any of your files. Prove this to yourself by checking the status of your Git tracking:

```shell
git status
```

You can see Git telling you how to add files you want to create a version of: use "git add" to track. Let's start tracking `file1` and `file2`:

```shell
git add file1 file2
```

Check the status to see if that worked. Git will tell you that you need to "commit" your changes. Think of committing as creating one version that Git will store. In our example, committing now will have Git remember that `file1` and `file2` were at some point empty (but they won't be for long!). Let's commit our changes:

```shell
git commit -m "First commit"
```

You'll notice the -m flag. The m is short for message. You should **always** have a commit message explaining what this version is (or what has changed since the last version). Here, I've made that message "First commit".

Here's what just happened: Git has stored what `file1` and `file2` currently look like. 

Now, go into `file1` and enter a bunch of text. Next, check Git's status--it will tell you that `file1` has been modified. Great! Now let's tell Git to store this new version of `file1`. Add and commit `file1` like we did before, remembering to add a new descriptive commit message (maybe, "Edit file1"). Check Git's status to confirm `file1` is in order.

Let's do the unthinkable.

```shell
rm *
```

You deleted all your files! No worries, Git to the rescue! You can "checkout" a previous version that Git saved. Do:
```shell
git checkout *
```

Git did the best it could. You get `file1` and `file2` back because you committed versions of them to Git. `file3` is gone forever :-(. Moral of the story: track early, track often!

What we've just seen is the basic flow of keeping track of edits in Git: Edit, add, commit, edit, add, commit, ed...


## The Hub in GitHub

So, then, what's GitHub?

GitHub upgrades Git in two major ways:  
1. Collaboration - allowing more than one person to safely contribute to a project
2. Visualization - allowing project changes and versions to be easily looked at

Think of GitHub as holding a "master" copy of your project. Anyone who wants to make changes can grab a local copy of the project, make edits locally, and update the "master" copy once they're done.

The best way to see this is in action. Make sure you've signed up for GitHub (see instructions above), get into groups of 2-3 people, and move on to the tasks.


## Collaborative Coding I

-set up github repo to be cloned containing blank task files- 

## Collaborative Coding II

Alright, every member of your team is now able to access your project, which has its master copy stored on GitHub.

-what task can they perform-

## What You've Learned

Skills developed + next steps. Applications.

## Credits and Citations
