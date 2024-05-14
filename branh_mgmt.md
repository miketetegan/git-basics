## **Branches management** ##
To list all branches, local and remotes use `git branch -a`. We can see we have one local **main** and one remote **main** repositories.
```py
$ git branch -a
* main
  remotes/origin/main
```
To create a new branch, use `git branch <branch_name>` or `git checkout -b <branch_name` to create a branch and switch to the newly created branch.
By default, the new branch is created based on the currently selected branch. To create a new branch based on another one, run `git branch -c <based_branch> <new_branch>`.
***Note:Use `git checkout <branch>`*** to swicth from a branch to another.
```py
$ git branch dev
$ git branch -a
  dev
* main
  remotes/origin/main

$ git checkout -b prod
Switched to a new branch 'prod'
$ git branch -a
  dev
  main
* prod
  remotes/origin/main
```
To rename a branch run `git branch -M <old_name> <new_name>` or you can use `git branch -M <new_name>` if the branch you want to rename is currently selected.
```py
$ git branch -M prod production
$ git branch -a
  dev
  main
* production
  remotes/origin/main
```
To delete a branch, run `git branch -d <branch_name>`.\
***Note: The branch you want to delete should not be currently selected or you will get an error***
```py
$ git branch -a
  dev
  main
* production
  remotes/origin/main
$ git branch -d production
error: Cannot delete branch 'production' checked out at '/test'

$ git branch main
$ git branch -d production
$ git branch -a
  dev
* main
  remotes/origin/main
```
To merge a branch to another one, run `git merge <branch_to_merge>`. Let's merge the **dev** branch to the **main** branch.
```py
$ git checkout main
Switched to branch 'main'
$ git merge dev
Updating 716ae24..18945c2
Fast-forward
 1 file changed
```
Instead of merging, you can rebase the changes to move all your commits from the branch you want to merge from, to the main branch.
```py
$ git checkout prod
Switched to branch 'prod'
$ git rebase main
Successfully rebased and updated refs/heads/prod.
$ git log --oneline


$ git checkout main
Switched to branch 'main'
$ git rebase prod
Successfully rebased and updated refs/heads/main.
$ git log --oneline
```











