[√] Pull down branches to review
      Installed Github pull requests and issues extension
      Just click on the botton left branch to get changes
[√] Switch between branches without moving code between them
      Click the lower left hand branch button and pick branch. 
[√] Merge master into my branch
      Go to branch > Merge from Main.
[√] Merge other branch into my branch
      Switch to `other branch` and pull down latest. 
      Switch back to `my branch`
      Source control `...` > branch > merge branch > select the branch to merge into current branch.
[√] Squash all my commits into 1
      *Do not do this on main*
      - Open Git Graph > Right Click on commit that is previous to the one(s) you want to keep 
      - Select "Reset current branch to this commit"
      - You will then see to your left the unstaged changes belonging to all the commits you had before. Proceed to “Commit All…”
      - Finally, do a force push to origin to replace all your existing commits for a single one.
      - Reference: https://dannyherran.com/2020/06/git-squash-commit-vs-code/
[√] Remove an unwanted commit / Go back to a pushed commit / Remove unwanted files
      Undo Last: Commit > Undo Last Commit
      Revert a file back to a previous commit: Use GitLens. Select File > File History > Commits > Right Click > Restore
      Revert a file removing a commit: Select File > File History > Commits > Right click on file > Commit > Revert Commit
[√] Cherry Pick a commit from one branch to another
      From the branch that will receive the cherry pick > Open Git Graph > Right Click on the commit > Select Cherry Pick > Confirm with *Yes, Cherry Pick*

[√] Reset a branch to be the same as a remote branch
      Switch to the branch to reset > Open Git Graph > Right click on commit (master) that you would like to reset to > select *Reset Current Branch to this Commit*
      Then in terminal `git push` (might have to force with `-f`)
      
[√] Git Fetch
      Go to View > Command Palette > Type in Git Fetch
      OR go to Branches > little circle is fetch
[√] Git Stash
      Stash Pop: throws away the (topmost, by default) stash after applying it
      Stash Apply: leaves it in the stash list for possible later reuse (or you can then git stash drop it)

[x] Abort merge- for when too many conflicts from sandbox, loyalty, etc
      How to do this in VS Code? Use below terminal command:
      git merge --abort

[ ] Rebase