# GIT

This document gives an overall picture of `Git`, assuming no previous background.

### Document contents:
[Basics of Git](#30-git-basics)

[Step 1: Working in the local repository](#1-working-in-the-local-repository)
- Commands treated: `git init`, `git status`, `git diff`, `git add`, `git commit`, `git log`

[Step 2: Working with remote repositories](#2-working-with-remote-repositories)
- Commands treated: `git clone`, `git remote add`, `git fetch`, `git merge`, `git push`

[Step 3: Working with branches](#3-working-with-branches)
- Commands treated: `git clone`, `git remote add`, `git fetch`, `git merge`, `git push`

## 0 Git basics
### 0.1 Why is `Git` useful?
`Git` makes it easy to handle code written by a team. First, by enabling multiple people to work in different parts of the code without interfering with one another thanks to what we call 'branches'. Secondly, it by allowing recoverability; `Git` keeps track of the changes made to the code at any state, and makes it easy to recover any step the code has been in.

The usefulness of `Git` has brought complimentary tools such as `GitHub`, which added many additional features allowing open-sourcing, Continuous Integration and Delivery, and much more.

### 0.2 Basic concepts
####  The `.git` folder: where data is stored
Instead of keeping a snapshot of the latest state of the files, `Git` stores documents as an overlay of changes, in a tree structure inside the `.git` folder. The `.git` folder is a hidden folder saved in the path we have told `Git` to initialize (either with `git init` or `git clone`; see sections 1 and 2).

- Example, from an original file of 2000 lines of code, if we remove 10 lines of code and add 50, instead of replacing the 2000 lines of code file with another with 2040 lines, `Git` will keep the original file and place on top of it a new file mentioning the changes in the code (the 10 lines removed and the 50 added). That way, any code that was saved in the `.git` folder is retrievable.

Note: it is important to distinguish our working files with our local files inside the `.git` folder. Our 'local' files are those saved in the working folder, the ones we open with the text editor and modify. `Git` will save (when we `commit`) and retrieve (for example, when we change branches) versions of these files in the `.git` folder when we tell it so. These versions or 'snapshots' of our code is what `Git` handles.

#### Committing
Committing is the way we tell `Git` to save the current state of our code in the local `.git` folder. Once our local code is up to date with the `.git` folder, we can run the `git commit` command to save the changes (see paragraph 1 below).

#### Branches
A branch is an independent version of the code; multiple branches can be active at the same time. Each person usually works in a single 'branch' (usually adding a new, isolated feature for the code), the changes that person makes to the branch will not affect other parts of the code. Once the branch is finished, changes on the branch can be easily compared to the current version of the code, making the code easy to review.

Note: Each branch is created for developers to work in a single feature without affecting the `master` branch (the 'current working version' of the code); once a branch is tested , it is 'merged' back (usually) to the `master` branch. 
- Example of when to use a branch: On monday, a developer of a Pet shop website is asked to add a new service to the website of displaying a photo of the available pets. For that, he creates a new branch called `pets-photos` (which at the beginning is a copy of the `master` branch), and starts working on it; he estimates he will do the job in three days. Creating a new branch allows him to start working on new code without losing the 'working version': '`master`'. On tuesday afternoon, he receives a call from his boss saying the website is down due to a bug on the code! `Git` allows him to save the current work on the `pets-photos` branch, and then create a new `urgent-fix` branch (which is again a copy of `master`) to fix the bug quickly. Once he is done fixing the bug, he merges the code of `urgent-fix` back to `master`, which enables the webpage to work again (`master` is now updated with the changes of `urgent-fix`). Now, the developer can take back where he left the `pets-photos` branch, and continue the feature he was previously working on. 


## 1. Working in the Local Repository
### 1.0 Initializing
```git init```
- creates an empty Git repository (`'.git'`) that gathers all committed files from the working document (see paragraph 0.2).

#### Basic files
Apart from our codebase, it is a good idea to initialize each project with two additional files:
- `README.md` file: uses the [Markdown language](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf) to render a description of the Project in GitHub.
- `.gitignore` file: a list of the files we do not want to upload to Github.

#### Note on `gitignore` file
The `.gitignore` file contains all files and terminations that should be ignored by `Git` (those files you might have or want in your local repository but you do not need in your code, such as `VS Code` files '`.vscode'`.)
The file contains a list of all terminations, folders, files to be ignored. The format is explained below:
- use `*.<extension>` to ignore all files ended up in the `<extension>` specified
- use `<folder>/` to ignore all files inside a folder
- use `<folder>/<filename>` to ignore a specific file

Example of `.gitignore` file: https://gist.github.com/octocat/9257657

### 1.1 Adding, Removing and Modifying files in the Staging Area
Conceptually, the Staging Area is what `Git` calls the list of 'files to be added later to my code'. 
The Staging Area allows us to keep track of the current changes of our code in real time. When a file added to the staging area, `Git` will save a snapshot of that file; `Git` will then be able to know if we have made changes on that file.

Once it is on the staging area, the file will be ready to be Committed (Saved on the `Git` tree, see point 1.2).

#### Checking status
```git status```
- compares the current state of the local files with the files on the staging area and outputs the differences. It will also let you know the branch you are currently working on, and the files already added to the Staging area.

```git diff```
- Tells you the files you've changed locally but not yet staged

#### Adding files to Staging area
```git add <file>```
- adds snapshot of `file` to the staging area (Snapshot of file is taken, and will be added to the Git repository next time we run `commit`) (Note that if you modify `<file>` again before committing, only the version added to the Staging area will be considered. To update the modified version, run the add command again with the same file)

```git add -A```
- adds all files of the current folder in the Staging area
    
#### Removing files from Staging area
```git rm <file>```
- Remove: Tells `Git` to not keep track of changes in `<file>` anymore (removes it from the `Git` tree)

#### Modifying file names
```git mv <previous_file_name> <new_file_name>```
- Updates the name of the file from v1 to v2 (so `Git` can keep track of the changes since the beginning). 
Note: if you remove the file (`git rm <previous_file_name>`) then add it again with another name(`git add <new_file_name>`), `Git` will still figure out the file is being renamed, but the `mv` command is the explicit way of doing so (preferred way).

### 1.2 Comitting files from Staging area to Local Repository
Once the local changes have been sent to Staging area (git has taken a 'snapshot' of the files), these snapshots are ready to be saved in the local git repository. Once in the local repository, any saved state will be retrievable at any time.

#### Adding files to the Local Repository
```git commit -m '<commit description>'```
- Copies all "snapshots" of the files added in the staging area, and saves a copy in to the local Git repository.

Note: In the background, what `Git` does on each `commit` statement is saving the changes done to the files at each step in an optimized format. The files do not get copied over and over, what is saved are only the lines of code that were deleted, and the new lines added from the previous version. That way, files can be 're-built' following any of the steps of each `commit` statement, from the initial state. Each `commit` statement receives a hash code, which will allow us to identify it, and retrieve it anytime we wish so.
- `-m` lets you add a comment to the commit (Important, so you can keep track of what you did in that commit). Note that `Git` will force you to add the message if it is not included.

#### Retrieving commit history
```git log```
- Outputs the history of commit statement done in the local repository. This command is very useful to understand where we are in the `Git` tree history; it can be used to retrieve the `commit` code and understand the branch tree.
Useful options: 
- `git log --pretty=oneline` displays all the information in one line
- `git log --pretty=format:" %s" --graph` displays the info demanded ("%h" prints the commit hash, "%s" prints the subject) in a visual way showing the branch and merge history.

## 2. Working with Remote Repositories
### 2.0 Configuring


### 2.1 Cloning remote repositories
```git clone [URL]```
- Creates a new folder in current directory, and copies all information of the specified URL
- `git clone [URL] name`: adding 'name' creates a folder with named 'name', and clones the content of the URL

### 2.2 Adding/checking remote repositories
```git remote```
- tells you the names of the remote repositories you have configured
..* adding -v (verbose) will tell you the URL. Note: `origin` is the default name of the repository you cloned your local file from.

```git remote show [remote repository name]```
- gives you info about the remote repository specified

```git remote add [shortname] [URL]```
- adds a new remote repository in the URL specified, with the shortname typed (shortname can be changed) 
example: `git remote add origin https://github....`

```git remote rename [oldname] [newname]```
- changes the name of the remote file from old to new name


### 2.3 Pulling data from remote repositories
```git fetch [remote repository name] [branchname]```
- updates the 'origin/master' local Git folder from the data of the 'master' remote repository (Github). Only the .git file is changed, not the working directory. 
ex: `git fetch origin master`
		
```git merge [repository name] [branchname]```
- takes the data from the 'origin/master' local .git folder to the 'master' local working folder (merging might bring discrepancies - i.e. a line modified in the .git folder & locally, they must be resolved before being able to end the merge command) 
ex: `git merge origin master`
		
```git pull [repository name] [branchname]```
- the pull command is equivalent of (fetch & merge)
ex: `git pull origin maser`

### 2.4 Pushing data upstream
```git push [remote repository name] [branchname]```
- "pushes" or updates the local data to the virtual repository. (will only work if you have access and if nobody has pushed since the last time you pulled code. If the code has been updated, you'll need to pull the code, change it, and then push it.)
- Adding `-u` creates a bond between 'origin/master' (local Git repository) and the virtual 'master' on Github. `-u` needs to be called one time only to do the bonding.

#### Force-pushing (Use very carefully)
In the cases we are sure

### 2.5 Tagging
```git tag -a [tag] -m [tag message]```
- sets up an annotated tag that will be associated with a specific commit
ex: `git tag -a v1.1 -m 'This is the 1.1 version'`

## 3. Working with Branches
Branching allows you to work in multiple tasks at the same time. For example: you are building some feature for an app. You create a branch "feature 1", and start working on it; the main "production" branch (Master) is unchanged. Then, you need to start working on another urgent feature. You create a branch from the master and start working on it.
Useful link: https://git-scm.com/book/en/v1/Git-Branching-Basic-Branching-and-Merging
	
```git branch [newbranch]```
- creates a new branch named 'newbranch' from the last commit of the current branch you are in (if you are not in Master and want to make a branch FROM master, switch back to Master and THEN create the new branch)

```git checkout [namebranch]```
- changes the pointer of the HEAD object, and all commits done from now on will go on the branch specified (note that if you have uncommitted changes that clash with the branch you are switching to, Git will not allow you to do the switch)

```git checkout -b [newbranch]```
- adding -b to the checkout command creates a new branch from the current branch AND changes the pointer to work on it

```git merge [branchname]```
- merges the specified branch with the branch you are currently in (ex: to merge with master you need to checkout to master then merge)

```git branch -d [branchname]```
- after the branch is merged, the branch pointer can be erased as it is useless

### Rebasing: 
`rebase` updates the position of your branch after new changes of master (while at branch different from master)

```git rebase master```
- after pulling to master last remote master changes) takes the `HEADER` and puts it into the latest version of master, which updates the position of the branch to the latest of master, this will tell you if there are merge conflicts. After this, a PR can be issued.

(To be added: `git stash`, `git pop`)