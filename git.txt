
=====Basic Commands=====

git init - initialize a new Git repository
git clone git@github.com:/username/repository.git - clone an existing repository using SSH
git status - shows the working directory status
git add [file] - add a file to the staging area (use git add . to add all files to the staging area)
git commit -m [message] - commit changes with a message
git push - push changes to the remote repository
git pull - fetch and merge changes from the remote repository

=====Branching and Merging=====

git branch - list branches
git branch [branch_name] - create a new branch
git checkout [branch_name] - switch to a branch
git merge [branch_name] - merge a branch into the current branch
git branch -d [branch_name] - delete a branch

=====Viewing History=====

git log - show commit logs
git log --oneline - show commit logs with a graph
git log --graph - show commit logs with a graph

=====Undoing Changes=====

git reset [file] - unstage a file
git checkout --[file] - discard changes in a file
git revert [commit] - revert a commit by creating a new commit

=====Remote Repository=====

git remote -v - list remote repositories
git remote add [name][url] - add a new remote repository
git fetch [remote] - fetch changes from a remote repository
git push [remote][branch] - push a branch to a remote repository
git pull [remote][branch] - pull changes from a remote repository branch

=====Stashing=====

git stash - save changes temporarily
git stash list - list all stashes
git stash apply [stash] - apply a stash
git stash drop [stash] - delete a stash

=====Tags=====

git tag - list tags
git tag [tag-name] - create a new tag
git push [remote][tag] - push a tag to a remote repository

=====Configuration=====

git config --global user.name "[name]" - set the global username
git config --global user.email "[email]" - set the global email
git config --list - list all configuration settings

=====Advanced Commands=====

git rebase [branch] - reapply commits on top of another base tip
git cherry-pick [commit] - apply the changes introduced by some existing commits
git bisect start - start binary search to find the commit that introduced a bug
git bisect bad - mark the current state as bad
git bisect good [commit] - mark a known good commit

=====.gitignore=====

# Compiled source #
###################
*.com
*.class
*.dll
*.exe
*.o
*.so

# Packages #
############
# it's better to unpack these files and commit the raw source
# git has its own built in compression methods
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip

# Logs and databases #
######################
*.log
*.sql
*.sqlite

# OS generated files #
######################
.DS_Store
Thumbs.db


