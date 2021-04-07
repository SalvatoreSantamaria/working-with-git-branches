## Working with git branches 
From https://app.pluralsight.com/library/courses/working-git-branches/table-of-contents
_Note on origin: `origin` is simply the nickname for the remote url. `remote add origin https://github.com/...` creates the nickname_
_Example: `git push origin master` is the shorthand for  `git push https://github.com/elie/first_repo.git master`_

list branches: `git branch`
list all local and remote branches: `git branch -a`
list only local branches: `git branch -r` 
   _If you have color options on it’s also quite easy to tell which branches aren’t pulled down since they’re listed in red._
see the branches on a remote: git `git ls-remote`
switch to a branch: `git checkout <branch-name>`
switch to a new branch: `git checkout -b <branch-name>`
rename a branch: `git branch -m <oldName> <newName>`
delete a branch: `git branch -d <branch-nam>`
force delete a branch: `git branch -D <branch-name>`
see branch history: `git log` or `git log --oneline`

View changes that aren't pushed yet: `git diff origin/master..HEAD`

Save your changes, back to last commit `git reset HEAD^ --soft`
Discard changes, back to last commit `git reset HEAD^ --hard`

Turn your local repository into a mirror image of the remote of your choice
*Remember to replace `origin` and `master` with the remote and branch that you want to synchronize with*
* Retrieve lastest data from the original: `git fetch origin`
* throw away all my changes, forget everything on my current local branch make it same orgin/master: `git reset --hard origin/master`
* Remove unwanted files from your working directory: `git clean -f -d`

*If you need to undo a commit, use revert*

To overwrite your local files do:

git fetch --all
git reset --hard <remote>/<branch_name>
For example:

git fetch --all
git reset --hard origin/master

---
## Merge 

target = target of the merge (main in this example)
source = solution branch

To merge branches, 
* 1 switch to the target(main) branch `git checkout <target-branch>`
* 2 merge in the source(solution) branch with `git merge <source-branch>`

To compare the two branches, use `git diff <branch1> <branch2>`

---
## Rebase 

`git rebase` is used to clean up local history to focus on the end result. This should increase accuracy and clarity.
Do not use rebase on a public branch. 
You can use rebase to squash multiple commits into 1. 
Rebasing will move work from `branch` directly onto the work from main. That way it would look like these two features were developed sequentially, when in reality they were developed in parallel.

Basic rebase instructions
* 1 git checkout `feature branch`
* 2 git rebase `main`  

---

* 1 Check to see which commit to use to start a rebase: `git merge-base <source-branch(solution)> <target-branch(main)>`
* 2 Start the rebase with `git rebase -i <commit-number-here, like ca9e666...>`
* 3 Then git will open the file and show the commits you can work with
```
pick 34f86e9 Added Notes
pick ca9e66e Commit 1
pick d7f8d31 Commit 2
pick 1061789 Commit 3
```
* 4 Change `pick` to `squash` to merge multiple commit in

--- 
## Cherry Pick 

Cherry pick from other branches to import specific commits into your branch, to do things like
- getting features needed for your ticket
- branches not ready to merge yet
- _note cherry picking does create a duplicate commit_ 

* 1 Find the wanted commit with `git log --oneline` or view the log from a different branch with `git log <branch-name>  --online`
* 2 Checkout the branch where you want to make a copy of the commit with `git checkout <branch-name>`
* 3  Use the cherry-pick command to append the commit to HEAD with `git cherry-pick <commit>`

---
## Checkout PR

Use the CLI in the terminal: `gh pr checkout 1234`
_see the open with GitHub CLI submenu in the pull request_
If you use `git pull` for PR's, you are merging in the code from the PR to the local branch. When you `git push` code next, the PR pulled code will go onto your current remote branch.



## Oh My Git! notes
Go back to a previous commit with `git checkout HEAD^`
Go back two commits with `git checkout HEAD~2`

Go to the last commit with `git checkout --detach name_of_branch`

## Notes on HEAD
HEAD is the sumbolic name for the currently checked out commit. 
HEAD always points to the most recent commit which is reflected in the working tree. Most git commands which make changes to the working tree will start by changing head
Normally HEAD points to a branch name. When you commit the status of the branch is altered and this change is visible through HEAD.
_Detaching HEAD just means attaching it to a commit instad of a branch._
Use `git log` to see commit hashes

_____


## Fetch vs Pull
`git fetch` Fetch will download any information from the remote that isn't already in the local copy. Then evaluate and decide what to do
`git pull` Pull is fetch AND merge into local branch

Trying to push but need to first integrate remote changes? 
Use either pull and then complete the merge and have a merge commit OR can rebase with `git rebase origin/master`

## Undoing Commits with reset
https://www.rithmschool.com/courses/git/git-github-checkout_reset
To undo commits, you can use `git reset` command
`git reset --soft COMMIT_SHA` moves the files commited back to the staging area
`git reset --mixed COMMIT_SHA` moves the files committed back to the working directory (default if no flag)
`git reset --hard COMMIT_SHA` undoes entire commit (dangerous)

COMMIT_SHA is the unique id (aka SHA) which identifies that commit. Type `git log --oneline` to see the list of commit messages along with the first seven characters of the commit sha. This is what you should pass into each of these commands. 

Using reset will not change the commit that you switch to but any commits that have come after it. 

If you want to move the last two commits to the staging area:
`git log --oneline`
a808698     Fourth commit  
ca0bbb4     Third commit
5ffcac5     Second commit
ac49968     First commit
`git reset --soft 5ffcac5` will move the files in the Forth commit and Third commit back to the staging area.
