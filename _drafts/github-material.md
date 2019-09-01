# GitHub

GitHub is a widely used development and collaboration platform. It's not the only one, though, and other similar services are for example Gitlab and BitBucket. The features and pricing differs from one service to another, but the common feature is that they provide hosting for Git repositories. In addition to that, GitHub provides a lot of features that make development and collaboration easier. 

In GitHub you can have public and private repositories. Public are good for when you want to for example have your GitHub profile as portfolio or when you want to provide chance to collaborate for other people. Private can be used in for example organisations that don't want to publish their source code or just if you don't want to show everyone your code. Those repositories are your _remotes_.

There are so many features that we're not going to go through all of them, but we're going to go through some the most important / used features. In my opinion, the most important thing that Github offers (compared to hosting a git server youself) is that you can easily visualise version control and changes in the source code. The categories of the features are listed in the screenshot below:

![Screenshot from GitHub website that lists categories of GitHub features: code review, project management, integrations, team management, social coding, documentation and code hosting.](../../../images/features_github.jpg)
<small>_(source: [GitHub webpage](https://github.com/features))_</small>

**Pull requests / Code reviews**  
By pull request, we mean a situation that someone has created a branch and wants to merge it back to the main branch (usually dev or master) so they create a request for someone to approve. Usually at this point, the new addition or some major fix has been done.

This is a nice way to ensure that someone has looked through changes that are about to be made to the source code. Other people reviewing the code can leave a comment to specific lines, and tell their opinion.

It is even possible to add a setting that requires that a pull request has to be approved before it can be merged. Merge can be performed from GitHub UI or locally.

**Fork**  
Even if you don't have permissions to a repository, you are able to fork it. Forking creates copy of the repository you forked under your account and let's you make changes to it. In order to get the changes to original repository, you need make a pull request. 

**Issues and project boards**  
GitHub provides tools for project management as well. It enables suggesting new features or reporting bugs and keeping track of the ongoing work. In professional settings project typically have separate project management tool, such as Jira, but GitHub boards can be handy for small/open source projects. 

**Wiki**  
Documentation is very important but often overlooked part of projects. In many occations documentation in separately somewhere else, and is updated lazily. GitHub provides a way to keep documentation coupled with the source code: wikis. In wikis one can have all project documentation from domain or technical perspective. 

**Security alerts**
One hot topic right now in infosec side is supply chain attack. Because projects usually use 3rd party libraries and frameworks, they are vital part of project's security. As security vulnerabilities are constantly found in them, GitHub has created a feature that alerts the team about the vulnerabilities.


**GitHub pages**  
GitHub offers you a way to host a website easily and for free. This could be used for example for having your portfolio or website when you apply for job. The website is built automatically based on code in your repository on website after some minor settings adjustments. 
