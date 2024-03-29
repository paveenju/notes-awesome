# Git Hints and Techniques

## Contents

- [The first Git workspace](#the-first-git-workspace)
- [Update a feature branch from master](#update-a-feature-branch-from-master)
- [Split a subfolder out into a new repository](#split-a-subfolder-out-into-a-new-repository)
- [Create a new local branch and push to its remote repository](#create-a-new-local-branch-and-push-to-its-remote-repository)
- [Move files from one repository to another while preserving git history](#move-files-from-one-repository-to-another-while-preserving-git-history)
- [Clone a git repository with a branch name](#clone-a-git-repository-with-a-branch-name)
- [Remove files or folders from a remote repository but keep them locally](#git-07)
- [Migrate a local branch to a new repository while keeping its histories](#git-08)
- [Change commit's information of specified commits](#change-commits-information-of-specified-commits)
---

## The first Git workspace

```console
git status
git add -A
git commit -m "Hello"
git remote add origin https://github.com/paveenju/hello-world.git
git remote -v
git branch --set-upstream-to=origin/master master
git push -u origin master
git pull
git pull --allow-unrelated-histories
```

## Update a feature branch from master

Merge method (Multiple developers in a branch):

Merging all files

```console
git pull
git checkout master
git pull
git checkout dev
git merge origin/master
```
Merging some files

```console
git pull
git checkout master
git pull
git checkout dev
git merge --no-ff --no-commit origin/master
git reset file1 file2 # if you do not want to merge file1 and file2
```
Rebase method (One developer one branch):

```console
git pull
git checkout master
git pull
git checkout dev
git rebase origin/master
# if there are some conflicts from old histories just cancel conflictsskip
git rebase --skip # until applying the last revision
git rebase --continue # until no rebase in progress
git pull
git add . # if there are some conflicts
git commit -m "Merged from master to dev"
git pull
git push origin
```

## Split a subfolder out into a new repository

This is highly recommended to work on a fresh clone.

```console
git clone https://github.com/USERNAME/REPOSITORY-NAME
cd REPOSITORY-NAME
git filter-branch --prune-empty --subdirectory-filter FOLDER-NAME BRANCH-NAME
git remote set-url origin https://github.com/USERNAME/NEW-REPOSITORY-NAME.git
git push -u origin BRANCH-NAME
```
Visit [GitHub Docs](https://docs.github.com/en/get-started/using-git/splitting-a-subfolder-out-into-a-new-repository) for more info.

## Create a new local branch and push to its remote repository

Git's branching functionality lets you create new branches of a project to test ideas, isolate new features, or experiment without impacting the main project.

```console
git checkout -b NEW-BRANCH
git push origin NEW-BRANCH:NEW-BRANCH
```

## Move files from one repository to another while preserving git history

Moving the files with history to a different repository requires the following steps:

```console
git clone --branch <branch> --origin origin --progress -v <git repository A url>
cd <git repository A directory>

git remote rm origin
git filter-branch --prune-empty --subdirectory-filter <directory> -- --all

mkdir <base directory>
mv * <base directory>

git add .
git commit

git clone <git repository B url>
cd <git repository B directory>

git remote add <branch-name> <git repository A directory>
git pull <branch-name> master --allow-unrelated-histories
git remote rm <branch-name>
git push
```

## Clone a git repository with a branch name

```console
git clone -b my-branch git@github.com:user/myproject.git
```

## <a name="git-06"></a> Fetch all branches from a remote repository

```console
git fetch origin
git branch -a
```

## <a name="git-07"></a> Remove files or folders in a remote repository but keep them locally

Step 1 - Remove files or folders remotely:

```console
git rm --cached Files
git rm -r --cached Folders
git commit -m "Removed files/folders from repository"
git push origin master
```
Step 2 - Make sure to modify .gitignore with the following examples:

```console
foldername/
filename
```

## <a name="git-08"></a> Migrate a local branch to a new repository while keeping histories

Assume that we would like to copy the local branch named `dev` to a new repository as the `master` branch and prepare you local directory for the new repository. 

```console
git fetch origin
git checkout -b dev origin/dev
git remote add new-origin <new-repo-url>
git push new-origin dev:master
git remote rm origin
git remote rename new-origin origin
git checkout -b master origin/master
git branch -D <local-branches-in-old-repo>
```

## Change commit's information of specified commits

Given that the commit history is `A-B-C-D-E-F` with `F` as `HEAD`, we follows these steps to change the author of `C` and `D`.

1. Specify `git rebase -i B` (if you need to edit `A`, use `git rebase -i --root`)
2. Change the lines for both `C` and `D` from `pick` to `edit`
3. Exit the editor (for `vim`, this would be pressing `Esc` and then typing `:wq`).
4. Once the rebase started, it would first pause at `C`
5. You would `git commit --amend --author="Author Name <email@address.com>"`
6. Then `git rebase --continue`
7. It would pause again at `D`
8. Then you would `git commit --amend --author="Author Name <email@address.com>"` again
9. `git rebase --continue`
10. The rebase would complete.
