# Quick guide to working with git

There is an excellent tutorial [here](
https://www.atlassian.com/git/tutorials/syncing/git-push)<br>
## Definitions

**master**: The main branch in your local repo<br>
**remote**: The shared repo that is at github<br>
**origin**: An alias on your machine to the remote url for the github repo<br>
**upstream**: Changes that have occured in repo that are yet to get to you<br>
**patch**: Synonymouse with a `git diff` output

## Starting a local repo

1.  Goto the folder you want as your root directory
2.  type: `git init`
3.  type: `echo "*.tmp" >> .gitignore` to ignore files in this file
4.  type: `git add .`  to add all files in this directory
5.  type: `git commit -am"my first commit"` to add and a message (the 
-am part is shorthand for 'add' and -m 'message')


## Link a local repo to a NEW repo at github

1.  Goto [github](https://github.com) and create a report (don't create a *README.md*)
2.  After you create the repo copy the new url that is created
3.  Back in your local repo type: `git remote add origin
    git@github.com:dwheelerau/git-howto.git`
   * The previous command adds the URL to the remote alias
5.  Then to push the local repo to github: `git push -u origin master`
   * This command is `push <remote> <local branch>`

## Syncing things up with a pull

A pull will get changes from the remote and add them to your local repo. <br>

**Option 1**: 
This first option uses git fetch to allow you to compare your local version
with the one that is help at the remote. Once you are happy you can
git merge to sync them.

1.  Get the remote master: `git fetch origin`
   * This will create a new branch that is origin/master
   * Checking out this new branch will disconect you from HEAD ie
any changes you make on this branch won't effect anything locally
2.  Compare the two: `git diff master origin/master`
3.  If you are happy merge them: `git merge origin/master`
   * Make sure you are on your local master branch when you do the merge
   * You will have to fix any conflicts at this point

**Option 2**: 
This option uses git pull but maintains the history. Git pull automatically
calls git fetch and does the merge.

1.  Type: `git pull --rebase origin`
   * The rebase option is a good one because it puts your changes
on top of what others have done and maintains a linear history. The 
way that this works is that it incorporates all the changes in your 
current branch with that of the remote so that you are then it is posible to
do a simple fast-foward merge without having two separate histories.

**Option 3**: 
This option just wipes your local repo and replaces it with the remote.
Note that all local changes will be lost!

1.  Type: `git pull --force origin`

## Syncing things with a push

A push will sync the remote up with your local repo. <br>

**Option 1**: 
This option is a standard push<br>
1.  Type: `git fetch origin master` to get a copy of the remote<br>
2.  Type: `git rebase -i origin/master` to rebase the remote with your
    local<br>
3.  Type: `git push origin master` to push your changes to github<br>
   * Since you already did the rebase this should just be a simple fast-forward
   * The format of the above command is `git push <remote> <local_branch>`
   * It is ok not to rebase and just push if you are sure that your remote
has not changed since the last pull (ie you are the only one working on it). 
However, if the 
remote has changed as well as the local (ie someone else pushed to it), then
your push will no longer be a fast-forward (fast forwarding the outofdate
remote to be up to date with yours). In the case of non-fastforward changes
you will have to pull the remote and deal with any conflicts before you can
push to it (or deal with it via rebase). Makes sense really and beats option 2 
below!

**Option 2**: 
This option will force your remote to be a copy of your local. Be careful
as this could stuff other people up who might be sharing your repo.<br>
1.  Type: `git push <remote> --force`

**Option 3**: 
This option pushes all local branches to the remote repo.<br>
1.  Type: `git push <remote> --all`
