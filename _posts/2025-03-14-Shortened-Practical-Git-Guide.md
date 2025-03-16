---
classes: wide
title: "Shortened Practical Git Guide"
excerpt: "A practical guide to Git for single users who need bare minimum functionality."
---

# Motivation
I'm writing this becaue my first attempt was too long and included features that weren't useful to my ideal user (my dad). What I thought was already shortened was not short enough and frankly didn't cover the true simplest use case of Git. This guide is for someone who has a collection of files and wants a better way to version control than saving to a G-drive folder and changing a version number. You don't need to use every single git function to make it useful so here's the least amount of features you can use to get some value from Git. 

# As Short as Possible
At the very center of Git is 3 simple operations, save/upload/download. If you are a one-person show with no risk of merge conflicts or writing on two machines at once this is what you need and *all* you need.

If you want to super-simplify use Github Desktop. But read the rest of this so that you know the context around the basic actions.

## Repository Creation

Create your repository on Github. Don't mess with Git init or anything like that. Once you've created your repository check the home page of the repo and copy the URL of it. 

## Download
Now go to your command line and run this command. This is your download.  

```
git clone <your_url>
```
## Save

Now go ahead and change some files. When you're ready to save type this command.
```
git status
```
This will show you all of the changes you've made since the last time you committed. File additions, deletions, changes will all show up here. To submit these changes to be saved run this.
```
git add .
```
If you want to submit specific changes you can type file names in place of the period. Now to save use this command.
```
git commit -m "some message here"
```
This will 'commit' (aka save) your changes but only locally. Your message is how you will trace back and figure out what you changed when so make sure it's descriptive. 

## Upload
Finally to upload to your 'remote' repository (Github) use Github desktop. I know we were all command line up to this point but going through the rigmarole of issuing personal keys or god-forbid ssh certificates is too much for this tutorial.

When you want to get your code or work on another computer just do the git clone step again and you'll have it wherever you need it. 