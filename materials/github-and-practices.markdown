---
layout: default
title: GitHub and Practices
parent: Materials in English
nav_order: 2
---

# Version control practices 
Version control practices vary from one team to another, but we wanted to give some ideas of what those practices can be. We'll provide examples of what it would mean in a code and what it would mean if you're writing a thesis.

## Content of a commit
Ideally, your commit should have only related changes but only a small amount of them. Keeping commits small and having related changes in a commit means that other people can more easily see what has changed and what's the purpose of the commit. It is also easy to roll back the change if something goes wrong and you don't want to keep the change after all.

*Programming example: a new function that provides some small part of functionality and possibly a test for the function.*

*Thesis example: Changing wording in a paragraph.*

## Committing frequency
Although the changes in a commit should be related, it doesn't mean that you shouldn't commit often. It is often encouraged to commit quite often, because if something goes wrong on your computer, well, then, this happens:
![Screenshot from Slack where a person tells that they lost all the changes they had made during a day because they hadn't committed and their computer froze.](/assets/not_committed.png)
<small>In English: "That feeling when your computer freezes on Friday and destroys a massive component that you've been working on the whole day, saves it as an empty file when restarting and you haven't committed it." </small>  

Another reason is of course that when you commit often, the commits stay small. 

## Commit messages
Because you're committing small changes, it is also very easy to describe the contents of the commit, right? Many people say that describing **why** you made a change is more important that **what** the changes are. I usually try to include both, but ideally, the message should also be quite short, only a few sentences. 

*Programming example: "Wrote a new function to be able to parse price information from XML. Also, wrote a test for it."*

*Thesis example: "Rewrote the definition of bias to make it more understandable for people that are not in this field."* 

## Branches
In every project I have worked in there has been some kind of branching. There's a debate what is the right way to do branching, whether you should have feature branches at all or should you just have one or two branches. I have mostly seen feature branches used and I prefer that way. It's because when you have separate branches, it's harder to mess up the entire project. It also makes it easier to track changes that are going to be deployed. 

*Programming example: A deployable, larger entity, for example, a new feature and tests for all the functions that are written when implementing the feature.*

*Thesis example: A complete section which introduces a new part of the thesis subject.*

## Review
Before the change is merged to the main branch, it is usually a good idea to let someone else check the changes. Even the experienced developers make errors all the time and everyone gets blind to their code, so it's a good idea not to skip the code reviews. You could probably ask someone to review the changes to your thesis, too! In GitHub-partwe introduce  one way of doing reviews.

## Monorepo vs polyrepo  
Monorepo means using one repository for multiple projects and so, polyrepo means having those projects in separate repositories. Selecting which one to use depends on the projects: if there share code and have a common purpose for the projects, then maybe it makes sense to have them together. If they have nothing in common and are not related, maybe keep them in separate repositories. You can find a pretty good comparison of them 
[here](https://github.com/joelparkerhenderson/monorepo_vs_polyrepo#comparisons).

# GitHub

GitHub is a widely used development and collaboration platform. It's not the only one, though, and other similar services are for example Gitlab and BitBucket. The features and pricing differs from one service to another, but the common feature is that they provide hosting for Git repositories. In addition to that, GitHub provides a lot of features that make development and collaboration easier. 

In GitHub, you can have public and private repositories. Public ones are good for when you want to for example have your GitHub profile as a portfolio or when you want to provide a chance to collaborate for other people. Private can be used in for example organizations that don't want to publish their source code or just if you don't want to show everyone your code. Those repositories are your _remotes_.

There are so many features that we're not going to go through all of them, but we're going to go through some of the most important/used features. In my opinion, the most important thing that Github offers (compared to hosting a git server yourself) is that you can easily visualize version control and changes in the source code. The categories of the features are listed in the screenshot below:

![Screenshot from GitHub website that lists categories of GitHub features: code review, project management, integrations, team management, social coding, documentation, and code hosting.](/assets/features_github.jpg)
<small>_(source: [GitHub webpage](https://github.com/features))_</small>

## Pull requests / Code reviews
By pull request, we mean a situation that someone has created a branch and wants to merge it back to the main branch (usually dev or master) so they create a request for someone to approve. Usually, at this point, the new addition or some major fix has been done.

This is a nice way to ensure that someone has looked through changes that are about to be made to the source code. Other people reviewing the code can leave a comment to specific lines, and tell their opinion.

It is even possible to add a setting that requires that a pull request has to be approved before it can be merged. Merge can be performed from GitHub UI or locally.

## Fork
Even if you don't have permissions to a repository, you can fork it. Forking creates a copy of the repository you forked under your account and allows you to make changes to it. In order to get the changes to the original repository, you need to make a pull request. 

## Issues and project boards
GitHub provides tools for project management as well. It enables suggesting new features or reporting bugs and keeping track of the ongoing work. In professional settings projects typically have a separate project management tool, such as Jira, but GitHub boards can be handy for small/open source projects. 

## Wiki  
Documentation is a very important but often overlooked part of projects. On many occasions documentation in separately somewhere else, and is updated lazily. GitHub provides a way to keep documentation coupled with the source code: wikis. In wikis, one can have all project documentation from domain or technical perspective. 

## Security alerts
One hot topic right now on the infosec side is the supply chain attack. Because projects usually use 3rd party libraries and frameworks, they are a vital part of project's security. As security vulnerabilities are constantly found in them, GitHub has created a feature that alerts the team about the vulnerabilities.

## GitHub pages 
GitHub offers you a way to host a website easily and for free. This could be used for example for having your portfolio or website when you apply for a job. The website is built automatically based on code in your repository after some minor settings adjustments. 