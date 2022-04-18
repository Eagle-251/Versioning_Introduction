# Git Cheatsheet

## Introduction

Git is a implementation of a code versioning platform (or version control). This is a way of tracking the changes made to, and recording the history of, files. Usually these files are source code files of a program or similar. Git is the most popular implementation of this. Not to be confused with Github or Gitlab as, although they use Git, they are server side programs host remote git repositories.

Git records every change made to files in version control using commits.
These are snapshots in time of the current state of a repository and each commit contains a unique reference that can be used later on to checkout the files as they were at that point in version history. This is contrasted to other forms of version control like delta-based versioning which records changes to files individually rather then a snapshot of the entire repository.

Snapshot based versioning is powerful for many reasons but not least because it allows users to have a local version of the entire history of the repository. This attribute is gives git the ability to be _distributed_ in that there is no one point of failure between a group of developers and central remote git server.

---

## Installation

### Linux

Git comes standard with most modern linux distributions.

If not installed already, most if not all package managers should have it available:

| Distro        |                           |
| ------------- | ------------------------- |
| Debian/Ubuntu | `sudo apt install git`    |
| Fedora        | `sudo dnf -y install git` |
| Arch          | `sudo pacman -S git`      |

### Mac OSx

Git is not installed by default on Mac OS.

There are multiple ways to install it on Mac, the simplest being to install the `.dmg` package.
This can be found at [Git SCM](https://git-scm.com/) project page.

Alternatively you can use [Homebrew](https://brew.sh/). This is a package manager for Mac OS. This is recommend if you plan to develop on Mac.

You can read [the docs](https://brew.sh/) if you wish to install this, then run: <br> `brew install git`

### Windows

To install on windows download the appropriate installer from [Git SCM](https://git-scm.com/download/win).

---

## Configuration

Out of the box Git should be set up to run very simple commands like `git clone` if you are cloning a public repository.
However before you start editing files it is important to make sure that your identity will be written to the commits so that other developers will know who made the changes. This is done through changing git configuration.

The base command for doing this is `git config`
This command alone will return a short help.

To get variable run `git config <config_variable>`
For exam
ple:

> `git config user.email`

To set a configuration variable append the desired variable to the command:

> `git config user.email user@example.com`

There are two main scopes that a configuration can apply in:

- **Global Scope**

  - This will apply to _all_ repositories on the users system account
  - To get/set a global variable add the `--global` before the path to the variable <br>
    To get:

    > `git config --global user.email`<br>

    To set:<br>

    > `git config --global user.email user@example`

- **Local Scope**

  - Local scope applies only the repository in which the command is being
  - This is the default behavior of the git config command; running `git config` without the `--global` flag will run in the local scope.<br>
    To get:

    > `git config --global user.email`<br>

    To set:<br>

    > `git config --global user.email user@example`

---

## Basic Operations

<br>

| Description                                                                           | Command                                       |
| ------------------------------------------------------------------------------------- | --------------------------------------------- |
| **Create a new Git repo in the current directory**                                    | `git init`                                    |
| **Adding changed files to source control**                                            | `git add <file>`                              |
| **Adding All Changed files to source control**                                        | `git add .`                                   |
| **Record change to staged files in repo history**                                     | `git commit -m "Short description of changes` |
| **Show summary of recent changes to the repository**                                  | `git log`                                     |
| **Show changes to files with or without a reference point**                           | `git diff`                                    |
| **Create a new branch (separate commit history)**                                     | `git branch <branch name>`                    |
| **Merge the history of two separate branches together**                               | `git merge <branch name>`                     |
| **Pull the latest changes from remote repo and merge them into the local repository** | `git pull`                                    |
| **Push latest local changes to the remote repository**                                | `git push`                                    |

## Typical Daily Workflow

This workflow is based on a [Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow). This is a workflow that maintains a protected main/master branch and a separate branch for each "feature". This workflow also heavily utilises pull requests to merge code from branches back into the main branch. This gives a very convenient point to discuss and/or fix code before push to the main branch. This aspect works best in partnership when used with issues where the branches, and later pull requests, stem from a single issue.
Furthermore this workflow is particularly useful when utilising CI/CD pipelines. For example the protected nature of the main branch (along with reviews happening before any writing to the main branch) means that (ideally) the main branch should only contain "non-broken" code. Creating a CD pipeline where a release gets published on each is good use of this workflow.  
<br>
For example:

![Example Workflow](https://victoria.dev/blog/git-branching-for-small-teams/cover.png)
