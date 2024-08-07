---
layout: post
published: true
title: 'Git and GitHub for Collaboration: a step-by-step tutorial'
date: '2023-09-06'
categories:
  - Tutorial
tags:
  - Git
  - GitHub
---
This post is a quick start manual for beginners to use Git with GitHub for source code control. Although this manual aims for the operations with repositories of GitHub, the instructions apply to general Git practices. This post assumes that you have already set up a GitHub account where you can store your source code and manage the development.
<!--more-->

# Table of Content

{:.no_toc}

* TOC
{:toc}

## Introduce to Git and GitHub

**Git** is an open source and free tool for source control management or what’s referred to as SCM. With Git, you can manage changes to files over time, so you can easily revert to a previous version if necessary. Git is also a distributed version control system, which means that you can work on your code on your own computer and then easily share it with others.

**GitHub** is a hosting service for Git repositories. It provides a place to store your code, collaborate with others, and track issues. GitHub is also a social platform where you can connect with other developers and learn from them.

Git and GitHub are essential tools for software development. They help us to track changes to our code, collaborate with others, and learn from others.

## Install and Configure Git

Many operating systems come with Git pre-installed, especially Linux and macOS systems. To check if Git is already installed on your system, open a terminal window and type the following command:

```bash
git --version
```
If you need to install a Git for your operating systems, please follow instructions from 
[Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

Here are the major steps of installation for Windows and CentOS Linux:

### Download and Install Git for Windows

1. Go to https://git-scm.com/download/win download the lastest version. The download will start automatically. If not, you can manually click the corresponding download links.

![Download Git for Windows]({{site.baseurl}}/img/post/gitlab01.png)

2. When the download finishes, you will get an `.exe` file, and you can double-click it to install. You can keep all default settings during installation.

### Install Git on CentOS Linux
The easiest way to install Git on CentOS Linux is through CentOS's package manager - Yum(Yellowdog Updater, Modified):

```bash
sudo yum install git
```

### Configure Git for the First Time

After installation of Git on your system, if you are using Windows system, you can start `Git Bash` from the **Start Menu**:

![Git Bash from Start Menu]({{site.baseurl}}/img/post/gitlab02.png)

You can also start `Git Bash` from the **Context Menu** through right-clicking from any local directory while pressing the **shift** button:

![Git Bash from Context Menu]({{site.baseurl}}/img/post/gitlab03.png)

You can also use the default command line of your operating system to run git commands. For the first time to run git command, it is a good idea to configure your Git environment by running the following commands: 

```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```
If you need set up proxy for git, you can run the following commands:
```
git config --global http.proxy <proxy_url>
git config --global https.proxy <proxy_url>
```

You can check all your settings through running:

```
 git config --list
```

This command looks for the file of `.gitconfig` from your $HOME directory. On Windows, the $HOME direcotry is usually `C:\Users\$USER`. On Linux, you can check your $HOME directory through command `echo $HOME`.

## Clone a Code Repository from GitHub

You can get a copy of a remote repository from GitHub through the `git clone` command. Click on the **Code** button shown in the following screenshot. There are two ways to connect to the remote repository: **HTTPS** and **SSH**.

![Clone GitHub Repository]({{site.baseurl}}/img/post/github01.png)

### Clone with HTTPS

1. Go to the GitHub repository that you want to clone.
2. Click on the **Code** button.
3. Under the HTTPS tab, copy the URL.
4. In your local terminal, navigate to the directory where you want to clone the repository.
5. Run the following command:

```
git clone <URL_HTTPS>
```

The command would prompt a message asking for the username and password to the remote GitHub repository. Enter your credentials and press Enter.

The remote repository will be cloned to your local directory.

**Note**: Cloning a repository using HTTPS is not the recommended way to do it. This is because it requires you to enter your GitHub username and password every time you want to clone the repository. This can be a security risk, especially if you are cloning the repository from a public computer.


### Clone with SSH

A more secure and convenient way to clone a repository is to use SSH. SSH is a secure protocol that allows you to authenticate to a remote server without having to enter your username and password. To use SSH, you will need to generate an SSH key pair. Once you have generated your SSH key pair, you can add it to your GitHub account. Then, you can clone the repository using the following command:

```
git clone git@<GITHUB_SERVER>.com:<USERNAME>/<REPOSITORY_NAME>.git
```

#### Generate a SSH Key Pair

You can create a new SSH key pair by running the following command in your local terminal. 
```
ssh-keygen -t ed25519 -C "your_email@example.com" -f $HOME/.ssh/<your file name>
```

You can just press Enter to use empty passphrase when the command prompt to ask for passphrase. This command generates two files with names of `<your file name>` and `<your file name>.pub` under the path of `$HOME\.ssh\`.


**Note**: if you are using a legacy system that doesn't support the Ed25519 algorithm, use:.

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f $HOME/.ssh/<your file name>
```

![Generate SSH Key Pair]({{site.baseurl}}/img/post/github02.png)


#### Adding SSH Key to SSH Agent

Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated a new SSH key.

Run the following command to start the ssh-agent in the background:

```
eval `ssh-agent -s`
```

Run the following command to add your SSH private key to the ssh-agent.
```
ssh-add ~/.ssh/<your file name>
```

Add the following settings into ~/.ssh/config file:

```
# my company gitlab production environment
Host *
  PreferredAuthentications publickey
  AddKeysToAgent yes
  IdentityFile ~/.ssh/ado_rsa
```

#### Add the Public Key GitHub Settings

Once you get the SSH key pair, add the SSH public key to your GitHub account settings:

1. Log into GitHub, click your profile photo icon in the upper-right corner of any page, then select **Settings** from the dropdown list.
2. In the "Access" section of the left sidebarSelect, click  **SSH and GPG keys**
3. Click **New SSH key** button in the upper-right corner of the page
4. Copy the content from generated public key file `<your file name>.pub` and paste it in the **Key** box and give the key an informative title for future management
5. Click **Add SSH key**.
  ![Set up SSH Keys in GitHub]({{site.baseurl}}/img/post/github03.png)


#### Clone with SSH Command

Once you set up your SSH key in your GitLab profile, you can run the following command with the corresponding SSH URL to clone the remote repository without inputting your username and password. 

```
git clone <URL_SSH>
```

![Clone with SSH]({{site.baseurl}}/img/post/github04.png)

Once you clone the remote repository to local successfully, you can navigate to the directory through `cd <REPOSITORY_NAME>`:

![Go into local directory]({{site.baseurl}}/img/post/github05.png)

Now, you are inside your working directory, and you can make any changes you like. Once you are happy with the changes, you can `add` and `commit` them to the local repository and then `push` to the remote repository so that your fellow team members can see the changes you made.

![git push flow]({{site.baseurl}}/img/post/gitlab12.png)

Please note that you are in the default **main** branch and all the changes you made are within this branch. And when you push the changes to the remote repo, it will update the **main** branch there. Usually, this is not the best practice. 

## Best Practices for Code Review

Excellent code depends on rigorous review. The following flow are usually the best practices for code review and team collaboration:

* Once checks out a repository, a developer creates a new feature **branch**, makes changes in this feature branch, and tests it. 

* When happy on the changes, the developer **push**es the changes in the **new branch**, and make a **pull request**. 

* The developer assigns the **pull request** to a **reviewer**, who looks at it and makes comments as needed. When the reviewer finishes, he/she can assign it back to the author.

* The author **addresses the comments**. This stage can go around for a while, but once both reviewer and author are happy, they can **approve a merge** or assign it to a final reviewer who can do the merge.

* The final reviewer follows the same reviewing process again. The author again addresses any comments. Once the final reviewer is happy and the build is green, then the new branch will be **merged** with the target branch.


Here are the demos on each of the code review steps.

### Pull from Remote

Before you make any changes, it is always a good idea to run the command `git pull` within the local repository to make sure your current local version is up to date.

![delete local branch]({{site.baseurl}}/img/post/github06.png)

#### Checkout Remote Rranch
Usually you need to check out remote branches created by other developers, here is how you can pull the branches you want:
1. **Fetch all remote branches**
```
git fetch origin
```
This command will fetch all remote branches from the reposity. `origin` is the remote name you're targeting. So if you have an `upstream` remote name, you can run `git fetch upstream`.

2. **List the branches available to checkout**
```
git branch -a
```
This command lists all branches available for checkout. The remote branches are prefixed with `remote/origin`

3. Pull from a remote branch
```
git checkout -b fix-feature-a origin/feature-a-branch
```
This command creates and checks out a new local branch names `fix-feature-a` that pulls all changes from remote branch `origin/feature-a-branch`.

### Create a New Branch

Branches let you work on new features or bug fixes of the main project code in the `master` branch. You can use `git branch <BRANCH_NAME>` to create a new branch and `git branch` to check your branches.

![create a new branch]({{site.baseurl}}/img/post/github07.png)

Note the asterisk next to the `main`, which indicates that you are currently in the `main` branch. To switch to your new branch, you need to run `git checkout <BRANCH_NAME>`.

![swith branch]({{site.baseurl}}/img/post/github08.png)

### Commit Changes

Now, you are in the new feature branch and ready to change your codes. 

#### git status

Once you finish your changes, you can run `git status` to check the changes you have made.


![check changes]({{site.baseurl}}/img/post/github09.png)

#### git add

You can run the command `git add <FILE_NAME>` (add the specific file) or `git add .` (add all files) to add your changes to the staging area. A staging area is an intermediate place between your working directory and local Git repo where any changes that you've made can be reviewed before you actually commit them to the repo.

![check changes]({{site.baseurl}}/img/post/github10.png)

#### git commit

Next, you can commit the changes to your local repo through running `git commit -m "MESSAGE_TEXT"`.

![commit changes]({{site.baseurl}}/img/post/github11.png)

#### git push

After committing to the local repo, you can push the commits from the local to the new branch in the remote repo through running `git push -u origin <BRANCH_NAME>`.

![push changes ]({{site.baseurl}}/img/post/github12.png)

#### merge request

Once you push the local to the new branch in the remote repository, you can submit a pull request through **Pull Requests** tab and then **New pull request** button on the remote repository page.

![merge request]({{site.baseurl}}/img/post/github13.png)

The **New pull request** button will pop up the **Open a pull request** page, where you can:

1. fill the title of the request;
2. write a brief description or comments;
3. assign reviewer(s) from the drop down list; 
4. add tags and labels;
5. link work item(s) from the drop down list;

![merge request]({{site.baseurl}}/img/post/github14.png)


Once the pull request has been submitted, the reviewer(s) will get notification and they can go the request page to do: 

1. check the commits and changes; 
2. write comments; 
3. approve the merge (if applicable);
4. request changes (if applicable).
![merge request]({{site.baseurl}}/img/post/github15.png)

After the changes have been approved, the branch can be merged to the target branch through the **Merge pull request** button.
![merge request]({{site.baseurl}}/img/post/github16.png)

#### delete the merged branch

Once your new branch has been merged to the target branch in the remote repository, you can delete the merged branches from the **branches** tab in the GitHub repository.
![merge request]({{site.baseurl}}/img/post/github17.png)

You can delete branch from your local repository by running 
`git branch -D <BRANCH_NAME>`. 
Note, you have to get out of the branch before you run this command deleting it.

![delete local branch]({{site.baseurl}}/img/post/github18.png)

#### pull from remote

Now, it will be a good practice to run `git pull` again to synchronize your remote repository to your local.


I hope this quick-start tutorial is helpful to you. Please feel free to leave any comments and advice. Thanks for reading.

## References

* https://git-scm.com/book/en/v2
* [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/enterprise-server@3.6/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux)
