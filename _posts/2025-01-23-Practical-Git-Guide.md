---
classes: wide
title: "Practical Git guide for people that don't use it 40 hours a week"
excerpt: "A practical Git guide for entry-level users"
---

# Setup
For setup purposes I'll assume you're using windows but the instructions will work with any operating system, you just won't be able to use the exact links here. If you are on Mac or Linux you'll have to search for something like "Git install Mac".

## Installing Git & Helpful addons
### Git and Git Bash
This link is for windows, pick the standalone installer. I'm sure you already know this but just for the sake of completeness I'll mention exactly what I am using.

[https://git-scm.com/downloads/win](https://git-scm.com/downloads/win)

If you want to remain on the command line the entire time you can run this command: 

	
```
winget install --id Git.Git -e --source winget
```

Both of these will install the Git command line tool as well as a custom terminal called 'Git Bash'. It's useful for a few things. The first, it gives the user a very nice color palette that highlights what Git branch you're on as well as Linux commands in case you're more accustomed to them. It is not necessary, powershell and cmd both work just as well.

### Git GUI
The official Git project recommends a number of GUIs, old timers will tell you not to use them and to get used to the command line. I've met excellent developers who use either and some use a mix of both. While starting out it's easier to visualize Git relationships using these tools. There are a ton of them but I've had most luck with the first two following. 

[Github Desktop](https://Github.com/apps/desktop) The GUI I've used the most. Does not require you to be using Github, automates certifications for push and pull.

[SourceTree](https://www.sourcetreeapp.com/) The GUI I've seen used by the most professional developers.

[UnGit](https://Github.com/FredrikNoren/unGit) I'm not familiar with this one but the Github README is really good and the xkcd comic at the top sums up the Git experience nicely, even when using it alongside 25+ year developers. I'm switching to this one now just to see what it's like. (Postnote: This is no longer maintained, it's probably still ok because Git doesn't change much but I would avoid for now. I did however learn about Chattanooga Open Data from this repository.)

You can use all of these, even all of them at once and pick whichever is simplest or you find the easiest to use.

### Git Bash
You can download Git Bash from the official Git project, it comes by default in the Windows Git installation.

Git commands will run in any shell (bash, powershell, cmd, zsh) but we want to use Git Bash. This shell mimics a bash shell (the shell used most frequently on Linux) and unifies the commands we'll write. From here on the commands are the same on every operating system.

# Git Explained

For starters, Git is never simplified as it should be. People throw all sorts of insane terms at you right out of the gate so here's what you really need to know. Git at its core cares about 3 things. 

1. Repositories
2. Branches
3. Commits

These three things, to Git, are nouns. Everything else in Git is a verb. Pull, Pushe, Clone, Fork, Merge, Rebase, everything you can think of is an action that effects your set of Repos, Branches, and Commits. THAT'S IT. The following sections will be sorted by these 3 nouns and the commands that are run on them.

## Repositories
A repository is either a local or a remote copy of a Git project. It's oftened shortened to the word 'repo'. Your local repository is a copy of your entire project on your local machine. A remote repository is a copy of the project on a server. Having a local and remote copy allows you to make some change on a local machine and keep a copy remotely that can be shared with users, other contributors, or different machines. 

### Git clone
When you use Git clone Git copies all of the files from the remote repository you point to and creates a .git file. Your .git file tracks your changes, the URL of your remote repository, your username, and other useful details for the project. THAT'S IT. The syntax for cloning is as simple as:
```
git clone <your_project_url>
```
This command only needs to be run once on your machine to get the project initiated. After that you can use the git pull command.

### Git init
When you do Git init Git creates a new repository with no remote copy. Similar to git clone it creates a .git file that tracks important information about your project. 

>### Practical Shortcut 1
 >Your first practical shortcut. If you want to create a new Git project DON'T use Git init. Create a new project on Github first, clone it, add your files, commit and push to origin. If you Git init first you may struggle to make a new repo on Github and match it up with your local repo, you have to set an origin, create an upstream, blah blah blah. I remedy this by just never doing it.
<!-- {: .notice--warning} -->

### Git remote add
If you want to add a remote after running Git init or if you want to change the remote you're pointing at you can use Git remote add. Because of the above practical shortcut you really won't ever have to use this.

## Branches
A branch is a silo of code that (in best practice) contains the changes a developer wants to make for a single feature. Many developers also use specific branches for development, staging, and production. 

> **Practical Shortcut 2**
>
> If you are working on a solo project you probably don't need to make any branches. "HERETIC! SINNER! MADMAN!" I hear you saying. To seriously simplify Git you can stick to commits, pushes, and pulls and treat them like save, upload, and download. Use just the main branch and forget about the rest until you really need it or you want to expand your horizons.

### Git branch
Git branch can be used in a couple of ways. 
```Git branch list```
Displays all of the branches available on your local.
```Git branch "branch name"```
Creates a new branch with the branch you are currently in as the parent branch, also known as the upstream branch.

### Git checkout
Git checkout switches the Git user to the branch they specify. 
>[!warning]- Practical Shortcut 3
>You can use checkout to both start a new branch and switch to it immediately by running:
>```Git checkout -b "branch_name"```
>I use this every time I want a new branch because I always want to switch to it.

### Git merge
Getting to Git merge is when we introduce some complexity. Git merge takes the changes made in one branch and combines them into another branch. When you use Git merge you are merging INTO your current branch the changes FROM the branch you specify. In Git Bash this will look like this:
```
yourDesktopName MINGW64 ~yourWorkingDirectory (currentBranch)
$ Git merge brachYouWantChangesFrom
```
The default way a merge occurs is by introducing a commit where you describe the branches merged and organize the differences between your branches. You'll often hear about 'fast-forward' merges, this is a special case wherein no changes have occurred on the branch being merged into. Git will do all of the merging for you, it basically simulates making the changes on the branch being merged into.

## Commits
While Git branches hold entire features, Git commits should hold small incremental code changes. Best practice is to make these small, only containing atomic changes, consider making a commit every time you would have clicked 'save document' in the 90s. 

Commits are important because if you screw something up later on you are going to revert to a specific commit. Packing too many changes into a single commit will risk not being able to isolate your bad changes from the good ones. 
### Git status
We're introducing new vocab here so sit tight. When you run Git status Git will present the changes that have occurred in your repository since the last commit. Some of these will be tracked and some will be untracked. Tracked means that you or another user have told Git about the file before. Untracked means the opposite. There are many cases you might want to not track a file such as generated sources, locale-specific settings, or files including secret keys.
> [!note]- Untracked or Gitignore?
> If you mean to keep files untracked you should add them to your Gitignore, this will keep Git from warning you that they are untracked when you run Git status.

Git status will also show you which files you've modified and what commands you can run next to add these changes to your commit. Run ```Git add .``` to add all of the changes and untracked files to your commit. Run ```Git add <file_name>``` if you want to add specific files. 

If you accidentally run Git add on something you don't want added you can run Git reset to remove your additions.

>[!warning]- Practical Shortcut 4
>Adding changes and files is often easier in a GUI. Every good GUI will show you what changes were made in the files and will show you a good list of your changes as well. In all, commits are a good task to undertake in a GUI.
### Git commit
Git commit takes all of your staged changes and creates a commit out of them. It attaches this commit to the end of your current branch and makes this commit the new HEAD of the branch. COMPLICATED? no. It's just like saving a file. If you want to go back to a previous commit you can use revert just like you can ctrl+z back to a previous version of your file. 
``` Git commit -m "Your commit message"```
Add this message or Git will launch vim and you'll have to learn how to escape vim (escape -> :q!). 

THATS IT. Don't complicate commits any more than that. And when in doubt, make your commit even if you're not sure of it. Then you can move from commit to commit depending on which changes you want to see.

Git stash
This command tucks all of your changes away into a separate location and resets your current directory. This is super useful if you get confused or things start to go awry in your Git you can stash your changes and reset back to the last commit on your branch. Then you can push, pull, branch, or whatever else you need to do but your changes will be saved in your stash.
>[!warning]- Practical Shortcut 5
>Oftentimes getting changes out of a stash is a fool's errand. A common workaround from stashing is to copy the changes you've made to a text file, Git stash, forget about this stash, and then copy the changes out of the text file and paste them into your now clean local repository. It's messy yes, but development is about simplicity and this is simpler.
# Back to Repositories
Ok, so we've been through creating or cloning a repository, branching from the main, creating commits, and even a little section about merging. Now we're going to talk about pushing, pulling, and merge requests. Believe it or not there are no new concepts introduced here, we are just running merges across remote and local repositories. 

Why did morons have to complicate these things? Because they have forgotten that the heart of engineering is simplification not complication and they know that if they continue to complicate at a rate that out-group people can't keep up they'll always feel superior to the people who aren't in the in-group that sacrifices all of their free time to invent ridiculous new concepts to ever-shrink their in-group. "But Bryce don't highly specialized fields need a highly specialized vernacular to convey complex concepts quickly?" No, these people want to feel superior and for that reason they never will be, speak to any snooty nerd and you will instantly understand this. 

To simplify the above, semantic-andys make everything worse.

### Git pull
Git pull is (simply) a fetch and a merge. Fetch is like clone in that you're downloading from a remote repository but fetch means that you only download changes instead of the full project. Merge is what we talked about before, putting the differences from some commit into our desired commit.
```Git pull origin main```
Here we're telling Git to fetch and merge all of the changes from the remote repository we have defined and nicknamed 'origin', at the repository's branch named 'main', at the most recent commit into our local current branch. THAT'S IT.
origin repo > main branch > most recent commit ----> local repo > current branch

>[!warning]- Practical Shortcut 6
>This is simple if you are developing on 2 different machines and you need to get changes from your remote repository but you never make changes on both machines at once. You won't ever run into merge conflicts. 
>Merging conflicts is best done in GUIs.

> [!warning]- Practical Shortcut 7
> If you find that merge conflicts are really killing your productivity then use the stash shortcut explained above. Stash all of your changes, pull for the most recent, write your changes over the top of what you've pulled. Don't wade in the awful merging conflict resolution, then rebasing, then you have to push because your merging and rebasing made 3 different brand new commits and now your local is different than your remote despite the contents being the exact same because you've got 3 commits that your remote doesn't know about. woops, got carried away.

### Git push
Git push puts your current local branch onto the remote repository. There are 3 scenarios we might push changes to our remote. 
#### Git push origin main
Use this command if you are working in your main branch and you're comfortable making changes directly to it. This is the simplest possible way to push changes but it's really only possible if you're abstaining from making new branches and you're working on main.
#### Git push origin some_branch
Use this command if you're working on a different branch from main. Then on Github you can create a pull request (called a merge request on Gitlab) and get your branch changes into main. This is the most common way I've seen professional developers do things, it makes for really easy code reviews because they're hosted on a website everyone can access instead of your local.
#### Git pull origin main -> Git push origin main
If you have changes in your remote that you don't yet have in your local you need to catch up before you push to main. This is because the push to main won't go through unless you are able to fast-forward merge. This is complicated, I know but doing a pull and then a push will work. If need be return to shortcuts 7 and 5, stash your changes, pull main, copy your changes in, push to main.
# Sample Workflows
## Simplest possible
We are using only the main branch on both remote and local repositories. This is a perfectly acceptable workflow despite not using branching at all.
``` 
Git clone some_repository
# grab your remote repo
for (all of the changes you want to make)
	echo "Hello World" > someFile.txt
	# make some change to the repository
	Git status
	# view the modified and untracked files
	Git add .
	# add all of the untracked and modified files
	Git commit -m "commit message, made some changes"
	# commit your staged changes and leave a descriptive message for posterity
Git push origin main
# put all of your changes into your Git remote
```
## Using branching
This workflow uses super simple branching only on your local. You'll be keeping your remote repository very simple by maintaining only the main branch. 
``` 
Git clone some_repository
# grab your remote repo
for (each feature you want to add)
	Git checkout -b some_branch_name
	# create and checkout a new feature branch
	for (all of the changes you want to make)
		echo "Hello World" > someFile.txt
		# make some change to the repository
		Git status
		# view the modified and untracked files
		Git add .
		# add all of the untracked and modified files
		Git commit -m "commit message, made some changes"
		# commit your staged changes and leave a descriptive message for posterity
	Git checkout main
	# checkout branch you want to merge changes into
	Git merge some_branch_name
	# merge some_branch_name into main
Git push origin main
# put all of your changes into your Git remote
```
## The 'Professional' way
``` 
Git clone some_repository
for (each feature you want to add)
	Git checkout -b some_branch_name
	# create and checkout a new feature branch
	for (all of the changes you want to make)
		echo "Hello World" > someFile.txt
		# make some change to the repository
		Git status
		# view the modified and untracked files
		Git add .
		# add all of the untracked and modified files
		Git commit -m "commit message, made some changes"
		# commit your staged changes and leave a descriptive message for posterity
	Git pull origin main
	# Necessary becuase someone has already made changes ahead of you
	# Merges origin main into your local, catching you up to main. Resolve conflicts if they occur.
	Git push --set-upstream "some_branch_name"
	# Push your change to remote on a new (to the remote) branch called some_branch_name
	> Go to Github and create a merge request, review with the team
```
# FAQ
## What if I made changes before branches?
That's ok, I do that all the time. You can still create a new branch and check it out and the changes will transfer to that branch so long as you haven't committed anything yet.

# Remember
When in doubt use the stash trick, it'll skip most of the tedious stuff for you.