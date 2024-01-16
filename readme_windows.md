# Git Installation and GitHub SSH Connection Guide

This guide provides detailed instructions on installing Git and setting up a secure SSH connection with GitHub. Additionally, it covers essential Git commands for managing both local and remote repositories.

## Table of Contents

1. [Git Installation](#git-installation)
2. [Git Bash Configuration](#git-bash-configuration)
3. [GitHub SSH Connection](#github-ssh-connection)
4. [Basic Git Commands](#basic-git-commands)
5. [Managing Remote Repository](#managing-remote-repository)

## Git Installation

1. Download Git for Windows from [git-scm.com](https://git-scm.com/download/win).
2. Run the installer and follow the on-screen instructions.


## Git Bash Configuration

1. Set user name:

```bash
git config --global user.name "Your Name"
```

2. Set email:

```bash
git config --global user.email "your_email@example.com"
```

## GitHub SSH Connection

1. Generate SSH key:

- Paste the text below, replacing the email used in the example with your GitHub email address.

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

> Note: If you are using a legacy system that doesn't support the Ed25519 algorithm, use:

```bash
 ssh-keygen -t rsa -b 4096 -C "<your_email@example.com>"

```

2. Auto-launching ssh-agent on Git

- You can run ssh-agent automatically when you open bash or Git shell. Copy the following lines and paste them into your ~/.profile or ~/.bashrc file in Git shell:

```bash
env=~/.ssh/agent.env

agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

agent_start () {
    (umask 077; ssh-agent >| "$env")
    . "$env" >| /dev/null ; }

agent_load_env

# agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2=agent not running
agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
    agent_start
    ssh-add
elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
    ssh-add
fi

unset env
```

3. Copy SSH key to clipboard

```bash
cat ~/.ssh/id_ed25519.pub | clip
```

> For Legacy System

```bash
cat ~/.ssh/id_rsa.pub | clip 
```

4. Add SSH key to GitHub
    - Go to GitHub Settings.
    - Click on "New SSH key" and paste your key.


## Basic Git Commands

### Initializing a Repository

1. Create a new repository:

```bash
git init
```

2. Change branch to main

```bash
git branch -M main
```

### Clone a repository:

```bash
git clone <repository-url>
```

> Example

```bash
git clone https://github.com/anil0403/git-commands.git
```

### Making Changes

1. Check status:

```bash
git status
```

2. Add changes to the staging area:

- Stage specific file.

```bash
git add <file>
```

- Stage all the files

```bash
git add .
```

3. Commit changes:

```bash
git commit -m "Commit message"
```

### Branching

1. Create a new branch:

```bash

git branch <branch-name>
```

2. Switch to a branch:

```bash
git switch <branch-name>
```

3. Create and switch to a new branch:

```bash
git checkout -b <branch-name>
```

## Managing Remote Repository

### Adding a Remote

1. Add a remote repository:

```bash
git remote add <remote-name> <remote-url>
```

>Example

```bash
git remote add origin git@github.com:anil0403/git-commands.git
```

### Fetching and Pulling

1. Pull changes from a remote repository:

```bash
git pull <remote-name> <branch-name>
```

### Pushing Changes

1. Push changes to a remote repository:

```bash
git push -u <remote-name> <branch-name>
```

## Branch Management

1. Create a Branch:

``` bash
git branch <branch-name>
```

2. Switch to a Branch:

```bash
git switch <branch-name>
```

3. Create and Switch to a Branch in One Command:

```bash
git switch -b <new_branch-name>
```

4. List Branches:

```bash
git branch
```

5. Merge Branches:

- To merge changes from one branch into another (e.g., merging feature branch into master), use:

```bash
git checkout master
```

```bash
git merge feature_branch
```

6. Delete a Branch:

- To delete a branch (after merging or otherwise), use:

```bash
git branch -d <branch-name>

```
