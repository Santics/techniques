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
git add .
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
~~~

