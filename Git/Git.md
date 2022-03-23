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

#remote repository
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
~~~

