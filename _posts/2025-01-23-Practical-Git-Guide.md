---
classes: wide
title: "Practical Git guide for people that don't use it 40 hours a week"
---

# Setup
For setup purposes I'll assume you're using windows but the instructions will work with any operating system, you just won't be able to use the exact links here.
## Installing Git & Helpful addons
### Git and Git Bash
This link is for windows, pick the standalone installer. I'm sure you already know this but just for the sake of completeness I'll mention exactly what I am using.

[https://git-scm.com/downloads/win](https://git-scm.com/downloads/win)

If you want to remain on the command line the entire time you can run this command: 

	
```bash
winget install --id Git.Git -e --source winget
```

Both of these will install the git command line tool as well as a custom terminal called 'Git Bash'. It's useful for a few things. The first, it gives the user a very nice color palette that highlights what git branch you're on as well as Linux commands in case you're more accustomed to them. It is not necessary, powershell and cmd both work just as well.

### Git GUI
Git recommends a number of GUIs, old timers will tell you not to use them and to get used to the command line. I've met excellent developers who use both strategies. While starting out it's easier to visualize git relationships using these tools. There are a ton of them, a few that I've tried are.

[Github Desktop](https://github.com/apps/desktop) The GUI I've used the most. Does not require you to be using Github.

[SourceTree](https://www.sourcetreeapp.com/)The GUI I've seen used by the most professional developers.

[Ungit](https://github.com/FredrikNoren/ungit) I'm not familiar with this one but the github README is really good and the xkcd comic at the top sums up the git experience nicely, even when using it alongside 25+ year developers. I'm switching to this one now just to see what it's like. (Postnote: This is no longer maintained, it's probably still ok because git doesn't change much but I would avoid for now. I did however learn about [[Chattanooga Open Data]] from this repository.)

You can use all of these, even all of them at once and pick whichever is simplest or you find the easiest to use.

# Git
Use Git Bash for the following commands because I want to create some files in the command line and I don't want to have to write Bash, Powershell, and CMD commands each time.

For starters, git is never simplified and it should be. People throw all sorts of insane terms at you right out of the gate so here's what you really need to know. Git at its core cares about 3 things. 
1. Repositories
2. Branches
3. Commits

These three things, to git, are nouns. Everything else in git is a verb. Pulls, Pushes, Clones, Forks, Merges, Rebases, everything you can think of is an action that effects your set of Repos, Branches, and Commits. THAT'S IT. The following sections will be sorted by these 3 nouns and the commands that are run on them.

## Repositories
A repository is either a local or a remote copy of a git project. You can link and unlink your local repo to remote repos and even host your own remote repo if you really want. 

### git clone
When you use git clone all it's doing is copying the remote repository to your local, setting you on the main/master branch, and telling you local git that the remote repo is located at whatever url you used. THAT'S IT

### git init
When you do git init it's creating a new repository with no remote copy. You can set this remote copy and then interact with it provided you have the correct permissions to do so.

> [!WARNING]- Practical Shortcut 1
> Your first practical shortcut. If you want to create a new git project DON'T use git init. Create a new project on Github first, clone it, add your files, commit and push to origin. If you git init first I have no idea how to make a new repo on Github and match it up with your local repo, you have to set an origin, create an upstream, blah blah blah. I remedy this by just never doing it.

### git remote add
If you want to add a remote after running git init or if you want to change the remote you're pointing at you can use git remote add. Because of the above practical shortcut you really won't ever have to use this.

## Branches
A branch is a silo of code that (in best practice) contains the changes a developer wants to make for a single feature. Many developers also use specific branches for development, staging, and production. 

> **Practical Shortcut 2**
>
> If you are working on a solo project you probably don't need to make any branches. "HERETIC! SINNER! MADMAN!" I hear you saying. To seriously simplify git you can stick to commits, pushes, and pulls and treat them like save, upload, and download. Use just the main branch and forget about the rest until you really need it or you want to expand your horizons.

### git branch
git branch can be used in a couple of ways. 
```git branch list```
Displays all of the branches available on your local.
```git branch "branch name"```
Creates a new branch with the branch you are currently in as the parent branch, also known as the upstream branch.

### git checkout
git checkout switches the git user to the branch they specify. 
>[!warning]- Practical Shortcut 3
>You can use checkout to both start a new branch and switch to it immediately by running:
>```git checkout -b "branch_name"```
>I use this every time I want a new branch because I always want to switch to it.

### git merge
Getting to git merge is when we introduce some complexity. Git merge takes the changes made in one branch and combines them into another branch. When you use git merge you are merging INTO your current branch the changes FROM the branch you specify. In git Bash this will look like this:
```
yourDesktopName MINGW64 ~yourWorkingDirectory (currentBranch)
$ git merge brachYouWantChangesFrom
```
The default way a merge occurs is by introducing a commit where you describe the branches merged and organize the differences between your branches. You'll often hear about 'fast-forward' merges, this is a special case wherein no changes have occurred on the branch being merged into. Git will do all of the merging for you, it basically simulates making the changes on the branch being merged into.

## Commits
While git branches hold entire features, git commits should hold small incremental code changes. Best practice is to make these small, only containing atomic changes, consider making a commit every time you would have clicked 'save document' in the 90s. 

Commits are important because if you screw something up later on you are going to revert to a specific commit. Packing too many changes into a single commit will risk not being able to isolate your bad changes from the good ones. 
### git status
We're introducing new vocab here so sit tight. When you run git status git will present the changes that have occurred in your repository since the last commit. Some of these will be tracked and some will be untracked. Tracked means that you or another user have told git about the file before. Untracked means the opposite. There are many cases you might want to not track a file such as generated sources, locale-specific settings, or files including secret keys.
> [!note]- Untracked or gitignore?
> If you mean to keep files untracked you should add them to your gitignore, this will keep git from warning you that they are untracked when you run git status.

git status will also show you which files you've modified and what commands you can run next to add these changes to your commit. Run ```git add .``` to add all of the changes and untracked files to your commit. Run ```git add <file_name>``` if you want to add specific files. 

If you accidentally run git add on something you don't want added you can run git reset to remove your additions.

>[!warning]- Practical Shortcut 4
>Adding changes and files is often easier in a GUI. Every good GUI will show you what changes were made in the files and will show you a good list of your changes as well. In all, commits are a good task to undertake in a GUI.
### git commit
git commit takes all of your staged changes and creates a commit out of them. It attaches this commit to the end of your current branch and makes this commit the new HEAD of the branch. COMPLICATED? no. It's just like saving a file. If you want to go back to a previous commit you can use revert just like you can ctrl+z back to a previous version of your file. 
``` git commit -m "Your commit message"```
Add this message or git will launch vim and you'll have to learn how to escape vim (escape -> :q!). 

THATS IT. Don't complicate commits any more than that. And when in doubt, make your commit even if you're not sure of it. Then you can move from commit to commit depending on which changes you want to see.

git stash
This command tucks all of your changes away into a separate location and resets your current directory. This is super useful if you get confused or things start to go awry in your git you can stash your changes and reset back to the last commit on your branch. Then you can push, pull, branch, or whatever else you need to do but your changes will be saved in your stash.
>[!warning]- Practical Shortcut 5
>Oftentimes getting changes out of a stash is a fool's errand. A common workaround from stashing is to copy the changes you've made to a text file, git stash, forget about this stash, and then copy the changes out of the text file and paste them into your now clean local repository. It's messy yes, but development is about simplicity and this is simpler.
# Back to Repositories
Ok, so we've been through creating or cloning a repository, branching from the main, creating commits, and even a little section about merging. Now we're going to talk about pushing, pulling, and merge requests. Believe it or not there are no new concepts introduced here, we are just running merges across remote and local repositories. 

Why did morons have to complicate these things? Because they have forgotten that the heart of engineering is simplification not complication and they know that if they continue to complicate at a rate that out-group people can't keep up they'll always feel superior to the people who aren't in the in-group that sacrifices all of their free time to invent ridiculous new concepts to ever-shrink their in-group. "But Bryce don't highly specialized fields need a highly specialized vernacular to convey complex concepts quickly?" No, these people want to feel superior and for that reason they never will be, speak to any snooty nerd and you will instantly understand this. 

To simplify the above, semantic-andys make everything worse.

### git pull
Git pull is (simply) a fetch and a merge. Fetch is like clone in that you're downloading from a remote repository but fetch means that you only download changes instead of the full project. Merge is what we talked about before, putting the differences from some commit into our desired commit.
```git pull origin main```
Here we're telling git to fetch and merge all of the changes from the remote repository we have defined and nicknamed 'origin', at the repository's branch named 'main', at the most recent commit into our local current branch. THAT'S IT.
origin repo > main branch > most recent commit ----> local repo > current branch

>[!warning]- Practical Shortcut 6
>This is simple if you are developing on 2 different machines and you need to get changes from your remote repository but you never make changes on both machines at once. You won't ever run into merge conflicts. 
>Merging conflicts is best done in GUIs.

> [!warning]- Practical Shortcut 7
> If you find that merge conflicts are really killing your productivity then use the stash shortcut explained above. Stash all of your changes, pull for the most recent, write your changes over the top of what you've pulled. Don't wade in the awful merging conflict resolution, then rebasing, then you have to push because your merging and rebasing made 3 different brand new commits and now your local is different than your remote despite the contents being the exact same because you've got 3 commits that your remote doesn't know about. woops, got carried away.

### git push
git push puts your current local branch onto the remote repository. There are 3 scenarios we might push changes to our remote. 
#### git push origin main
Use this command if you are working in your main branch and you're comfortable making changes directly to it. This is the simplest possible way to push changes but it's really only possible if you're abstaining from making new branches and you're working on main.
#### git push origin some_branch
Use this command if you're working on a different branch from main. Then on github you can create a pull request (called a merge request on gitlab) and get your branch changes into main. This is the most common way I've seen professional developers do things, it makes for really easy code reviews because they're hosted on a website everyone can access instead of your local.
#### git pull origin main -> git push origin main
If you have changes in your remote that you don't yet have in your local you need to catch up before you push to main. This is because the push to main won't go through unless you are able to fast-forward merge. This is complicated, I know but doing a pull and then a push will work. If need be return to shortcuts 7 and 5, stash your changes, pull main, copy your changes in, push to main.
# Sample Workflows
## Simplest possible
We are using only the main branch on both remote and local repositories. This is a perfectly acceptable workflow despite not using branching at all.
``` 
git clone some_repository
# grab your remote repo
for (all of the changes you want to make)
	echo "Hello World" > someFile.txt
	# make some change to the repository
	git status
	# view the modified and untracked files
	git add .
	# add all of the untracked and modified files
	git commit -m "commit message, made some changes"
	# commit your staged changes and leave a descriptive message for posterity
git push origin main
# put all of your changes into your git remote
```
## Using branching
This workflow uses super simple branching only on your local. You'll be keeping your remote repository very simple by maintaining only the main branch. 
``` 
git clone some_repository
# grab your remote repo
for (each feature you want to add)
	git checkout -b some_branch_name
	# create and checkout a new feature branch
	for (all of the changes you want to make)
		echo "Hello World" > someFile.txt
		# make some change to the repository
		git status
		# view the modified and untracked files
		git add .
		# add all of the untracked and modified files
		git commit -m "commit message, made some changes"
		# commit your staged changes and leave a descriptive message for posterity
	git checkout main
	# checkout branch you want to merge changes into
	git merge some_branch_name
	# merge some_branch_name into main
git push origin main
# put all of your changes into your git remote
```
## The 'Professional' way
``` 
git clone some_repository
for (each feature you want to add)
	git checkout -b some_branch_name
	# create and checkout a new feature branch
	for (all of the changes you want to make)
		echo "Hello World" > someFile.txt
		# make some change to the repository
		git status
		# view the modified and untracked files
		git add .
		# add all of the untracked and modified files
		git commit -m "commit message, made some changes"
		# commit your staged changes and leave a descriptive message for posterity
	git pull origin main
	# Necessary becuase someone has already made changes ahead of you
	# Merges origin main into your local, catching you up to main. Resolve conflicts if they occur.
	git push --set-upstream "some_branch_name"
	# Push your change to remote on a new (to the remote) branch called some_branch_name
	> Go to github and create a merge request, review with the team
```
# FAQ
## What if I made changes before branches?
That's ok, I do that all the time. You can still create a new branch and check it out and the changes will transfer to that branch so long as you haven't committed anything yet.

# Remember
When in doubt use the stash trick, it'll skip most of the tedious stuff for you.