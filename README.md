# Quick guide to working with git

## Definitions

**master**: The main branch in your local repo<br>
**remote**: The shared repo that is at github<br>
**origin**: An alias on your machine to the remote url for the github repo<br>
**upstream**: Changes that have occured in repo that are yet to get to you<br>


## Starting a local repo

1.  Goto the folder you want as your root directory
2.  type: `git init`
3.  type: `git echo "*.tmp" >> .gitignore # ignore files in this file`
4.  type: `git add . # add all files in this directory`
5.  type: `git commit -am"my first commit" # add and a message`


## Link a local repo to a NEW repo at github

1.  Goto github and create a report (don't create a *README.md*)
2.  After you create the repo copy the new url that is created
3.  Back in your local repo type: `git remote add origin
    git@github.com:dwheelerau/git-howto.git`
   * The previous command adds the URL to the remote alias
5.  Then to push the local repo to github: `git push -u origin master`
   * This command is `push <remote> <local branch>`

## Syncing things up with a pull

**option 1**
This first option uses git fetch to allow you to compare your local version
with the one that is help at the remote. Once you are happy you can
git merge to sync them.

1.  Get the remote master: `git fetch origin`
   * This will create a new branch that is origin/master
   * Checking out this new branch will disconect you from HEAD ie
any changes you make on this branch won't effect anything locally
2.  Compare the two: git diff master origin/master
3.  If you are happy merge them: `git merge origin/master`
   * Make sure you are on your local master branch when you do the merge
   * You will have to fix any conflicts at this point

**Option 2**
This option uses git pull but maintains the history. Git pull automatically
calls git fetch and does the merge.

1.  Type: `git pull --rebase origin`
   * The rebase option is a good one because it puts your changes
on top of what others have done and maintains a linear history.

**Option 3**
This option just wipes your local repo and replaces it with the remote.
Note that all local changes will be lost!

1.  Type: `git pull --force origin`
