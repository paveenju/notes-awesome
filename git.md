# Git Hints and Techniques

## Contents

- [A First Git Workspace](#a-first-git-workspace)
- [Split a subfolder out into a new repository](#split-a-subfolder-out-into-a-new-repository)
- [Create a new local branch and push to remote repository](#create-a-new-local-branch-and-push-to-remote-repository)
- [Move files from one repository to another, preserving git history](#move-files-from-one-repository-to-another)
---

## A First Git Workspace

```console
$ git status

$ git add -A

$ git commit -m "Hello"

$ git remote add origin https://github.com/paveenju/hello-world.git

$ git remote -v

$ git branch --set-upstream-to=origin/master master

$ git push -u origin master

$ git pull

$ git pull --allow-unrelated-histories
```
## Split a subfolder out into a new repository

This is highly recommended to work on a fresh clone.

```console
$ git clone https://github.com/USERNAME/REPOSITORY-NAME

$ cd REPOSITORY-NAME

$ git filter-branch --prune-empty --subdirectory-filter FOLDER-NAME BRANCH-NAME

$ git remote set-url origin https://github.com/USERNAME/NEW-REPOSITORY-NAME.git

$ git push -u origin BRANCH-NAME
```
Visit [GitHub Docs](https://docs.github.com/en/get-started/using-git/splitting-a-subfolder-out-into-a-new-repository) for more info.

## Create a new local branch and push to remote repository

Git's branching functionality lets you create new branches of a project to test ideas, isolate new features, or experiment without impacting the main project.

```console
$ git branch NEW-BRANCH

$ git checkout NEW-BRANCH

$ git push -u origin NEW-BRANCH
```

## Move files from one repository to another, preserving git history

Moving the files with history to a different repository requires the following steps:

```console
$ git clone --branch <branch> --origin origin --progress -v <git repository A url>
$ cd <git repository A directory>

$ git remote rm origin

$ git filter-branch --prune-empty --subdirectory-filter <directory> -- --all

$ mkdir <base directory>
$ mv * <base directory>

$ git add .
$ git commit

$ git clone <git repository B url>
$ cd <git repository B directory>

$ git remote add <branch-name> <git repository A directory>

$ git pull <branch-name> master --allow-unrelated-histories

$ git remote rm <branch-name>

$ git push
```
