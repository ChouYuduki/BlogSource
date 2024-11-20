+++
date = '2024-11-19'
title = 'How To Use Git'
author = 'Saka'
description = "Git Tutorial"
categories = [
    "Linux"
]
tags = [
    "Git",
    "Tutorial"
]

+++
### 1. Initial your directory

use this command to initial the current dir: `git init` 

then you can use this command to check your dir’s status: `git status` 

### 2. submit your files

add all of your modifying: `git add .` 

*if you want to retract your add, use this: `git reset`* 

then your should tell git who you are: `git config --global [user.name](http://user.name) "[your name]"`

finally push your files: `git commit -m "[what you modified]"` 

### 3. ignore your files

if these are some files you don’t want git to track, first create a file called `.gitignore` 

then add files’ name into this file

{{<quote>}}
💡 
**if you let git start tracking some file, 
it will keep tracking it, 
even you try to ignore it after tracking, 
so you have to let git stop tracking the file:**


`git rm --cached [file name]`

{{</quote>}}

### 4. add branch

check now all of branches in this directory: `git branch`

you can use the command to create new branch: `git branch [branch name]`

then switch to the branch `git checkout [branch name]` 

if you want to switch back to the main branch: `git checkout master`

if you want to merge the branch to your main branch: `git merge [branch name]` 

if you want to delete the branch: `git branch -d [branch name]` 

### 5. submit to github

first create a new repository in github, and get it’s link:


in terminal tell where is your repository:

`git remote add origin [https://github.com/link/....git]` 

then push your directory:

`git push --set-upstream origin master` or `git push -u origin master`

here github may let you input your username and pwd,

**But This Password is NOT your github login password!!!**

**go to github `setting > Developer Settings > Personal access tokens`**


**and remember to tickle all of below**


then copy your personal access tokens, it will be shown only once.

finally paste it on the password field of the terminal.

if you want github remember your info here, run this command line before you push:

`git config credential.helper store` 

after the above, every time you want to push your modification, just use `git push` without any additional parameters.

### get newest version of this repository

use `git pull` in this directory to get newest modificaiton

### others
`git clone --recursive`
clone main repository and all of submodules at the same time