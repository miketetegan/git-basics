## **Initialize a git repository and start tracking files** ##
To initialize a git repository and start tracking a folder's files, go in the folder and use `git init` commaand. To verify that the folder have been initialized, use `git status` or check if the "**.git**" folder has been created. This folder contains metadata and configurations of the repository\
In the example bellow the "**app**" folder has been initialized as a git repository.
```py
$ cd app/
$ git status
fatal: not a git repository (or any of the parent directories): .git

$ git init
Initialized empty Git repository in /app/.git

$ git status
On branch master
No commits yet
nothing to commit (create/copy files and use "git add" to track)

$ ls -a
.git
```
Now that the git repository is created, you can start creating your files and track them. In the example below, the "**test**" file has been created . To check it's tracking status, you can use `git status`.
```py
$ touch test
$ git status
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test
nothing added to commit but untracked files present (use "git add" to track)
```
In the above output, you can see that the test file is untracked. To add it to the tracked files, use `git add <file_name>` or `git add .` for all files in the folder.
```py
$ git add .
$ git status
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   test
```
Now that the file is tracked, you need to commit the changes to save them. To commit changes, Git uses some parameters to keep track of who commit the changes in a history. The required ones are your name and your email, configured by using respectively `git config --global user.name <name>` and `git config --global user.email <email>`. You can list the parameters with `git config --list`.\
To commit your changes, use `git commit -m <message>`. The message describes what the commit is about.
```py
$ git config --global user.name "mike"
$ git config --global user.email "miketeteganbenissan@gmail.com"
$ git commit -m "initialization"
[master (root-commit) 3ecdb4d] initialization
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test
```
Once the commit is complete, you can use `git logs` or `git logs --oneline` to check the commit history. You can notice that our configured parameters are used as part of the commit log, with a hash that uniquely identified this commit.
```py
$ git log
commit 3ecdb4d7de11653f3202d1db6565ac72eaefe69c (HEAD -> master)
Author: mike <miketeteganbenissan@gmail.com>
Date:   Tue May 14 10:34:33 2024 +0000
    initialization

$ git log --oneline
3ecdb4d (HEAD -> master) initialization
```

## Commands Summary ##
| Command | Description |
| --- | --- |
| `git init` | Initialize the folder as a Git repository |
| `git status` | Check Git tracked and untracked files |
| `git config --global user.email` | Configure the mail used in the commit history |
| `git config --global user.name` | Configure the username used in the commit history |
| `git add` | Add files to staging area |
| `git log` | Check the commit history |
| `git log --oneline` | Summary output of `git log` |


