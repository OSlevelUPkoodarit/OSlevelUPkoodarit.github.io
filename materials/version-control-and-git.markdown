---
layout: default
title: Version Control and Git
parent: Materials in English
nav_order: 4
---

# Version control and Git

Version control is a system or service that records changes to a file or set of files over time. If you are already familiar with Google Drive or Dropbox, you already kind of know what version control aims to do with code files and why. Some may even have used Overleaf to write their thesis or some school work. The basic idea and motivation for using some kind of version control is the same for all these services: First, it works as a backup - if something happens to your computer or files, then you can always get it back from online service. Second, it's very often that something goes wrong while implementing a new functionality or a feature. Version control allows you to recall a specific version of your work and revert back to that state (a specific file or the entire project). It's also a necessary tool for remote team work for sharing code between developers and for contributing to other people's projects. It allows you to see who last modified something and the changes over time. In this context, we mainly focus on code files, in reality any type of file could be placed under version control.

## Git

Git is a free, open source version control system and it has become quite popular among software developers and companies. Git stores information a little bit differently than some of the other version control systems. The core idea is, that git does not store only changes, but the entire state of the files at a given moment. "Git thinks of its data more like a set of snapshots of a mini filesystem. Every time you commit, or save the state of your project in Git, it basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot." [[Git book]](https://git-scm.com/book). In other words, every version is essentially a state of your files at a specific point in time. One of the pros of using git is that almost everything happens locally. This means that you don't need internet connection for most of the stuff. Git is often used with command line, but nowadays there exists some very handy graphical tools and plugins as well for git.

## The three stages of files

There are three main stages of files in git: **modified**, **staged** and **committed**.

Commit is one of the most important concepts in git, since all the information in git projects is saved as a commit. You can think of a commit as a bundle of changes that have been saved to the local git repository. In other words, committed means that a file has been saved as it currently is to your local git database.
Modified means, that there are some changes in your file, but you have not yet committed it to your database.
Staged means that you have marked a modified file in its current version to go into your next commit snapshot.

## Working directory, staging area, and Git directory

There are also three main sections of a git project: Working directory, staging area, and Git directory. Git directory is the most important part, since it is the "mini file system" or database that stores your files and their metadata. It is also what is copied when you clone the repository from another computer. The working directory is a single checkout of one version of the project, in other words, the files in your computers disk, which you can use and modify. The staging area is part of git directory that stores the information of which files will be included in the next commit.

## Starting a new Git project

When starting a new git project, the git directory needs to be initialized with command:

```
git init
```

This will allow you to run other git commands in the project folder. This will also create a .git subfolder, which contains some metadata of your project.

## Creating a commit

After making any changes to files, the state of a file will automatically change to modified. Before creating a commit, we need to somehow indicate which files will be included in the next commit. This is done by running the command:

```
git add <filename>
```

It is also possible to add all the modified files in the project with a single command:

```
git add .
```

This will add all the files in your current folder and all the files under it. It's quite handy most of the times, since you don't have to hand pick all the files that have changed. Now the state of the files has changed to staged, but the staged files are not yet saved to the git directory. We have only indicated, that we want to save these changed files as they are at the moment in the next commit. Finally, we can actually save the files to the git directory running:

```
git commit -m "Some describing message about the changes"
```

This will change the state of the files to committed. Note that each commit needs to have a message explaining what kind of changes that specific commit introduces and what is the purpose for those changes. This makes it easier to review the project history and progress, but also to roll back any changes and fix bugs later on. If you leave out the flag -m and the message, a text editor will open, where you can write a longer, detailed description below the title message. The commit is then created by saving and exiting the text editor. At this point all the work is still located in your computer. If, for some weird reason, it would explode or get stolen, all the work would still be lost.

## The basic Git workflow

There are usually about three steps in the normal git workflow:

1. Modifying files in the working directory
2. Adding modified files to staging
3. Creating a commit from all the changed files

A good way to chech the current status of project files is to run:

```
git status
```

## Remote repositories

In order to share the code with other developers and create a backup, we need to create a remote repository, which will be connected to the local repository on your computer. This can be done using services like GitHub and GitLab. We cover GitHub in the next part, but for now, it is important to understand the difference between local and remote repositories. When a remote repository is created and connected with the local one, it is possible to transfer information between them. This means, that there are two versions of the same project: **local**, which is on your computer, and **remote**, which is in GitHub, for example. This connection is made running the command:

```
git remote add <remote name> <remote address>
```

Origin is the common naming convention for the remote repository. Note that a single project can have multiple remote repositories. After adding the remote repository for git project, we can finally push the changes there and make sure our hard work won't get lost if something happens to our computer. This can be done by running:

```
git push <remote name> <branch name>
```

We will cover branches in the next chapters. Note that if you add the flag -u after the push command, next time you don't need to specify the name of the remote and the branch to push changes to the same place. What if someone else made changes and you would like to fetch them to your local machine? The changes in the remote repository can be fetched by running:

```
git pull
```

This only works if you already have some version of the project on your local machine. Git pull also changes the local files to reflect the changes pulled from remote. If you only wish to fetch the changes but not change anything yet on your local git directory, it can be done by running:

```
git fetch
```

If you would like to start collaborating in a completely new project and assuming you have access to that repository, you could clone it to your computer by running:

```
git clone <remote address>
```

## Exercises

Let's go through how commit is created and the different stages of files in practice with command line. First, we will create an empty folder and initialize a git project with the command `git init`. Did something change in the folder? Why do we need to do this?

Next, we will create a new text file called "example.txt" inside the folder. Now, let's run the command `git status` and take a closer look on the output.
What are untracked files and why those are mentioned in the output? A good hint might be "nothing added to commit but untracked files present (use "git add" to track)".

Let's add the changes in the new file by running `git add example.txt`. What does `git status` output say about the current status of the file?

After adding the file to the next commit, let's write something in the text file. What does `git status` output say about the current status of the file?

Let's create another file, called "example2.txt" in the same folder.

Let's add all the changes again by running `git add .`. What does the output say?

After making sure both files are to be committed, let's run `git commit -m"My first commit"`. What does the output say about the current status of the files?

In the output, you can find some information about the files. `Changes to be committed` means that the files under that title are successfully staged and hence, will be included in the next commit. Similarly, `Changes not staged for commit` refers to the changes which git is aware of, which will not be added to the next commit. `Untracked files` are not tracked by git. In other words, they are unknown to git, and the changes inside them are not being followed. This also means that the changes will not be added to the next commit. Git also makes it easier for us to follow which files are staged and which are not, since all the staged changes are green and not staged are red in the output. Basically if you run `git status` and see red, you know that there are some changes not staged for the commit. After actually committing the changes, the output tells you the status of your local branch with `nothing to commit, working tree clean`. This means, that there are no changes that git is aware of and that are not yet saved successfully.

There are great graphical tools and plugins for git. There might be some differences between them in which steps are automatically done and which are not. For example. git desktop adds automatically all the files to staging.

## Sources

- [Lapio course material (Computing tools for CS studies)](https://tkt-lapio.github.io)