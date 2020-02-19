# Git basics

## 0.1 - Why is `Git` useful?
`Git` makes it easy to handle code written by a team. It enables:
- multiple people to work in different parts of the code without interfering with one another thanks to [branches](#branches),
- code recoverability: `Git` keeps track of the changes made to the code at any state, and makes it easy to recover any step the code has been in,
- visualization of the added and removed lines in the code at each step, which is very useful to follow-up projects (usually).

The usefulness of `Git` has brought complimentary tools such as `GitHub`, which added many additional features allowing open-sourcing, Continuous Integration and Delivery, and much more.

## 0.2 - Basic concepts
###  The `.git/` folder: where data is stored
Instead of keeping a snapshot of the latest state of the files (as a regular computer does with files), `Git` stores documents as an overlay of changes, in a tree structure inside the `.git/` folder (local repository). The `.git/` folder is a hidden folder saved in the path we have told `Git` to initialize the project (either with `git init` or `git clone`; see sections 1 and 2).

- *Simplified idea on how files are stored: From an original file of 2000 lines of code, if we remove 10 lines of code and add 50 and then save the file (or 'commit' it in `Git` jargon), instead of replacing the 2000 lines of code file with another file with 2040 lines, `Git` will keep the original file and place on top of it a new file mentioning the changes in the code (the 10 lines removed and the 50 added). That way, any step that was saved in the `.git/` folder is retrievable.*

> Note: it is important to distinguish our working files with our local files inside the `.git/` folder. Our 'local' files are those saved in the working folder, the ones we open with the text editor and modify. `Git` will save (when we `commit`)  snapshots of these local files in the `.git/` folder when we tell it so. `Git` will also retrieve the saved files in the `.git/` folder (for example, when we change to another branch), and update our local files accordingly.

### Committing
Committing is the way we tell `Git` to save the current state of our code in the local `.git/` folder. Each time we feel we are at a step that we might want to retrieve later, or save our progress (once a piece of our code starts working as we expected, for example), we can run the `git commit` command to save the changes.

### Workspace, Staging Area, Local Repository, Remote Repository
It is important to understand the four 'stages', or 'areas' our code can be in:
- The **workspace** is simply the area where our local files are placed (usually the current version of our code); these are the files we can open with the text editor and modify to update the code.
- The **staging area** is the list of files 'to be saved to the local `.git/` repository' when we decide to. (The list gets updated every time we run the `git add` command; we can check the current status of the list by running `git status`). `Git` keeps that list to make sure we keep track of our changes before we `commit` our changes in the local `.git/` repository (see paragraph 1.2 of the [Git cheatsheet](1-complete-cheatsheet.md)).
- The **local repository** is a hidden folder named `.git/`, where `Git` will save all the versions of the files we committed in an optimized format.
- The **remote repository** is simply an online copy of our project (usually saved on GitHub or GitLab). Having a remote copy of the project enables many features, such as granting access to the latest version of our code to our team members (see Paragraph 2 of the [Git cheatsheet](1-complete-cheatsheet.md)).

### Branches
A branch is an independent version of the code; multiple branches can be active at the same time. Each person usually works in a single 'branch' (usually adding a new, isolated feature for the code); the changes that person makes to the branch will not affect other parts of the code. Once the branch is finished, changes on the branch can be easily compared to the current version of the code, making the code easy to review.

> Note: Each branch is created for developers to work in a single feature without affecting the 'base' branch (usually `master`, the 'current working version' of the code); once a branch is tested , it is 'merged' back to the base branch. 
- Example of when to use a branch: On monday, a developer of a Pet shop website is asked to add a new service to the website of displaying a photo of the available pets. For that, he creates a new branch called `pets-photos` (which at the beginning is a copy of the `master` branch), and starts working on it; he estimates he will do the job in three days. Creating a new branch allows him to start working on new code without losing the 'working version': '`master`'. On tuesday afternoon, he receives a call from the Pet shop owner saying the website is down due to a bug on the working code. `Git` allows him to save the current work on the `pets-photos` branch, and then create a new `urgent-fix` branch (which is again a copy of `master`) to fix the bug quickly. Once he is done fixing the bug, he merges the code of `urgent-fix` back to `master`, which enables the webpage to work again (`master` is now updated with the changes of `urgent-fix`). Now, the developer can take back where he left the `pets-photos` branch, and continue the feature he was previously working on. 

### Pull requests
A pull request is the way we should 'merge' branches into our working code. Once our active branch (the one we are working on) functions as we expect and is ready to be added to the code, we add it to the code through a pull request, which will send a notification to the other team members that you want to add your code to the '`master`' branch (the 'working version' of the code), and let them see what lines will be deleted and added to the code once the Pull Request is approved. The Pull Request allows the other team members to review your work; a PR needs to be reviewed and approved by at least one member of the team before confirming the merge.

> Note: once a Pull Request is launched, a notification in GitHub is launched while the `master` branch is unchanged. All members will be able to check the changes that PR would bring to the code if approved, and gives the option to Approve, Reject or add comments to the code. Once it is approved, the code changes get added to the master branch.

The working flow of Git is as follows (Assuming we already have a working version of our code called `master`):
- We want to add a new feature to our code, we create a branch in our local repository (which is a copy of `master` at the beginning)
- We start modifying the code in the new branch, and test it accordingly until it behaves as we expect
- Once we are happy with it, we commit the branch and push it to GitHub (GitHub will have now a `master` branch and the branch you just pushed).
- Once the branch is on GitHub, we can launch a Pull Request to let the other team members know we want to add that code to the `master` branch
- Other team members review the code, accept it (or propose changes until they accept it)
- Once another team member (who is not the one who coded the branch) accepts the Pull Request, the changes get added to the working code