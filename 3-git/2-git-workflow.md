# GIT WORKFLOW

This document summarizes the 'typical' workflow of commands used while working with `Git`. This document assumes the use of GitHub.

### Step 1: Initialize the project (`git init` or `git clone`)
- **Step 1.1:** Open a new Repository in GitHub, give it a name

- **Step 1.2 (possibility A):** Use `git init` to start the project from scratch. In that case, it is recommended to create a `README.md` file and `.gitignore` files. GitHub enables the creation of a defaule `README.md` file for the project, although it is always better to create your own.

- **Step 1.2 (possibility B):** use `git clone [URL]` to copy an existent project in your local machine. You can either do so to modify the repository you cloned from (the one with the same `[URL]`), in that case it is recommended to use `git clone -u [URL]` (`-u` will add the remote repository as a shortcut for 'origin')



[Git workflow]

## 0 Git basics
### 0.1 Why is `Git` useful?
`Git` makes it easy to handle code written by a team. First, by enabling multiple people to work in different parts of the code without interfering with one another thanks to branches. Secondly, by allowing recoverability; `Git` keeps track of the changes made to the code at any state, and makes it easy to recover any step the code has been in.

The usefulness of `Git` has brought complimentary tools such as `GitHub`, which added many additional features allowing open-sourcing, Continuous Integration and Delivery, and much more.

### 0.2 Basic concepts
####  The `.git` folder: where data is stored
Instead of keeping a snapshot of the latest state of the files, `Git` stores documents as an overlay of changes, in a tree structure inside the `.git/` folder (local repository). The `.git/` folder is a hidden folder saved in the path we have told `Git` to initialize the project (either with `git init` or `git clone`; see sections 1 and 2).

- Example: From an original file of 2000 lines of code, if we remove 10 lines of code and add 50, instead of replacing the 2000 lines of code file with another file with 2040 lines, `Git` will keep the original file and place on top of it a new file mentioning the changes in the code (the 10 lines removed and the 50 added). That way, any step that was saved in the `.git/` folder is retrievable.

Note: it is important to distinguish our working files with our local files inside the `.git/` folder. Our 'local' files are those saved in the working folder, the ones we open with the text editor and modify. `Git` will save (when we `commit`)  snapshots of these local files in the `.git/` folder when we tell it so. `Git` will also retrieve the saved files in the `.git/` folder (for example, when we change to another branch), and update our local files accordingly.

#### Committing
Committing is the way we tell `Git` to save the current state of our code in the local `.git/` folder. Once our local code is up to date with the `.git/` folder, we can run the `git commit` command to save the changes (see paragraph 1 below).

#### Workspace, Staging Area, Local Repository, Remote Repository
It is important to understand the four 'stages', or 'areas' our code can be in:
- The 'workspace' is simply the area where our local files are placed (usually the current version of our code); these are the files we can open with the text editor and modify to update the code.
- The 'staging area' is the list of files 'to be saved to the local `.git/` repository' when we say so. `Git` keeps that list to make sure we keep track of our changes before we `commit` (or save) our changes in the local `.git/` repository (see paragraph 1.2).
- The 'local repository' is a hidden folder named `.git/`, where `Git` will save all the versions of the files we committed in an optimized format.
- The 'remote repository' is simply an online copy of our project (usually saved on GitHub or GitLab). Having a remote copy of the project enables many features, such as granting access to the latest verion of our code to our team members (see Paragraph 2).

#### Branches
A branch is an independent version of the code; multiple branches can be active at the same time. Each person usually works in a single 'branch' (usually adding a new, isolated feature for the code), the changes that person makes to the branch will not affect other parts of the code. Once the branch is finished, changes on the branch can be easily compared to the current version of the code, making the code easy to review.

Note: Each branch is created for developers to work in a single feature without affecting the `master` branch (the 'current working version' of the code); once a branch is tested , it is 'merged' back (usually) to the `master` branch. 
- Example of when to use a branch: On monday, a developer of a Pet shop website is asked to add a new service to the website of displaying a photo of the available pets. For that, he creates a new branch called `pets-photos` (which at the beginning is a copy of the `master` branch), and starts working on it; he estimates he will do the job in three days. Creating a new branch allows him to start working on new code without losing the 'working version': '`master`'. On tuesday afternoon, he receives a call from his boss saying the website is down due to a bug on the code! `Git` allows him to save the current work on the `pets-photos` branch, and then create a new `urgent-fix` branch (which is again a copy of `master`) to fix the bug quickly. Once he is done fixing the bug, he merges the code of `urgent-fix` back to `master`, which enables the webpage to work again (`master` is now updated with the changes of `urgent-fix`). Now, the developer can take back where he left the `pets-photos` branch, and continue the feature he was previously working on. 


## 1. Working in the Local Repository
### 1.0 Initializing
```git init```
- creates an empty Git repository (`.git/`) that gathers all committed files from the working document (see paragraph 0.2).

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
The Staging Area allows us to keep track of the current changes of our code in real time. When a file added to the staging area, `Git` will take a snapshot of that file; `Git` will then be able to know if we have made changes on that file.

Once it is on the staging area, the file will be ready to be Committed (Saved on the `Git` tree, see point 1.2).

#### Checking status
```git status```
- compares the current state of the local files with the files on the staging area and outputs the differences. It will also let you know the branch you are currently working on, and the files already added to the Staging area.

```git diff```
- Tells you the files you've changed locally but not yet staged

#### Adding files to Staging area
```git add [file]```
- adds snapshot of `[file]` to the staging area (Snapshot of file is taken, and will be added to the Git repository next time we run `commit`) (Note that if you modify `[file]` again before committing, only the version added to the Staging area will be considered. To update the modified version, run the add command again with the same file)

```git add -A```
- adds all modified files of the current folder in the Staging area

#### Removing files from Staging area
```git rm [file]```
- Remove: Tells `Git` to not keep track of changes in `[file]` anymore (removes it from the `Git` tree)

#### Modifying file names
```git mv [previous_file_name] [new_file_name]```
- Updates the name of the file from `[previous_file_name]` to `[new_file_name]` (this command explicitely tells `Git` that the new file had a different name in the past, and if we decide to retrieve a past version of the new file, it should look for the previous name). 
Note: if you delete (using the `rm` command) the file (`git rm [previous_file_name]`) then add it again with another name(`git add [new_file_name]`), `Git` will still figure out the file is being renamed, but the `mv` command is the explicit way of doing so (preferred way).

### 1.2 Comitting files from Staging area to Local Repository
Once the local changes have been sent to Staging area (git has taken a 'snapshot' of the files), these snapshots are ready to be saved in the local git repository. Once in the local repository, any saved state will be retrievable at any time.

#### Adding files to the Local Repository
```git commit -m '<commit description>'```
- Takes a "snapshot" of all files listed in the staging area, and saves a copy in to the local `.git/` repository.

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
Before working with any remote repository (in GitHub, for example), it is important to set up correctly the username and email of our account. GitHub will use this data to autheticate us every time we try to push changes to remote repositories.

```git config --global user.name [my-username]```
- Sets up the username to 'my-username'

```git config --global user.email [my.email@example.com]```
- Sets up the email

### 2.1 Cloning remote repositories
Cloning makes a copy of a remote repository in a local file, and allows us to start working immediately. (It is similar to `git init`, but the contents are copied from a remote repository instead of being empty).
```git clone [URL]```
- Creates a new folder in current directory, and makes a local copy of the contents of the repository of the specified URL
- `git clone [URL] [folder_name]`: adding `[folder_name]` creates a new folder (named `[folder_name]`), and clones the content of the URL

### 2.2 Adding/checking remote repositories
```git remote```
- lists the names of the remote repositories you have configured
- adding `-v` (verbose) will print the URLs of each remote repository.
Note: `origin` is the default name for the 'base' project (the repository you cloned the project from).

```git remote show [remote repository name]```
- gives you info about the remote repository

```git remote add [shortname] [URL]```
- adds a new remote repository in the URL specified, with the shortname typed (shortname can be changed) 
Example: `git remote add origin https://github....`

```git remote rename [oldname] [newname]```
- changes the name of the remote file from old to new name


### 2.3 Pulling data from remote repositories
```git fetch [remote repository name] [branchname]```
- updates the local `.git/` folder from the data of a branch in the remote repository (Github). Only the `.git/` file is changed, not the local working files. 
Example: `git fetch origin master`
		
```git merge [repository name] [branchname]```
- takes the data from a branch in the local `.git/` folder and merges it into our local files in the workspace (merging might bring discrepancies - i.e. a line modified in the `.git/` folder & locally, they must be resolved before being able to end the merge command, see Paragraph 3).
Example: `git merge origin master`
		
```git pull [repository name] [branchname]```
- the pull command is equivalent of fetch & merge. The changes on the remote repository are saved in the local `.git/` repository and merget onto our workspace.
Example: `git pull origin maser`

### 2.4 Pushing data upstream
```git push [remote repository name] [branchname]```
- "pushes" or updates the local data to the remote repository. This command will only work if we have access to the repository, and if there are no merge conflicts in the code.
- Note: Adding `-u` (`git push -u ...`) in the statement creates a bond between 'origin/master' (local Git repository) and the virtual 'master' on Github. `-u` needs to be called one time only to do the bonding.

#### Force-pushing (Use very carefully)
In the cases we are absolutely sure that we want to ignore the changes in the remote repository to push code from our local files, we can use the `-f` command added to the push statement. (`git push -f ...`). This will automatically update the remote repository with the changes on the local one, removing any conflicting parts in favor of the local data.

### 2.5 Tagging
```git tag -a [tag] -m [tag message]```
- sets up an annotated tag that will be associated with a specific commit
Example: `git tag -a v1.1 -m 'This is the 1.1 version'`

## 3. Working with Branches
### 3.1 Creating and switching branches
Branching allows us to work in multiple tasks at the same time (see Paragraph 0).
This is a useful [link](https://git-scm.com/book/en/v1/Git-Branching-Basic-Branching-and-Merging) explaining branching.
	
```git branch [newbranch]```
- creates a new branch named 'newbranch' from the last commit of the current branch we are in. If we are not in `master` and want to make a branch FROM it, we must switch back to `master` (command: `git checkout master`) before running the above command and THEN create the new branch.

```git checkout [namebranch]```
- Switches to the branch spacified. The way Git handles it is by changing the pointer of the HEAD object, which will make all commits done from now on will go on the branch specified (note that if we have uncommitted changes that clash with the branch we are switching to, Git will not allow us to do the switch; to sort that see the `git stash` command).

```git checkout -b [newbranch]```
- adding `-b` to the checkout command creates a new branch from the current branch AND changes the pointer to work on it

### 3.2 Merging branches
#### Successful merges
```git merge [branchname]```
- merges the specified branch with the branch you are currently in.

```git branch -d [branchname]```
- This command deletes the branch (`-d`). This should be ran after branches are mergerd.

#### Sorting out merge conflicts
Merge conflicts occur when we merge code to a branch that has been changed since the last time we pulled code from it (for example, we create a `new-branch` from `master`, and someone modified `master` before we merged back the `new-branch` changes-). Not all changes generate merge conflicts, only the ones affecting the same lines of code we modified in our branch. Note that **merging will be blocked until we resolve the merge conflict**.

There are many ways to sort out Merge conflicts, the easiest is using opening our text editor and manually selecting the lines of code we want to keep. A merge conflict looks like this:

``` Python
# This code is unaffected by the merge conflict

<<<<<< HEAD
# These lines were modified since
# the last time we pulled from the branch

=======
# These lines are the ones we modified
# that are conflicting with the lines above

>>>>>> new-branch
```
- To sort out the merge conflict, we must select the lines that we wish to keep (we can select parts of each side), and delete the `<<<<<< HEAD`, `=======` and `>>>>>> new-branch` operators.

Additional [resource](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-using-the-command-line) on sorting out Merge conflicts.

### 3.3 Sorting out merge conflicts on the local machine
It is good practice to sort out merge conflicts on our local repository before pushing them on GitHub (although GitHub allows also to easily do so when a Pull Request is launched).

There are two ways of ensuring our code does not contain merge conflicts:
- Pulling the last changes from the 
`rebase` updates the position of your branch after new changes of master (while at branch different from master)

```git rebase master```
- after pulling to master last remote master changes) takes the `HEAD` and puts it into the latest version of master, which updates the position of the branch to the latest of master, this will tell you if there are merge conflicts. After this, a PR can be issued.

(To be added: `git stash`, `git pop`)