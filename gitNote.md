## start git

`git config --global user.name 'myName'`  
`git config --global user.email 'my@email'`  
set the user name and email.

`git init`  
creates repo with branch named master.

`git config --global init.defaultBranch main`  
change the default branch name.

`git status`  
to see the files state.

## commit

`git commit -m "msg"`  
take a snapshot of current state with msg.

## add

`git add fileName`  
`git add .`  
add the files to track.

## log

`git log`  
to see all git history and commits.

## checkout

`git checkout commitHash`  
change the head to specific commit.

`git checkout main`  
change head to latest commit in main branch.

`git checkout -b newBranch`  
create a new branch and set header to it.

## branch

`git branch -M main`  
change branch name to main.

`git branch branchName`  
create a new branch.

`git branch newBranch sourceBranch`  
create a new branch based on source branch.

## remote

`git remote add origin url`  
set remote origin to url.

`git remote add name url`  
set remote name to url.

## push

`git push -u origin main`  
push to remote origin to branch main.

`git push remoteName commitHash:remoteBranch`  
push specific commit to remote.

## merge

`git merge branchName`

## reset

`git reset commitHash`  
`git reset --soft commitHash`  
`git reset --hard commitHash`  
move to a past commit and ignore the fallowing commits. hard reset will delete the rest of commits.

## stash
`git stash -m "msg"`  
save changes without commit.

`git stash pop`  
pop the last stash and apply.

`git stash apply stashName`  
apply a stash from stash list.

`git stash list`  
see all stashes.

## extra commands

`git revert commitHash`  
works like reset but can keep the commits.

`git rebase HEAD~2 --exec "git commit --amend --no-edit --date 'now'"`  
change the date of commits with rebase.
