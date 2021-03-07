## Working with git branches 
From https://app.pluralsight.com/library/courses/working-git-branches/table-of-contents

list branches: `git branch`
switch to a branch: `git checkout <branch-name>`
switch to a new branch: `git checkout -b <branch-name>`
rename a branch: `git branch -m <oldName> <newName>`
delete a branch: `git branch -d <branch-nam>`
force delete a branch: `git branch -D <branch-name>`
see branch history: `git log` or `git log --oneline`

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

* 1 Check to see which commit to use to start a rebase: `git merge-base <source-branch> <target-branch>`
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
