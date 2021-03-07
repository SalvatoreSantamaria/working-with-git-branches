From https://app.pluralsight.com/library/courses/working-git-branches/table-of-contents

list branches: `git branch`
switch to a branch: `git checkout <branch-name>`
switch to a new branch: `git checkout -b <branch-name>`
rename a branch: `git branch -m <oldName> <newName>`
delete a branch: `git branch -d <branch-nam>`
force delete a branch: `git branch -D <branch-name>`
see branch history: `git log` or `git log --oneline`

---

target = target of the merge (main in this example)
source = solution branch

To merge branches, 
* 1 switch to the target(main) branch `git checkout <target-branch>`
* 2 merge in the source(solution) branch with `git merge <source-branch>`

To compare the two branches, use `git diff <branch1> <branch2>`

---

`git rebase` is used to clean up local history to focus on the end result. This should increase accuracy and clarity.
Do not use rebase on a public branch. 
You can use rebase to squash multiple commits into 1. 

Check to see which commit to use to start a rebase: `git merge-base <source-branch> <target-branch>`
Start the rebase with 


Then git will open the file and show the commits you can work with
```
pick 34f86e9 Added Notes
pick ca9e66e Commit 1
pick d7f8d31 Commit 2
pick 1061789 Commit 3
```
Change `pick` to `squash` to merge multiple commit in