# Git Starter

### What is Git ?

Git is an open source distributed version control system

### Git Basics

# Git

### Initiate git in a project

There are two ways to initialise git for a project. 

- By running git init command in project base directory

```
> git init
```

- By cloning existing repo using git clone

```
> git clone https://github.com/iamvickyav/preparation.git
```

Once Git is initiated in the project, a hidden folder called **.git** gets created inside the project base directory

### Stages of a file
Untracked: the file exists, but is not part of git's version control
Staged: the file has been added to git's version control but changes have not been committed
Committed: the change has been committed

http://archaeogeek.github.io/foss4gukdontbeafraid/git/commandsummary.html

| Command 		| Usage  						    |
|--------------	|----------------------------------|
| git init  	| initialise a repository   	    |
| git add   	| add a file to the staging area   |
| git commit	| commit changes to the repository |
| git status	| show current status			    |
| git clone		| clone repository to local        |
| git push		| push to remote repo              |
| git pull		| download changes from remote repo|
