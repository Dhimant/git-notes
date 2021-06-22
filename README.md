# git-notes

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
