# Git commands

At its core, git is like a key value store. 
1.	The Value = Data and git stores the compressed data in a blob, along with metadata in a header which includes the identifier blob, size of the content, \0 delimiter and the actual content.
2.	The Key = Hash of the Data also called as SHA1. SHA1 is nothing but a 40-digit hexadecimal number for given a piece of data.
3.	GIT store its data in .git directory. And the blobs are stored in .git/objects folder.

```
root@bond:~/projects# echo 'Hello, World!' | git hash-object --stdin 
8ab686eafeb1f44702738c8b0f24f2567c36da6d
root@bond:~/projects#
 ```

## Does the hash of a file change if the filename changes?

No, SHA1 of the file remains unchanged (as shown below)
```
root@bond:~/projects/My_Articles# echo this is test file > test.txt
root@bond:~/projects/My_Articles# ls
README.md  articles  images  test.txt
root@bond:~/projects/My_Articles# shasum test.txt 
4a3adea6a7ca4a8ac6ccb8605317572c319786dc  test.txt
root@bond:~/projects/My_Articles# mv test.txt file1.txt
root@bond:~/projects/My_Articles# ls
README.md  articles  file1.txt  images
root@bond:~/projects/My_Articles# shasum file1.txt 
4a3adea6a7ca4a8ac6ccb8605317572c319786dc  file1.txt
root@bond:~/projects/My_Articles#
```

## How to check number of branches in git?
A branch is just a pointer to a particular commit. The pointer of the current branch changes as new commits are made.
```
root@bond:~/projects/My_Articles# git show-branch -a
* [develop] Installed PWSH 7 on ubuntu 18.04
 ! [origin/HEAD] Installed PWSH 7 on ubuntu 18.04
  ! [origin/develop] Installed PWSH 7 on ubuntu 18.04
   ! [origin/master] Created .gitignore file
----
*++  [develop] Installed PWSH 7 on ubuntu 18.04
*+++ [origin/master] Created .gitignore file
root@bond:~/projects/My_Articles#
```

### All the file changes are saved in .git/objects directory. Git cat-file command is used to check the type (-t) and content (-p) of the object
```
root@bond:~/projects/My_Articles# tree .git/objects/
.git/objects/
├── 1c
│   └── 4cb79e4d765f17fd97d70a8c52b04e996908fa
├── 9d
│   └── 8a4e73e4f8897352d20eda060a812dab709fc9
├── info
└── pack
    ├── pack-85af9fc9d0131cce8a6feeee184b459367d0f766.idx
    └── pack-85af9fc9d0131cce8a6feeee184b459367d0f766.pack

4 directories, 4 files
root@bond:~/projects/My_Articles# git cat-file -t 9d8a4e7
blob
root@bond:~/projects/My_Articles# git cat-file -p 9d8a4e7
this is test file
root@bond:~/projects/My_Articles# git cat-file -t 1c4cb79
blob
root@bond:~/projects/My_Articles# git cat-file -p 1c4cb79
this is test file
adding second line
root@bond:~/projects/My_Articles#
```
*If you change any data about the commit, the commit will have
a new SHA1 hash. Even if the files don’t change, the created date will. Therefore, we can’t change commits.*

### Run the following command to find the current commit the branch is pointing to.
```
root@bond:~/projects/My_Articles# cat .git/refs/heads/develop 
4dc0fd90374678db6e4298631fde4cd9a6c8543a
root@bond:~/projects/My_Articles# git cat-file -p 4dc0fd90
tree e2fa745f9c7dccea43822bf87b3703eafbe71705
parent 01ebee7630c3ede44f6577886f073df3eb2c98f5
author sharma-shruti <shruti26.inbox@gmail.com> 1585296091 +0000
committer sharma-shruti <shruti26.inbox@gmail.com> 1585296091 +0000

this is my test file
root@bond:~/projects/My_Articles#
```

## The code can be stored in any of these 3 areas in git.
1.	Working area – The files in working area, are stored locally and are not handled by git. They can be discarded or can be moved to the staging area. Also called as untracked files.
2.	Staging area - The staging area is how git knows what will change between the current commit and the next commit.
3.	The repository - git knows about all the files in repository and contains all of your commits.

## Headless OR Detached Head
1.	Sometimes you need to checkout a specific commit (or tag) instead of a branch. 
2.	git moves the HEAD pointer to that commit 
3.	as soon as you checkout a different branch or commit, the value of HEAD will point to the new SHA 
4.	There is no reference pointing to the commits you made in a detached state.
```
root@bond:~/projects/My_Articles# git tag my_first_tag
root@bond:~/projects/My_Articles# git show-ref --tags
2c899342c3c1e6822b8d861151761907e5d3bef5 refs/tags/my_first_tag
root@bond:~/projects/My_Articles# git tag --points-at 2c899
my_first_tag
root@bond:~/projects/My_Articles# git log --oneline
2c89934 (HEAD -> develop, tag: my_first_tag, origin/develop, origin/HEAD) Add new hello world file
4dc0fd9 this is my test file
01ebee7 Installed PWSH 7 on ubuntu 18.04
e849c0d (origin/master, master) Created .gitignore file
91ffb99 Created an articles folder and moved all .md file in to this folder.
4461ba4 Auto stash before rebase of "origin/develop"
bf2613c Created a document on github best practices
55d1043 Added some new images
root@bond:~/projects/My_Articles# git checkout 2c89934
Note: checking out '2c89934'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 2c89934 Add new hello world file
root@bond:~/projects/My_Articles#
```
## Create a Dangling Commit
Our previous commit - 2c89934 in this case - was made in a detached HEAD state, it doesn't have any references pointing to it. It's not part of a branch, and has no tags. This is called a Dangling Commit. You'll see this warning if you try to switch branches as below.

```
root@bond:~/projects/My_Articles# cat .git/HEAD
2c899342c3c1e6822b8d861151761907e5d3bef5
root@bond:~/projects/My_Articles# echo "This is a test file" > dangle.txt
root@bond:~/projects/My_Articles# git add dangle.txt

root@bond:~/projects/My_Articles# git commit -m "This is a dangling commit"
[detached HEAD 19eb3eb] This is a dangling commit
 1 file changed, 1 insertion(+)
 create mode 100644 dangle.txt

root@bond:~/projects/My_Articles# git log --oneline
19eb3eb (HEAD) This is a dangling commit
2c89934 (tag: my_first_tag, origin/develop, origin/HEAD, develop) Add new hello world file
4dc0fd9 this is my test file
01ebee7 Installed PWSH 7 on ubuntu 18.04
e849c0d (origin/master, master) Created .gitignore file

root@bond:~/projects/My_Articles# git checkout develop 
Warning: you are leaving 1 commit behind, not connected to
any of your branches:

  19eb3eb This is a dangling commit

If you want to keep it by creating a new branch, this may be a good time
to do so with:

 git branch <new-branch-name> 19eb3eb

Switched to branch 'develop'
Your branch is up to date with 'origin/develop'.
root@bond:~/projects/My_Articles#
```
