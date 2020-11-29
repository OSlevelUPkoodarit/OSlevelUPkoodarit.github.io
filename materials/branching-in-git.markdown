---
layout: default
title: Branching in Git
parent: Materials in English
nav_order: 3
---

# Branching

Once the team and the projects grow, you may encounter issues with making changes at the same time. 
They can also be a way of project management: if all the features are implemented in branches then it's easier to make sure that incomplete features are not deployed. 

By default, all repositories have **master** branch. It is usually the main branch that is used for deploying changes but it doesn't have to be. Git doesn't restrict the number of branches but it is considered good practice to remove old, unused branches. 

Creating a branch means that you make a copy of a repository in its current state and can make changes to it without affecting the original branch. When you have done all the changes, you can merge it back to the original branch, which means it adds changes from the new branch to the old one. You can switch between branches easily even though you haven't finished everything in a branch.

Creating a new branch:
```
git branch testbranch
```
where git indicates that you want to use git commands and branch testbranch tells that you want to create a new branch with name testbranch. 

and then you need to move to a new branch to make the changes there:
```
git checkout testbranch
```
You can change back to the master branch with the following command:
```
git checkout master 
```
You can list all branches you currently have with the following command:
```
git branch 
```
\* in front of a branch name indicates that you're currently making changes to that branch. 

## Merging and rebasing
Merging means combining the contents of two things into one. In version control case this usually means that we want to merge changes made in a separate (feature) branch back into the main branch. There are two ways of doing this:

```
git checkout master 
git merge feature 
```

```
git checkout feature
git rebase master
git checkout master
git merge feature
```

The difference is that when you merge, the version control history is not rewritten and the version control has sidepaths (branches). Rebase will relocate your commit to be the latest ones, thus rewrites the history but at the same time, keeps version control "clean" and linear. The difference can be hard to understand at first, but luckily there is [git visualization tool by GitHub](http://git-school.github.io/visualizing-git/)!

This is your first branching exercise (in visualization tool): 
1. Make a commit in master
2. Create a new branch with a name that you come up
3. Checkout the new branch
4. Make a few commits (for some reason adds are not needed)
5. Checkout master
6. Make a few commits 
7. Merge/rebase new branch into master

Do this twice and try both merging and rebasing to see the difference.

Second exercise: complete first Introduction Sequence in [this git practice environment](https://learngitbranching.js.org/). You can do others, too, but they go beyond the scope of this workshop. 


## Merge conflicts
Sometimes merging changes doesn't go as planned. When multiple people change the same content and then try to push/merge, merge conflicts occur. This happens because the version control system cannot know which one is the correct content or if both are correct but incomplete. When a merge conflict occurs, someone (the one trying to push/merge changes later) has to decide which change is correct and fix the files manually or with a tool.

The file with a merge conflict shows where the conflict has occurred. Conflicted lines look like this:
```
When a merge conflict occurs
<<<<<<< HEAD
fix the issue manually.
=======
use a tool to resolve it.
>>>>>>> feature-branch
```
The line before ======= shows what was in the repository when you tried to pull. Line after it shows your changes. This can be manually resolved by simply removing the text that is invalid and also the lines that indicate the conflict. 



Exercise:
This time we will cause merge conflict on purpose so that you have experience in fixing it. If you're working solo on a project it is very likely that you don't encounter them, but when working in teams it is vital to know how to fix them. This is something you need to on your GitHub account and in the repository that you've already created. 

1. Create a file to a repository if you don't already have one. Write a line of text to it and push it to the remote repository.
2. Clone a second copy of the repository on your computer. Now you will have the same repository twice. 
3. Change the file in both repositories and commit them. It is important that you change the text that you already wrote there. 
4. Push the changes from one local copy to remote.
5. Change to other copy and pull the changes, you should now have a merge conflict!
6. Fix it manually or using a tool!