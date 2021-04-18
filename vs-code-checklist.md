[√] Pull down branches to review
      Installed Github pull requests and issues extension
      Just click on the botton left branch to get changes
[√] Switch between branches without moving code between them
      Click the lower left hand branch button and pick branch. 
[√] Merge master into my branch
      Go to branch > Merge from Main.
[√] Merge other branch into my branch
      Branch > merge branch > select the branch to merge into current branch.
[ ] Squash all my commits into 1
      Have to use a Git Graph or similar extention
[√] Remove an unwanted commit / Go back to a pushed commit / Remove unwanted files
      Undo Last: Commit > Undo Last Commit
      Revert a file back to a previous commit: Use GitLens. Select File > File History > Commits > Right Click > Restore
      Revert a file removing a commit: Select File > File History > Commits > Right click on file > Commit > Revert Commit
[ ] Cherry Pick a commit from one branch to another
[ ] Reset a branch to be the same as a remote branch

  *Remember to replace `origin` and `master` with the remote and branch that you want to synchronize with*  
1. Retrieve lastest data from the original: `git fetch origin`  
2. throw away all my changes, forget everything on my current local branch make it same orgin/master: `git reset --hard origin/master`  
3. Remove unwanted files from your working directory: `git clean -f -d`  



[√] Git Stash
      Stash Pop: throws away the (topmost, by default) stash after applying it
      Stash Apply: leaves it in the stash list for possible later reuse (or you can then git stash drop it)

