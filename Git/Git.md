# Git Guide

> **Fundamental Concepts**

Working Directory

Stage(Index)

Repository

![1](.\resource\1.PNG)
![2](.\resource\2.PNG)
![3](.\resource\3.PNG)



***

> **Basic Commands**



~~~bash
git config --global user.name "Your name"
git config --global user.email "email@example.com"


#commonly used commands
#initialize a repository
#add some modifications
#commit some modifications with some messages
git init
git add filename1.txt filename2.md
#git add . saves all changes except delteing something
git add .
#git add -A really means saving all changes
git add -A
#git add -u means saving modifying and deleting except creating new documents
git add -u
git commit -m "message"


#check some information of current git repository
git status
git diff


#check commit id & repository history
git log
git log -- pretty=oneline
#version back
#HEAD refers to current version
#HEAD^ refers to the former one
#we can understand other situations by analogy 
git reset --hard HEAD^
git reset --hard HEAD^^
git reset --hard HEAD~100
git reset --hard <some commitid>
#list of executed commands
#when you reset to some former version but regret(forget some commit ids)
#use this commands to check the history of commands about version control to get some information
git reflog


#commands to undo changes
#discard changes in working directory
#-- means working directory
#it replaces working directory with the version in repository
git checkout -- <file>
git restore <file>
#unstage changes
git reset HEAD <file>
git restore --staged <file>


#delete some file
git rm <file>


#remote repository basic
#associate remote repository on Github
ssh-keygen -t rsa -C "yourmail@example.com"
git remote add origin git@github.com:username/projectname
git push -u origin master
#check some information about remote repository
git remote -v
#remove remote repository
#it just means unbinding local and remote repository
#rather than deleting remote repository physically
git remote rm origin
git remote rm <name>
#clone remote repository
git clone git@github.com:username/projectname.git
git clone https:://github.com/username/projectname


#basic branches management
#pointer:HEAD->master or  HEAD->otherbranches
#create a new branch dev
#commands parameter b meams create and switch
git checkout -b dev
git switch -c dev
#another way to create
git branch dev
#more ways to switch
git checkout dev
git switch master
#check branch list & current branch
git branch


#merging branches
#this command merges specified branch to current branch
git merge dev
#delete branches
git branch -d dev
#use this command to check merging graphs
git log --graph
#use this to check commits only
git log --pretty=oneline --abbrev-commit
#--no-ff  mode v.s fast forward mode
#--no-ff mode means generating a new commit while megring
#the merged history has branches which means you can identify the merging history
#while the latter cannot(we have no idea whether there was a merging operation)
#from another prespective
#--no-ff means new a space(which copies the content dev points at) and let master point at it
#while fastforward do not new a pointer,it just let master points at something the pointer dev points
git merge --no-ff -m "merge with --no-ff" dev 


#bug branches
#in this situation,we want to save our working directory temporarily and restore it later
#save working directory
git stash
#check saved working directory
git stash list
#restore or delete saved working directory
#attention:when you ues this command,coressponding stash item will not be deleted
git stash apply stash@{one number on the list}
#delete specific stash item
git stash drop stash@{one number on the list}
#restore the working directory item and delete the item in the list
git stash pop 
#copy one spcific commit to current branch
git cherry-pick <commit id>


#delete one branch which is never be merged by force
git branch -D <branch name>


#remote repository advanced
#while executing git clone, we can only see master branch by default
#if we want to develop programs in dev branch,we should fetch remote origin/dev to local environment
git checkout -b dev origin/dev
#if command "git push" fails
#usually it is because remote repository is ahead of local repository
#in collaborative development, it happens when other people push some commits to remote repository
#try use this to fetch newest commits from origin/somebranch
git pull
#if git pull fails
#it is may because we did not specify connections between local branch and origin/branch,try use this to track remote branch from origin and pull again
git branch --set-upstream-to=origin/dev dev
git branch --set-upstream-to <branch-name> origin/<branch-name>
git pull
#if remote repository is ahead of local repository, we need to execute git pull
#but this integration will creat extra merge commits
#if many corporators have done this, git log would be a diaster
#we can use the following commands to avoid this
git rebase
#when we use the following command, we should make sure working directory is clean
#we can commit or stash first
git pull -r
#if rebase procedure has conflicts
git rebase --abort
#or solve conflicts and execute
git rebase --continue


#tag management
#tag is an immovable pointer to a specific commit log
#bear in mind that a tag is always relating to one commit
#if this commit appears in master and dev simultaneously,it means we can see this tag 
#in each branch
#create a new tag
#the tag affixes to the latest commit by default
git tag v1.0
#tag affixes to one specific commit
git tag v0.9 <commit_id>
#tag with comments affixes to one specific commit
#-a assigns tagname
git tag -a v0.1 -m "some comments" <commit_id>
#check all tags
git tag
#check tag information in detail
git show <tagname>
#delete tags
git tag -d v0.1
#push tags to remote repository
git push origin <tagname>
git push origin --tags
#delete tags in remote repository
#first delete local tags, and delete remote tags
git tag -d v0.9
git push origin :refs/tags/v0.9

~~~

