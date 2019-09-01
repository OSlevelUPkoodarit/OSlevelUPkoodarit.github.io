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
* in front of a branch name indicates that you're currently making changes to that branch. 

#### Merge conflicts

