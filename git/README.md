# Cheat Sheet for Git

This cheat sheet is filled with some handy tips and commands to use git cli in short time!

## Generate SSH Key

```bash
ssh-keygen -t ed25519 -C "email@email.com"
# ssh key will be store in ~/.ssh/ directory

# start ssh-agent in background
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

## Print remote origing

```bash
git remote -v
```

## Add new remote

```bash
# new_remote_name - name of the remote repository how it is printed in the list of the remotes
# remote_url is URL of the remote that is used during the clone command, for instance
git remote add new_remote_name remote_url

# push to the branch_name in new_remore_name repository
git push new_remote_name branch_name
```

## New branch in the remote

```bash
# creates new_feature_branch branch on top of the main branch of the remote_repository repository 
git checkout -b new_feature_branch remote_repository/main

git add .
git commit -m "describe changes in the commit"
git push remote_repository new_feature_branch

# set upstream for local branch to the remote branch, after setting upstream you can
# simply use git push nad git pull without specifying the remote and branch names
git push --set-upstream remote_repository new_feature_branch
```

## Switch to the branches between remote repositories


```bash
git fetch remote_repository
git checkout remote_repository/branch_name
```

## Sync remote branch with fork's remote

```bash
# first, fetch the latest changes from the original remote repository
# assume upstream is the name of the original name of the remote repository
# original is the name of the remote repository of the fork
git fetch upstream

# checkout the feature branches where changes maden
git checkout feature_branch

# this command will apply feature branch's changes on top of the latest main
# from original repository, need to resolve any conflicts if they arise
git rebase upstream/main

# will update feature_branch in the remote repository with rebased changes
git push origin feature_branch
```