# git-essentials
A bare-minimum walkthrough to get started with using git with github.

## Getting a repository

A git repository represents a project's entire history (except for untracked or ignored files) - and the current state of the project too.  

### Start your own git repo

To start your own git repository on your local machine use: 

```bash
cd <your-project-directory>
git init 
git add -A
git commit -m 'initial commit'
```

Here, we're creating an empty git repository that doesn't contain anything - all files are untracked!  To resolve this, we use `git add -A`, which does two things - adds all of the files in your project to git's list of tracked files, *and* stages those files for commit. 

That means that the subsequent `git commit -m 'initial commit'` records the creation of those files - with all of their present content - in git.  The `-m` just lets you put a short one-line message with your commit - for posterity, and the good of those who have to try to find out why you've done what you have. 

If you're using github, you probably want to create a repository (unless it's the contents of your codebase is private), and push up your new repo - so there's a *remote* copy on github, and a local one too. 

After [creating a respository on github](https://help.github.com/articles/create-a-repo/) (and do not create a readme..), execute the following to set up the github repository as one of your remote repositories. 

```bash
git remote add origin <https-git-address-from-github>
git push -u origin master
```

This adds the github repo as the `origin` remote repo, and pushes your current project state up to it.  the `-u` flag in `git push -u origin master` means that your local git repository regards the `origin` remote repository as the 'upstream' one.  All subsequent uses of `git push` will automagically push changes to that remote as a result. 

### Clone an existing repository from git

Setting up is much simpler if there is already a git repository on github: 

```bash
cd <the-directory-you-keep-your-projects-in>
git clone <https-git-address-from-github>
cd <name-of-project>
```

Aaand you're done.  

## Inspecting the current state

It's perfectly normal, in the throes of a particularly emersive wrestle with a problem, to forget which files you've added, which you've edited, and which you've removed since your last commit.  

You can access a summary using `git status` - or, even better (in my view) - its sleeker cousin: 

```bash
git status -s
```

Rule of thumb - if you can't tell what anything means in `git status -s`, just use the regular `git status`, and it'll give you the fuller explanation you probably wanted. As time goes by, you'll find yourself reaching for the full `git status` less and less, as you get more accustomed to the shorter form the `-s` flag offers.

## Commiting changes 

As you work on the project, you can observe what has changed between your last commit and now be using the `git diff` command: 

```bash
git diff
```

This will show you what lines you have removed and added since you last commited.

Once you're happy with your changes, it's time to stage the files and commit them. 

```bash
git add -A
git commit 
```

As before, `git add -A` adds all changes to git, staging them for commit.  You'll notice that `git commit` has not got the `-m` flag anymore - because now you've done some real work, a better summary is due than a one liner.

Instead, `git commit` should open some kind of text editor.  Enter a short summary line first, then hit enter twice, and write out a longer explanation of what the change(s) you've made are.  Hit save (whatever save looks like in your editor..) and you're done - all committed. 

If you're being especially good (and if it's possible), having commits that each do a single job is often preferable than one end-of-session commit.  Commit early, commit often, and push often too.  That way, you can wind back time in a granular way, and have a backup available on the internet in case you've stuffed up somehow. 

## Pushing changes to github

Once you've got some new commits locally, you can share them in the github repo with git push: 

```bash
git push
```

## Taging releases

```bash
git tag
```
To list available tags

You can create tags in two ways: 

### Annotated tags

```bash
git tag -a v1.0 -m 'version 1.0'
```

### Lightweight tags

```bash
git tag v1.1
```
To create a lightweight tag we don't supply the -a -m options. It is common to append the tag with `lw` ie `git tag v1.1-lw` but it is not necessary

## Pulling changes from github

If someone else has made updates to the github project (or you have from another machine..), you can get up to date by running: 

```bash
git pull
```

## Avoiding tracking files

It's often necessary to *avoid* tracking some files. This will include all ephemeral artifacts assocaited with your work - files respresenting your repl session, data for local use, dotfiles representing your personal preferences (like IDE settings) - as well as files containing sensitive data.  You'd never put people's private information on a public github repo without explicit consent, of course, but be careful not to put API secrets & tokens there too. 

**BEFORE** you add any file to git, it's advisable to create a `.gitignore` file, fill it in appropriately and run `git add .gitgnore` first.  You can find example files in the [github gitignore](https://github.com/github/gitignore/) repository.  For example, if you're using R for your project, your [gitignore might want to look something like](https://github.com/github/gitignore/blob/master/R.gitignore)

## Notable exceptions

In this quick-start guide, we've not covered what branches are, and how to use them.To start with, this might not be immediately necessary information (although branching, branches, merging, and all the associated joy of that, are definitely good things when done properly). 

It's also true that merge conflicts may occur if you pull from a github repo that someone else is updating - in this case, reach for the internet to teach you what to do.  It's probably too much to learn in your first sitting. :) 

There are also better workflows for staging changes for commit - particularly using the `git add -p` utility, which allows you to review each change and decide if you want to add it interactively. 
Topics for later learning!

## Helpful Resources

This is very much the bare minimum of what you need to know to get started - and do useful things - with git + github.  You'll find a whole load more information (well written too) in the [Git Book](https://git-scm.com/book/en/v2)
