## Working with git branches 
From https://app.pluralsight.com/library/courses/working-git-branches/table-of-contents  
_Note on origin: `origin` is simply the nickname for the remote url. `remote add origin https://github.com/...` creates the nickname_  
_Example: `git push origin master` is the shorthand for  `git push https://github.com/elie/first_repo.git master`_


* list branches: `git branch`  
* list all local and remote branches: `git branch -a`  
* list only local branches: `git branch -r`   

  * _If you have color options on it’s also quite easy to tell which branches aren’t pulled down since they’re listed in red._  
* see the branches on a remote: `git ls-remote`  
* switch to a branch: `git checkout <branch-name>`  
* switch to a new branch: `git checkout -b <branch-name>`  

  * example: `git checkout -b working-with-code`  
* rename a branch: `git branch -m <oldName> <newName>`  
* delete a branch: `git branch -d <branch-nam>`  
* force delete a branch: `git branch -D <branch-name>`  
* see branch history: `git log` or `git log --oneline`  
* View changes that aren't pushed yet: `git diff origin/master..HEAD`  
* Save your changes, back to last commit `git reset HEAD^ --soft`  
* Discard changes, back to last commit `git reset HEAD^ --hard`  

---
## Turn your local repository into a mirror image of the remote of your choice  

  *Remember to replace `origin` and `master` with the remote and branch that you want to synchronize with*  
1. Retrieve lastest data from the original: `git fetch origin`  
2. throw away all my changes, forget everything on my current local branch make it same orgin/master: `git reset --hard origin/master`  
3. Remove unwanted files from your working directory: `git clean -f -d`  

* *If you need to undo a commit, use revert*  

### Quick Version: To overwrite your local files do:  

* `git fetch --all`  
* `git reset --hard <remote>/<branch_name>`  

For example:  
* `git fetch --all  `
* `git reset --hard origin/master  `

---
## Merge 

The easiest option is to merge the master branch into the feature branch using something like the following:
`git checkout feature`
`git merge master`

This creates a new “merge commit” in the feature branch that ties together the histories of both branches, giving you a branch structure that looks like this:
           _f_f_f__merge_commit
_master_m_/_m_m_m_/

To compare the two branches, use `git diff <branch1> <branch2>`

---
## Rebase 
https://www.atlassian.com/git/tutorials/merging-vs-rebasing

**Never use rebase on public branches**

`git rebase` is used to clean up local history to focus on the end result. This should increase accuracy and clarity.
Do not use rebase on a public branch. 
You can use rebase to squash multiple commits into 1. 
Rebasing will move work from `feature branch` directly onto the work from main. That way it would look like these two features were developed sequentially, when in reality they were developed in parallel.

Basic rebase instructions
* 1 git checkout `feature branch`
* 2 git rebase `master`  

Once you have rebased, if you try to push to GitHub, your push will be rejected because the remote branch has a different commit history. In order to bypass this, you can use the --force (or -f) flag after git push, but be very careful - this will override your GitHub commit history. You never want to do this if other people are working on that remote branch. This is only useful if you are alone and want to push up your commits before merging into a branch that others work on. 

---

* 1 Check to see which commit to use to start a rebase: `git merge-base <source-branch(solution)> <target-branch(main)>`
* 2 Start the rebase with `git rebase -i <commit-number-here, like ca9e666...>`
* 3 Then git will open the file and show the commits you can work with
```
pick 34f86e9 Added Notes
squash ca9e66e Commit 1
squash d7f8d31 Commit 2
squash 1061789 Commit 3
```
* 4 Change `pick` to `squash` to merge multiple commits in

--- 
## Cherry Pick 
https://www.atlassian.com/git/tutorials/cherry-pick

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
  `git pull --rebase` will use rebase instead of the default merge.


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
Steve Griffith : https://www.youtube.com/watch?v=ipav1TCV8BI

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


If you want to undo the last commit from a repo on github  
1 Get the SHA with `git log --online`
a808698     Fourth commit  
ca0bbb4     Third commit
5ffcac5     Second commit
ac49968     First commit
2 Move to previous commit and put Forth commit files back to staging area `git reset --soft ca0bbb4`
3 Edit these files  
4 Commit the files with `git commit -m 'some message'`
5 Push them back up with `git push -f` (-f because you are now behind the remote counterpart, and you will receive a terminal warning saying so)
---

## Git Revert
https://www.rithmschool.com/courses/git/git-github-reverting

`git revert` _undoes_ a commit by appending a new commit with the resulting content
`git reset` _removes_ the commit from commit history. *Dangerous*

Use `git revert HEAD~2` to revert a commit that is 2 back from where we are
```
touch first.txt # Create a file called `first.txt`
echo Start >> first.txt # Add the text "Start" to `first.txt`

git add . # Add the `first.txt` file
git commit -m "adding first" # Commit with the message "Adding first.txt"

echo WRONG > wrong.txt # Add the text "WRONG" to `wrong.txt`
git add . # Add the `wrong.txt` file
git commit -m "adding WRONG to wrong.txt" # Commit with the message "Adding WRONG to wrong.txt"

echo More >> first.txt # Add the text "More" to `first.txt`
git add . # Add the `first.txt` file
git commit -m "adding More to first.txt" # Commit with the message "Adding More to first.txt"

echo Even More >> first.txt # Add the text "Even More" to `first.txt`
git add . # Add the `first.txt` file
git commit -m "adding Even More to First.txt" # Commit with the message "Adding More to first.txt"

# OH NO! We want to undo the commit with the text "WRONG" - let's revert!
```
OR 
use `git log` and find the SHA of that commit 



---
## Git Diff

Once you have made a commit, you can see the message, author and some additional information using the git log command. When you type this in you will also see the full SHA, which, as we've discussed, is a unique identifier for the commit. To get out of git log you can type q.

As you work on a project by adding and modifying files and committing changes, your commit history will expand and your git log will grow. Sometimes you'll want to compare the history of your code at two different points in time. To do this, we can use the git diff command.

If you want to see differences between your commits you can use the git diff command and specify the SHA to compare. This will compare your code now to your code at that SHA. Here are a few different kinds of diff-s that you can see.

`git diff` - See changes in the working tree not yet staged for the next commit.

`git diff --cached` - See Changes between the staging area and your last commit.

`git diff HEAD` - See all changes in the working directory since your last commit.

`git diff ANOTHER_BRANCH` - compare with the latest code on another branch

`git diff HEAD~1 HEAD` - compare with the previous commit (add ~2, ~3 for older commits)

You can read more about git diff here: https://git-scm.com/docs/git-diff

---
## Git Clean 
`git clean` runs on untracked files. 
- Untracked files are those created within the working directory, but are not yet added to the tracking index.
- Once executed, you cannot undo `git clean`
- When it is fully executed, it will create a hard file system deletion.
- `git clean -n` shows what **would** be deleted but doesn't actually delete.
- Use `git clean -f` to actually delete.

## Git Stash
`git stash` will not save changes to the branch, but save them in a stash for later work. 
Use `git stash save "Description of changes here"` to stash your local uncommitted changes, thereby making your repo clean and free of changes again.

## PR Steps 
https://bocoup.com/blog/git-workflow-walkthrough-reviewing-pull-requests-local
1 Make local environment in a clean state by either stashing or saving to feature branch
2 Pull down the remote branch that the PR is based on with `git checkout -b BRANCHNAME origin/BRANCHNAME`

3 **OR** Pull down PR Branch with a **read-only** copy with `git fetch origin pull/ID/head:BRANCHNAME` 
- Example `git fetch origin pull/37/head:somechange`. This will give a ready only reference to the PR.
- `ID` is the numberical ID assigned to the PR, which you can see in the URL or at the top of the PR page. 
- `BRANCHNAME` is the local branch name you want to give it
4 Now switch this branch to local with `git checkout somechange`

5 If you used a feature branch approach and checked in your changes, you can just switch back to your feature branch and go.
- `git checkout your_feature_branch`
- If you used stash, run `git stash pop` and all stashed changes will be back locally and uncommitted.