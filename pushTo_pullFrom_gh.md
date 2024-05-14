## **"Push to" and "Pull from" a Github repository** ##
To push or pull changes to a remote repository, we need an SSH key to connect to our github account. To generate an ssh key, run `ssh-keygen -t <algorithm> -b <bytes> -C <comment>` command and follow the instructions.
```py
$ ssh-keygen -t ed25519 -C "miketeteganbenissan@gmail.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/root/.ssh/id_ed25519): ./key
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in ./key
Your public key has been saved in ./key.pub
The key fingerprint is:
SHA256:g0cZHishqCewJ9CdxSgJ4RN5y5a9S8Kh5pEyAufuk34 miketeteganbenissan@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
|o=.+.=o o        |
|+.*.+..o =       |
|o=o.+ . =        |
|* =* . +         |
|.B= . o S        |
|+=.o o . .       |
|=o..o .          |
| .+ E.           |
| ooo             |
+----[SHA256]-----+

$ ls
key  key.pub
```
In the above output, the command generates two key files, one private and one public. Now we have to copy the content of the public file in our github account to be able to authenticate.\
Once done, you can check you can authenticate to github by trying to ssh to **github.com**, using the private key.
```py
$ ssh git@github.com -i key
PTY allocation request failed on channel 0
Hi miketetegan! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```
From the output above, you can see that you can successfully authenticate to github.com.\
Now to finish, make sure the **ssh-agent** is running with `eval "$(ssh-agent -s)"` and add the private key file to the ssh agent by running `ssh-add <private_key>`. 
```py
$ eval "$(ssh-agent -s)"
Agent pid 15439

$ ssh-add key
Identity added: key (miketeteganbenissan@gmail.com) #the value in parenthesis is the comment we specified during the key creation
```
If we try to push to the repository, we can see we get an error. There is still some configurations left to do before we can push to our git repository.
```py
$ git push
fatal: No configured push destination.
Either specify the URL from the command-line or configure a remote repository using
    git remote add <remote_name> <url>
and then push using the remote name
    git push <remote_name>
```
We have to configured to which remote repository we want to push our changes to. Run `git remote add <name> <url>` to do so. To push the configuration, run `git push <remote_name>`. Let's push our configuration to our remote **test** repository.\
You can list configured remote repositories by running `git remote -v`.\
***Note that the repository should already exist in Github before you can push the changes to it***.
```py
$ git remote add origin git@github.com:miketetegan/test.git

$ git remote -v
origin  git@github.com:miketetegan/test.git (fetch)
origin  git@github.com:miketetegan/test.git (push)
```
Now we need to add the remote upstream branch we want to push to.  
The default branch created in Github is **main** but the one created in our local repository is named **master**, so we need to rename our local branch to match the remote Github branch name, by running `git branch -M <new_name>`. To list all branches, use `git branch -a`.
```py
$ git branch -a
* master

$ git branch -M main
$ git branch -a
* main

$ git push --set-upstream origin main
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Delta compression using up to 2 threads
Compressing objects: 100% (1/1), done.
Writing objects: 100% (1/1), 259 bytes | 51.00 KiB/s, done.
Total 1 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:miketetegan/test.git
   067914a..9a98bfc  main -> main
branch 'main' set up to track 'origin/main'.

$ git branch -a
* main
  remotes/origin/main
```
We can see that our local repo has been successfully pushed to the remote Github repository. The remote branch has also been added as shown in the above output.
To pull remote changes to local repo, we need to specify as well the remote repository we want to pull from and the branch name by running `git pull <remote> <branch>`.
```py
$ git pull origin main
remote: Enumerating objects: 24, done.
remote: Counting objects: 100% (24/24), done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 24 (delta 6), reused 8 (delta 1), pack-reused 0
Unpacking objects: 100% (24/24), 9.30 KiB | 238.00 KiB/s, done.
From github.com:miketetegan/git-basics
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
```

## Commands Summary ##
| Command | Description |
| --- | --- |
| `ssh-keygen` | Generates an SSH key pair |
| `ssh-add <key>` | Add a private key to the ssh-agent |
| `git remote add` | Add a remote repository |
| `git remote -v` | List configured remote repositories |
| `git branch -a` | List local and remote branches |
| `git branch -M` | Rename a branch |
| `git pull` | Pull from a remote repository |
| `git push` | Push to a remote repository |




