Here are my learning notes of Git Essential Training on [Lynda](https://www.lynda.com/)

# chapter 00
Goal: use git to manage files and source code.  
what: 
* git is a distributed version control  
no need to communicate with a central server (faster, no network access required, no single failure point)
* developers can "fork" the project and work independently . 
* git concepts and [architecture](https://git-scm.com/about) .  
two-tree architecture, three-trees architecture . 
[git workflow](https://git-scm.com/about/distributed) . 
* commit message best practices   
be clear and descriptive
* commands .  
git add/commit/diff/ . 

Resource: [git official webiste](https://git-scm.com/)


# chapter 01 What's git
* what is Git used for?  
keep track of changes, for source control management, as a version control system
* features of distributed version control .  
users maintain their own repositories, don't have to work from a central repository, changes are stored as **change sets**.
# chapter 02 Install git
1. go to [here](https://git-scm.com/downloads). scm is short for source code mamangement . 
2. configure git: 
* System-level: for every user in this PC (not often); /etc/gitconfig; git config --system
* User-level: for a single/current user in this PC;  ~/.gitconfig; git config --global
* Project-based: only work for this project; my_project/.git/config; git config
3. Practice
```{r, engine='bash', count_lines}
# set 
git config --global user.name "LisaFan18"
git config --global user.email "haha@gmail.com"
git config --global core.editor "nano"
git config --global color.ui true
# retrieve
git config --list 
git config user.name
# check the configuration file
cat ~/.gitconfig
# Using git help
git help 
```
# chapter 03 Get Started
1. initialize: git init; .git
2. make changes: 
3. add the changes: git add .
4. commit changes to the repository with a message: git commit -m "..."
5. view the commit log: git log; git help log;
* best practices
  * be clear and descriptive, short single line summary (&lt; 50 chars)
  * optionally followed by a blank line and a more complete description. 
  * keep each line to &lt; 72 chars
  * write commit messages in present tense, not past tense. 
  * bullet points are usually asterisks or hyphens
  * add "ticket tracking numbers" from bugs or support requests
  * develop shorthand for your organization

```{r, engine='bash', count_lines}
#first go to the directory where git need to track, then run
git init 
# check the hidden directory of .git which is created by "git init", 
ls -la 
# config is the project-based configuration directory, if you no longer need git, just delete .git directory.
# view the log
git log
git log -n 1
git log --since=2019-07-06
git log --author="Lisa*"
git log --grep="init*"
```

# chapter 04 Git concepts and Architecture
