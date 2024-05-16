---
title: Github workflow
author: ivan
date: 2024-05-16 20:00:00 +0800
categories: [programming]
tags: [github, workflow]
---

## Introduction

For a lot of us, no matter you are a student or a professional developer, coding has been a part of our daily life. However, managing your project can be a headache if you have multiple versions of coding scripts and you need to switch back and forth between different versions. This is where Github comes in handy. Github is a version control system that allows you to manage your project in a more organized way. In this article, I will introduce the basic workflow of Github and how you can use it to manage your project.

## Basic terminologies

### Git and Github

Before we dive into the workflow, let's first understand the difference between Git and Github. Git is a version control system that allows you to track changes in your project. It is a command-line tool that you can use to manage your project locally. On the other hand, Github is a web-based platform that allows you to host your project online. It provides a graphical user interface that makes it easier to manage your project and collaborate with others. You can think of Git as the engine that powers Github, and Github as the platform that makes it easier to work with Git. 

### Key concepts

1. **Repository**: A `repository` is like a folder that contains all the files of your project. You can think of it as a project folder that stores all the files related to your project.

2. **Branch**: A `branch` is like a parallel universe where you can make changes to your project without affecting the main project. You can create a new branch to work on a new feature or fix a bug, and then merge the changes back to the main project.

3. **Add**: An `add` is the process of adding files to the staging area. When you make changes to your project, you need to add the files to the staging area before you can commit the changes.

4. **Commit**: A `commit` is a snapshot of your project at a specific point in time. When you make changes to your project, you need to commit the changes to save the snapshot.

5. **Clone**: A `clone` is a copy of a repository that you can work on locally. When you clone a repository, you download a copy of the repository to your local machine and can make changes to the project locally.

6. **Push**: A `push` is the process of uploading the changes from your local machine to the remote repository. When you make changes to your project locally, you need to push the changes to apply the changes to the remote repository.

7. **Pull**: A `pull` is the process of downloading the changes from the remote repository to your local machine. When you work on a project with others, you need to pull the changes from the remote repository to get the latest changes.

8. **Merge**: A `merge` is the process of combining the changes from one branch to another. When you create a pull request, you need to merge the changes to apply the changes to the main project.

9. **Pull request**: A `pull request` is a request to merge the changes from one branch to another. When you finish working on a new feature or fixing a bug, you can create a pull request to merge the changes back to the main project.

10. **ssh key**: An `ssh key` is a secure way to authenticate your identity when you interact with the remote repository. You need to create an ssh key to authenticate your identity when you push or pull changes to the remote repository.


## Work on your own project

Now that we have a basic understanding of Github, let's dive into the workflow. The basic workflow of Github consists of the following steps:


### Step 1: Setting up Github

Before you can start using Github, you need to create an account on Github. You can sign up for a free account on [Github](https://github.com/) by providing your email address, username, and password. Once you have created an account, you can create a new repository to store your project files. You can create a new repository by clicking on the "New" button on the Github homepage and providing a name for your repository. You can also add a description and choose whether the repository should be public or private. Let's say you have created a repository called "my-project" to store your project files.


### Step 2: Setting up Git

Before you can start using Github, you need to install Git on your computer. You can download Git from the official website [here](https://git-scm.com/). Once you have installed Git, you need to configure your Git username and email address on your computer. You can do this by running the following commands in the terminal:

```console
$ git config --global user.name "<your_username>"
$ git config --global user.email "<your_email@example.com>"
```
### Step 3: Setting up the ssh key

Before you can start using Github, you need to create an ssh key on your computer so that you can authenticate your identity when you interact with the remote repository. You can create an ssh key by running the following command in the terminal:

```console
$ ssh-keygen -t ed25519 -C "<your_email@example.com>"
```

if you are using MacOS, you can run the following command in the terminal:

```console
$ ssh-keygen -t rsa "<your_email@example.com>"
```

The default location for the ssh key is `~/.ssh`. There are two files generated: `id_ed25519` and `id_ed25519.pub`. On MacOS, the default names of the two files are `id_rsa` and `id_rsa.pub`. The `id_ed25519` (`id_rsa`) file is the private key, and the `id_ed25519.pub` (`id_rsa.pub`) file is the public key. Please note that the private key should be kept secret and should not be shared with others. The public key is the key that you need to add to your Github account. You can view the public key by running the following command in the terminal:

```console
$ cat ~/.ssh/id_ed25519.pub
```

or on MacOS:

```console
$ cat ~/.ssh/id_rsa.pub
```

Then you can copy the public key and add it to your Github account. You can do this by going to the "Settings" page on Github, clicking on the "SSH and GPG keys" tab, and then clicking on the "New SSH key" button. You can paste the public key into the "Key" field and provide a title for the key. Once you have added the public key to your Github account, you can authenticate your identity when you interact with the remote repository.


### Step 4: Cloning the repository

Once you have set up Github, Git and ssh key, you can clone the repository to your local machine. You can do this by running the following command in the terminal:

```console
$ git clone git@github.com:your_username/my-project.git 
```

This command will download a copy of the repository to your local machine and create a new folder called `my-project` to store the project files. The default location is `~` (i.e., `C:\Users\your_pc_username` or `/Users/your_mac_username`). You can also specify a different location by providing a path after the repository URL. For example, if you want to clone the repository to the `Documents` folder, you can run the following command:

```console
$ git clone git@github.com:your_username/my-project.git ~/Documents
```

### Step 5: Making changes to the project

Once you have cloned the repository to your local machine, you can make changes to the project files. Try to imagine that your local project is consist of two parts: the local git repository and local machine. The local git repository is where all the commits are stored. The local machine is where the actual files are stored. Notice that the default branch is `main`, you can create a new branch to work on a new feature or fix a bug by running the following command in the terminal:

```console
$ git checkout -b new-feature
```

This command will create a new branch called `new-feature` and copy all the files from the main branch to the new branch. You can make changes to the project files in the new branch without affecting the main project. Once you have made changes to the project files, you need to check the changes you have made to the files. You can do this by running the following command in the terminal:

```console
$ git status
```

This command will show you all the modified files and untracked files in the project folder. Once you have confirmed the changes, you can add the files to the local git repository by running the following command in the terminal:

```console
$ git add .
```

This command will add all the files in the project folder to the local git repository. You can also add specific files by providing the file name after the `git add` command. For example, if you want to add a file called `index.html`, you can run the following command:

```console
$ git add index.html
```

Once you have added the files to the local git repository, you can commit the changes by running the following command in the terminal:

```console
$ git commit -m "Add new feature"
```

This command will save a snapshot of the project files at a specific point in time. You can provide a message to describe the changes that you have made in the commit. Once you have committed the changes, you can push the changes to the remote repository by running the following command in the terminal:

```console
$ git push origin new-feature
```

This command will upload the changes from the new branch to the remote repository (Github). You can view the changes on the Github website by going to the repository page and clicking on the "Branches" tab. However, the changes are not applied to the main project yet. You need to merge the changes to the main project by running the following command in the terminal:

```console
$ git checkout main
$ git merge new-feature
$ git push origin main
```

This command will switch back to the main branch, merge the changes from the new branch to the main branch, and push the changes to the remote repository. You can view the changes on the Github website by going to the repository page and clicking on the "Commits" tab. The changes are now applied to the main project, and you can switch to the new branch to work on a new feature or fix a bug.


## Collaborating with others

Above is the basic workflow of Github. If you are working on a project with others, and you found that there is a new commit on the main branch after you push the changes to the new-feature branch, you need to pull the changes from the main branch first to get the latest changes. You can do this by running the following command in the terminal:


```console
$ git pull origin main
```

Then, you need to change back to the new-feature branch and try to merge the changes from the main branch to the new-feature branch by running the following command in the terminal:

```console
$ git checkout new-feature
$ git rebase main
```

This command will apply the changes from the main branch to the new-feature branch. Notice that we are using `rebase` instead of `merge` here. The difference between `rebase` and `merge` is that `rebase` will apply the changes from the main branch to the new-feature branch in a linear way (i.e., your commit in the new-feature branch will be applied based on the new commit on the main branch), while `merge` will create a new commit to merge the changes from the main branch to the new-feature branch. There might be conflicts when you rebase the changes and you need to resolve the conflicts by editing the files manually. Once you have resolved the conflicts, you can push the changes to the remote repository by running the following command in the terminal:

```console
$ git push -f origin new-feature
```

This command will force push the changes to the remote repository. The changes are now applied to the new-feature branch, and you can create a pull request to merge the changes back to the main project. You can do this by going to the repository page on Github, clicking on the "Pull requests" tab, and then clicking on the "New pull request" button. You can provide a title and description for the pull request and then click on the "Create pull request" button. Once you have created the pull request, you can wait for the project owner to review the changes and merge the changes to the main project.

Now that the main branch has been updated, you can first delete the new-feature branch on Github by going to the repository page, clicking on the "Branches" tab, and then clicking on the "Delete branch" button. After that you can delete the new-feature branch and pull the latest changes from the main branch by running the following command in the terminal:

```console
$ git branch -d new-feature
$ git pull origin main
```

This command will delete the new-feature branch and pull the latest changes from the main branch to your local machine. You can now switch to the main branch and create a new branch to work on a new feature or fix a bug.

## Conclusion

In conclusion, Github is a powerful tool that allows you to manage your project in a more organized way. By following the basic workflow of Github, you can work on a project more efficiently and collaborate with others more effectively. If you have any questions or suggestions, please feel free to leave a comment below. Thank you for reading!






