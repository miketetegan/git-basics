## **Commits management** ##

To edit the message of the last commit, use `git commit --amend -m "<message>"`.
```py
$ git log --oneline
d062f60 (HEAD -> master) old_commit
9d52b78 init commit

$ git commit --amend -m "new_commit"
[master b0920fe] new commit
 Date: Thu May 16 16:40:51 2024 +0000
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file1

 $ git log --oneline
d062f60 (HEAD -> master) new_commit
9d52b78 init commit
```
To edit the message of an old commit, is a multi step process.\ 
First, you need to start an interactive rebase with the hash of the commit you want to edit, by running `git rebase -i <commit_hash>`.\
Next you need to locate the line corresponding to the commit you want to rename in the opened editor and change the action from pick to reword or edit.\
Then you can modify the commit message, by running `git commit --amend`. \
To finish, run `git rebase --continue` to commit the changes.
```

```















