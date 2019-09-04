# Branching

Once the team and the projects grow, you may encounter issues with making chances at the same time. 
They can also be way of project management: if all the features are implemented in branches then it's easier to make sure that incomplete features are not deployed. 

By default all repositories have **master** branch. It is usually main branch that is used for deploying changes but it doesn't have to be. Git doesn't restrict the amount of branches but it is considered good practice to remove old, unused branches. 

Creating a branch means that you make a copy of repository in its current state and can make changes to it without affecting the original branch. When you have done all the changes, you can merge it back to the original branch, which means it adds changes from new branch to the old one. You can switch between branches easily even though you haven't finished everything in a branch.

Creating a new branch:
```
git branch testbranch
```
where git indicates that you want to use git commands and branch testbranch tells that you want to create a new branch with name testbranch. 

and then you need to move to a new branch in order to make the changes there:
```
git checkout testbranch
```
You can change back to master branch with the following command:
```
git checkout master 
```
You can list all branches you currently have with the following command:
```
git branch 
```
\* in front of a branch name indicates that you're currently making changes to that branch. 

#### Merging and rebasing
Merging means combining contents of two things into one. In version control case this usually means that we want to merge changes made in a separate (feature) branch back into main branch. There are two ways of doing this:

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

The difference is that when you merge, the version control history is not rewritten and the version control has sidepaths (branches). Rebase will relocate your commit to be the latest ones, thus rewrites the history but at the same time, keeps version control "clean" and linear. The difference can be hard to understand at first, but luckily there is [git visualisation tool by GitHub](http://git-school.github.io/visualizing-git/)!

This is your first branching exercise (in visualisation tool): 
1. Make a commit in master
2. Create new branch with name that you come up
3. Checkout the new branch
4. Make a few commits (for some reason adds are not needed)
5. Checkout master
6. Make a few commits 
7. Merge / rebase new branch into master

Do this twice and try both merging and rebasing to see the difference.

Second exercise: complete first Introduction Sequence in [this git practice environment](https://learngitbranching.js.org/). You can do other's, too, but they go beyond the scope of this workshop. 


##### Merge conflicts

