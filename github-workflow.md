# GitHub Workflow
Important pratices when working with git and GitHub in collaborative settings.

## Table of Contents


## Why Use Git and GitHub
Git is a version control tool designed for any coding projects, however, you can use it to store any digital document you want. Imagine it like Google Docs, you can store your current progress, and can go back to a previous version when you need to, every version you store in git is called a "commit". One extra feature git offers is the ability to write a short description for what you did in each commit, this is called a "comment message".

Note that git only store your project on local device, using the convient pipeline git has with GitHub, all the commits and commit messages of your project can be copied over to a GitHub repository (repo for short), allow other devices and users to download a copy of it and work on it. The action of copying your local git commits to a GitHub repo is called "push".

It is important to realize that GitHub repository only update when someone push to it, and changes to the repo by other devices will only be updated on your local git project when you do a "pull", which means copying over new commits to the repo to your local project.

When using GitHub in a collaborative setting, there are three major concerns to address:
 1. when a user update their local git repo without pulling the new pushed to the GitHub repo, their local repo is now at conflict with the remote repo, like a timeline that is being split into two branches, this is called a merge conflict.
 2. what is shown on the main branch of a GitHub repo should run without known problems. This is because when a member is working on a part of the repo, they do not want a bug in another part updated with other members to be crushing down the project, making it difficult for the member to debug their own part.
 3. it is important to describe your commits in a standardized way so that other members can understand what changes you brought to the repo.

 These concerns can be handled with careful practices, which will be described below.

## Setup Git and GitHub
### Setup Git Locally
Install git through the [official website](https://git-scm.com/downloads) with default settings (include Git Bash) or through command `sudo apt update && sudo apt install git`.

Verify installation with `git --version`.

Configure your git profile:
```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```
Note: if you want to use a different name/email on a certain git project, you can set local profile to that project by not having `--global` tag in the commands above.

Next step is to enerate SSH key for linking to your GitHub account

### Set Up SSH Connection to GitHub
Go to your ssh folder:
`cd ~/.ssh`
If such file does not exist, create one, you will definitely use it for other things in the future.


Generate a new key with a custom name:
`ssh-keygen -t ed25519 -C "your-email@example.com" -f ~/.ssh/github_personal`
Here it will ask you to setup a passphrase (password) for when you use this key, although you can skip it be pressing enter, I suggest setting up a key for git. I like to manually type the passphrase everytime I push to GitHub, but you can store the passphrase in "autofill" using SSH agent.
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/github_personal
```


View your public key:

cat ~/.ssh/github_personal.pub

5. Add Key to GitHub

Go to GitHub → Settings → SSH and GPG Keys → New SSH key

Paste the copied .pub file contents

Save

6. Test SSH Connection
ssh -T git@github.com


Expected output:

Hi username! You've successfully authenticated, but GitHub does not provide shell access.

7. Clone and Push with SSH

Clone your repo:

git clone git@github.com:username/repo.git


Make changes and push:

git add .
git commit -m "Initial commit"
git push origin main

8. Common Issues

Permission denied (publickey) → wrong key or not added to agent

Multiple GitHub accounts → use ~/.ssh/config to manage keys

Windows → always use Git Bash or WSL for SSH setup