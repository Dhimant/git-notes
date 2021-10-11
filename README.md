# Git Notes

# Git can give you a heart attack ! 

**1. Match your local branch to remote branch**

    git fetch origin
    git reset --hard origin/master

    https://stackoverflow.com/questions/1628088/reset-local-repository-branch-to-be-just-like-remote-repository-head
    https://stackoverflow.com/questions/11225293/what-is-the-difference-between-git-reset-vs-git-rebase#:~:text=They%20are%20completely%20different.,rebase%20is%20what%20you%20want.

**2. Simple Git Strategy** 

    - Every new branch will be created from the Master branch.
    - Commit your changes to the new created branch
    - Merge newly created branch with Develop & Design
    - Merge newly created branch with Staging branch [ if want to deploy changes on the stage server]
    - Merge newly created branch with Master branch [If you want to deploy changes on the Live server]
   
   **Steps By Example**
   
    1. git pull origin master       
    2. create and checkout branch if not already
    
    git checkout -b bugfix/i-am-bug
    -- above command will create a new branch and also check it out
    git checkout bugfix/i-am-bug
    -- above command will checkout the branch once changes are done commit the branch 
    git commit -m "message for the commit"    
    git push origin bugfix/i-am-bug
    
    3.git checkout master
    
    4.git merge bugfix/i-am-bug
    
    5.git push origin master

   **Naming Convention** 

    hotfix/more-gray-shades
    coldfix/more-gray-shades
    feature/more-gray-shades
    patch/more-gray-shades
    extension/more-gray-shades
    bugfix/mobile-guest-customer
    
   **Git Questions**
   
   1. Git : List all unmerged changes in git
   ```
   git branch --no-merged master
   git branch --no-merged staging

   https://stackoverflow.com/questions/3600728/git-list-all-unmerged-changes-in-git
   ```
   2. Git View branches by creation date
   ```
   git for-each-ref --sort='-authordate'
   https://stackoverflow.com/questions/43214887/git-view-remote-branches-by-creation-date   
   ```
   3.How to see all local commits which are not pushed to the remote branch?
   ```
   git log --branches --not --remotes --no-walk --decorate --oneline

   https://stackoverflow.com/questions/39220870/in-git-list-names-of-branches-with-unpushed-commits
   https://stackoverflow.com/questions/30601511/how-to-see-all-local-commits-which-are-not-pushed-to-the-remote-branch
   ```
   4. How to find branches with uncommited changes
   5. How can I know if a branch has been already merged into master?
   ```
   git branch --merged master
   git branch --merged
   https://stackoverflow.com/questions/226976/how-can-i-know-if-a-branch-has-been-already-merged-into-master
   ```
   6. Git command to display HEAD commit id?
   ```
   git rev-parse HEAD
   git rev-parse --short HEAD
   git log -1
   git log | head -n 1 
   
   ```
   7. Git RollBack Pushed commits
   ```
   Example: You deployed the code after commit and now there are issues on production and you want to rollback
   
   Revert each commit one by one till to the branch you want to revert it back to, if there is any merge commit you must supply -m option usually with value 1
   
   https://stackoverflow.com/questions/4114095/how-do-i-revert-a-git-repository-to-a-previous-commit?noredirect=1&lq=1
   https://stackoverflow.com/questions/5970889/why-does-git-revert-complain-about-a-missing-m-option
   
   git revert --no-commit f2851f28 
   git revert --no-commit -m 1 7af9cc09    
   git revert --no-commit 760cb679 
   git revert --no-commit a4561389
  
   check your files after each revert
   once done 
   
   git commit
   
   if you want to abort the revert
   git revert --abort

   
   ```
   8. For Emergency rollback
   
   ```
    Example Scenario: 

    So you committed and merged some branches to master and deployed changed to production, but now you realised that it is breaking the site completely and you want to rollback immediately, because site is broke

    git reset --hard <old-commit-id>

    -- hard reset to last known working commit on local

    git push -f <remote-name> <branch-name>

    -- push changes to remote

    if the above push command does not work try the following
    git push origin HEAD --force

    https://stackoverflow.com/questions/4372435/how-can-i-rollback-a-git-repository-to-a-specific-commit
   
   ```
   9. Git Stash
   
   ```
   Example Scenario:
   You are working on a feature branch, it's not finished yet, and now you have a bug at production and have to move to another branch without commiting the current branch because your work is not complete yet. git stash is here for the rescue 
   
   https://www.atlassian.com/git/tutorials/saving-changes/git-stash
   
   Stashing your work

   git status
   git stash
   git status
   
   Re-applying your stashed changes
   
   git status
   git stash pop
   
   Above will only work for the files that are already tracked by git, new files won't be stashed, to stash new files track them using git add or use the below command
   
   git stash -u
   or
   git stash --include-untracked
   
   You can create multiple stash on same branch and list them using following command ( WIP means, Work In Progress )
   git stash list  
   
   git stash pop will apply the most recent stash stash@{0}

   You can choose which stash to re-apply by passing its identifier as the last argument, for example:
   
   git stash pop stash@{2}
 
   
   ```
   10. Create patch from commit

   ```
   git format-patch -1 {commitId}
   -- The above command will genetate the .patch file
   git apply m2-hotfixes/*.patch
   -- Apply patch using git apply command

   ```

    
