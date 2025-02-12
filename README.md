# git-reference

> Git command reference

- [terminal](#terminal)
- [setup](#setup)
- [state](#state)
- [branch](#branch)
- [remote](#remote)
- [commit](#commit)
- [stash](#stash)
- [sync](#sync)
- [rewrite history](#rewrite-history)
- [vanquish ghosts](#vanquish-ghosts)

## terminal
```bash
# navigate to a particular folder
cd "<path>"
# navigate up a folder
cd ..
# navigate to your home folder
cd
# list items in current folder
ls
# query size of subdirectories
du -h --max-depth=1 ./ | sort -hr
# query available CPU(s)
lscpu | grep -E '^Thread|^Core|^Socket|^CPU\('
# query free and used system memory
free -ght
# query total memory used per user
ps aux | awk 'NR != 1 {x[$1] += $4} END{ for(z in x) {print z, x[z]"%"}}' | sort -k2 -r
```

## setup
```bash
# check global and local git settings
git config --global -l
git config --local -l
# configure global git settings
git config --global user.name "<full-name>"
git config --global user.email "<email>"
git config --global core.editor "nano -w"
# configure local git settings
cd "<desired-path-for-local-settings>"
git config --local user.name "<local-full-name>"
git config --local user.email "<local-email>"
# initialize a local git repository
cd "<desired-path>"
git init
# clone a remote repository
git clone <https-origin-url>
```

## state
```bash
# check git status
git status
# check git log
git log                # verbose
git log --oneline      # condense each commit to a single line
git log --oneline -n 5 # print only the last 5 commits
```

## branch
```bash
# list all local branches
git branch
# create a local branch
git branch <local-branch-name>
# switch between branches and update working directory
git checkout <branch-name>
# delete local branch only if its commits are merged upstream
git branch -d <local-branch-name>
# delete local branch unconditionally
git branch -D <local-branch-name>
# delete remote branch
git push origin :<remote-branch-name>
# checkout a pull request
git fetch origin pull/<pr-number>/head:<branch-name>
# list branches and their creators
git for-each-ref --sort=authorname --format "%(authorname) %(refname)"
```

## remote
```bash
# view remote settings
git remote -v
# configure 'origin' remote branch
git remote add origin <https-origin-url>
# change 'origin' remote branch URL
git remote set-url origin <https-origin-url>
# configure 'upstream' remote branch (when working with a fork)
git remote add upstream <https-origin-url>
# change 'upstream' remote branch URL
git remote set-url upstream <https-origin-url>
```

## commit
```bash
# stage one file
git add <file.ext>
# stage all files (danger, this stages all changes)
git add .
# unstage one file
git reset HEAD <file.ext>
# commit with message
git commit -m "Message"
# amend a local commit
git commit --amend # this will open up the git editor
# push local commits to origin
git push origin <remote-branch-name>
```

## stash
```bash
# list all stashed files
git stash list
# stash all modified files without committing
git stash
# restore the most recent stashed files
git stash pop
# drop the most recent stashed files
git stash drop
```

## sync
```bash
# sync a local fork with changes made in upstream/main
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
# sync a local branch with changes made in origin/main
git fetch origin
git checkout <branch-name>
git merge origin/main
```

## rewrite history
```bash
git checkout <local-branch-name>
# undo Nth previous local commits, but keep the changes
git reset HEAD~N
# reset local branch to Nth previous commit
git reset --hard HEAD~N
# reset local and remote branches to a previous commit
git reset --hard <sha-of-last-commit-to-keep>
git push -f origin <remote-branch-name>
```

## vanquish ghosts
```bash
# prune remote branches
git fetch --prune origin
# prune upstream branches
git fetch --prune upstream
```
