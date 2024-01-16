# Git Installation and GitHub SSH Connection Guide

This guide provides detailed instructions on installing Git and setting up a secure SSH connection with GitHub. Additionally, it covers essential Git commands for managing both local and remote repositories.

## Table of Contents

1. [Git Installation](#git-installation)
2. [Git Bash Configuration](#git-bash-configuration)
3. [GitHub SSH Connection](#github-ssh-connection)
4. [Basic Git Commands](#basic-git-commands)
5. [Managing Remote Repository](#managing-remote-repository)

## Git Installation


1. Install Git via Homebrew:

```bash
brew install git
```

2. Alternatively, download the macOS installer from [git-scm.com](https://git-scm.com/download/mac) and follow the instructions.



## GitHub SSH Connection

1. Generate SSH Key

-Paste the text below, replacing the email used in the example with your GitHub email address.

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

> Note: If you are using a legacy system that doesn't support the Ed25519 algorithm, use:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

2. Adding your SSH key to the ssh-agent

>Start the ssh-agent in the background.

```bash
eval "$(ssh-agent -s)"
```

> Add your SSH private key to the ssh-agent and store your passphrase in the keychain. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_ed25519 in the command with the name of your private key file.

```bash
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

>Note: The --apple-use-keychain option stores the passphrase in your keychain for you when you add an SSH key to the ssh-agent. If you chose not to add a passphrase to your key, run the command without the --apple-use-keychain option.

> The --apple-use-keychain option is in Apple's standard version of ssh-add. In macOS versions prior to Monterey (12.0), the --apple-use-keychain and --apple-load-keychain flags used the syntax -K and -A, respectively.

> If you don't have Apple's standard version of ssh-add installed, you may receive an error. For more information, see "Error: ssh-add: illegal option -- apple-use-keychain."

> If you continue to be prompted for your passphrase, you may need to add the command to your ~/.zshrc file (or your ~/.bashrc file for bash).

3. Copy SSH key to clipboard

```bash
pbcopy < ~/.ssh/id_ed25519.pub 
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

### Pulling

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
