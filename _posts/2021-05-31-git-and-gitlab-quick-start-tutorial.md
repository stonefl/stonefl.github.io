---
layout: post
published: true
title: Git and GitLab Quick Start Tutorial
date: '2021-02-15'
categories:
  - Tutorial
tags:
  - Git
  - GitLab
  - GitHub
---
This post is a quick start manual for beginners to Git or GitLab. Although this manual aims for the GitLab Enterprise edition on Windows, the instructions apply to general Git and GitLab/GitHub practices. This post assumes that you have already set up a GitLab web account where you can restore and manage your source code. 
<!--more-->

## Download and Install Git for Windows
The following instructions are for installing Git on Windows, if you need to install Git for other operating systems, please follow the instructions on [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

Go to https://git-scm.com/download/win and the download will start automatically. If the download doesn't start automatically, you can manually do so through clicking the download links.

![Download Git for Windows]({{site.baseurl}}/img/post/gitlab01.png)

When the download finishes, you will get an `.exe` file and you can double-click it to install. You can keep all default settings during installation.

## Configure Git for the First Time
After installation of Git your Windows system, you can start `Git Bash` from the **Start Menu**:

![Git Bash from Start Menu]({{site.baseurl}}/img/post/gitlab02.png)

You can also start `Git Bash` from the **Context Menu** through right-click from any local directory:

![Git Bash from Context Menu]({{site.baseurl}}/img/post/gitlab03.png)

Once you start your `Git Bash` for the first time, it is a good idea to customize your Git environment through running the following commands. Note, the setting commands only need to run once.
```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```
You can check all your settings through running:
```
 git config --list
```
On Windows systems, this command  looks for the file `.gitconfig` from your $HOME directory, which usually is `C:\Users\$USER`.

## Clone a GitLab Repository
You can get a copy of a remote repository on GitLab through `git clone` command. As shown in the following picture, there are two ways to connect to the remote repository: **HTTPS** and **SSH**.

![Clone GitLab Repository]({{site.baseurl}}/img/post/gitlab04.png)

### Clone with HTTPS
You can copy the URL to the HTTPS and run the following command to clone the remote repository to your local directory. The command would prompt message asking for the username and password to the remote GitLab project.
```
git clone <URL_HTTPS>
```
![Clone with HTTPS]({{site.baseurl}}/img/post/gitlab05.png)

### Clone with SSH

Cloning with SSH is securer and is the recommended way by FedEx Enterprise. To clone with SSH connection, you need to follow the instructions below to set up SSH Key in your GitLab profile.

#### Generate SSH Key Pair
You can create a new SSH key pair through running the following command in the `Git Bash` or `PowerShell`. You can use the default key file name and empty passphrase. This command generates two files with names of `id_rsa` and `id_rsa.pub` under the path of `C:\Users\$USER\.ssh\`.

```
ssh-keygen -t rsa -b 4096 -C "<USERNAME>" -f $HOME/.ssh/gitlab_rsa
```

![Generate SSH Key Pair]({{site.baseurl}}/img/post/gitlab06.png)


#### Configure SSH in SSH Agent
Run the following commands 
```
eval `ssh-agent -s`
ssh-add ~/.ssh/gitlab_rsa
```
Add the following settings into `~/.ssh/config` file. Generate a new one if it doesn't exist yet:
```
# FedEx gitlab production environment
Host gitlab.prod.fedex.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/gitlab_rsa
```
#### Set up SSH Keys in GitLab Profile

Once you get the SSH key pair, set up the SSH key through the following steps:
* Log into GitLab, click your profile picture in the upper-right corner of the page
* Select **Settings** from the dropdown list
* Select **SSH Keys** from the **User Settings** on the left menu
* Copy the content from generated `id_rsa.pub` and paste it in the **Key** box and set up the expiration date if needed
* Click **Add key**, you will get an email notifying you added a key to your profile.
![Set up SSH Keys in GitLab]({{site.baseurl}}/img/post/gitlab07.png)


#### Clone with SSH Command
Once you set up your SSH key in your GitLab profile, you can run the following command with corresponding SSH URL to clone the remote repository without inputting username and password. 
```
git clone <URL_SSH>
```
![Clone with SSH]({{site.baseurl}}/img/post/gitlab08.png)

Once you clone the remote repository to local successfully, you can navigate to the directory through `cd <REPOSITORY_NAME>`:

![Go into local directory]({{site.baseurl}}/img/post/gitlab09.png)

Now, you are inside your working directory and you can make any changes you like. Once you are happy with the changes, you can `add` and `commit` them to the local repository and then `push` to the remote repository so that your fellow team members can see the changes you made.

![git push flow]({{site.baseurl}}/img/post/gitlab12.png)

Please note that you are in the default **master** branch and all the changes you made are within this branch.  And when you push the changes to remote repo, it will update the **master** branch there. Usually, this is not the best practice. 

## Best Practices for Code Review

Excellent code depends on rigorous review. The following flow might be the best practices for code review and team collaboration:
* Once check out a repository, a developer creates a new feature **branch** and makes changes this feature branch and tests it. 
* When the developer is happy on the changes, then he/she **push**es the changes to the **new branch**, and make a **merge request**. 
* The developer assigns the **merge request** to a **reviewer**, who looks at it and makes comments as appropriate. When the reviewer finish, he/she can assign it back to the author.
* The author **addresses the comments**. This stage can go around for a while, but once both reviewer and author are happy, they can approve a merge or assign it to a final reviewer who can do the merge.
* The final reviewer follows the same reviewing process again. The author again addresses any comments. Once the final reviewer is happy and the build is green, then the new branch will be **merged to the target branch**.

### Pull from Remote
Before you make any changes, it is always a good idea to run command `git pull` to make sure your current local repository is up to date.

![delete local branch]({{site.baseurl}}/img/post/gitlab21.png)

### Create a New Branch
Branches let you work on new features or bug fixes of the main project code that is in the `master` branch. You can use `git branch <BRANCH_NAME>` to create a new branch and `git branch` to check your branches.

![create a new branch]({{site.baseurl}}/img/post/gitlab10.png)

Note the asterisk next to the `master` which indicates that you are currently in the `master` branch. To switch to your new branch, you need to run `git checkout <BRANCH_NAME>`.

![swith branch]({{site.baseurl}}/img/post/gitlab11.png)

### Commit Local Changes
Now, you are in the new feature branch and are ready to make changes to your codes. 

#### git status
Once you finish your changes, you can run `git staus` to check the changes you have made.


![check changes]({{site.baseurl}}/img/post/gitlab13.png)

#### git add
You can run command `git add <FILE_NAME>` (add the specific file) or `git add .` (add all files) to add your changes to the staging area. The staging area is an intermediate place between your working directory and local Git repo where any changes that you've made can be reviewed before you actually commit them to the repo.

![check changes]({{site.baseurl}}/img/post/gitlab14.png)

#### git commit
Next, you can commit the changes to your local repo through running `git commit -m "MESSAGE_TEXT"`.

![commit changes]({{site.baseurl}}/img/post/gitlab15.png)

#### git push
After commit to local repo, you can push the commits from the local to the new branch in the remote repo through running `git push -u origin <BRANCH_NAME>`.

![push changes ]({{site.baseurl}}/img/post/gitlab16.png)

#### merge request
Once you pushed the local to the new branch in remote repository, you can submit a **merger request** through the URL in above command or from **Project** -->**Branches** in the GitLab page.

![merge request]({{site.baseurl}}/img/post/gitlab17.png)

The **Merge Request** button will pop up the **New Merge Request** page, where you can: 1) fill the title of the request; 2) write a brief description; 3) assign reviewer(s), Milestone and Labels; and 4) set up approval rules.  

![merge request]({{site.baseurl}}/img/post/gitlab18.png)



Once the merge request has been submitted, the reviewer(s) will get notification and they can go the request page to do: 1) check the commits and changes; 2) write comments; 3) approve the merge (if applicable); or 4) close the merge request (if applicable).

![review merge request]({{site.baseurl}}/img/post/gitlab19.png)

#### delete local branch
Once your new branch has been merged to the target branch in the remote repository, you can delete your local branch through running `git branch delete -d <BRANCH_NAME>`.  Note, you have to get out of the branch before you running this command deleting it.

![delete local branch]({{site.baseurl}}/img/post/gitlab20.png)

#### pull from remote
Now, it will be a good practice to run `git pull` again to synchronize your remote repository to your local.

## References

* https://docs.gitlab.com/ee/gitlab-basics/start-using-git.html
* https://about.gitlab.com/images/press/git-cheat-sheet.pdf
* https://about.gitlab.com/blog/2017/03/17/demo-mastering-code-review-with-gitlab/ 
* GitLab Get Started: https://about.gitlab.com/get-started/
* GitLab Learn: https://about.gitlab.com/learn/
* https://git-scm.com/book/en/v2
