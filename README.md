# Quick guide to working with git

## Definitions

**master**: The main branch in your local repo
**remote**: The shared repo that is at github
**origin**: An alias on your machine to the remote url for the github repo


## Starting a local repo

1.  Goto the folder you want as your root directory/s/s
2.  type: `git init`/s/s
3.  type: `git echo "*.tmp" >> .gitignore # ignore files in this file`/s/s
4.  type: `git add . # add all files in this directory`/s/s
5.  type: `git commit -am"my first commit" # add and a message`/s/s


## Link a local repo to a NEW repo at github

1.  Goto github and create a report (don't create a *README.md*)/s/s
2.  After you create the repo copy the new url that is created
3.  Back in your local repo type: `git remote add origin
    git@github.com:dwheelerau/git-howto.git`
*    The previous command adds the URL to the remote alias
5.  Then to push the local repo to github: `git push -u origin master`
*    This command is *push <remote> <local branch>*
