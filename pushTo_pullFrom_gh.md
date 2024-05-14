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
Identity added: key (miketeteganbenissan@gmail.com)
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
We have to configured to which remote repository we want to push our changes to. Run `git remote add <name> <url>` to do so. You can list configured remote repositories by running `git remote -v`\
```py
$ git remote add origin git@github.com:miketetegan/git-basics.git

$ git remote -v
origin  git@github.com:miketetegan/git-basics.git (fetch)
origin  git@github.com:miketetegan/git-basics.git (push)

```
To push the configuration, run `git push <remote_name>`. Let's push our configuration to our remote **git-basics** repository. Note that the repository should already exist in Github before you can push changes to it. 
















