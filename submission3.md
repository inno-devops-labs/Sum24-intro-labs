### Task 1. Understanding Version Control Systems.
```Git Log``` to find commit hash
```sh
commit 87128d69d3f3606d005a2b591e625f86a92fc0ad (HEAD -> lab-3)
Author: AppleWolf <Stealth102@yandex.ru>

Date:   Tue Jun 25 14:04:38 2024 +0300

    Create submission file
```
```git cat-file -p 87128d69d3f3606d005a2b591e625f86a92fc0ad``` to inspect the contents of commit

```sh
tree c0c781579a11bf8df1020a3029255ee4509d2738
parent 73e47a96362163df885d217f65567b4def9f4727
author AppleWolf <Stealth102@yandex.ru> 1719313478 +0300
committer AppleWolf <Stealth102@yandex.ru> 171931347 +0300
```
```git cat-file -p c0c781579a11bf8df1020a3029255ee4509d2738``` to inspect the contents of tree
```sh
100644 blob ede183da8ef201e5f5737eea502edc77fd8a9bdc    README.md
100644 blob 5738bc15a0416ad2624df13badfb235052777e79    index.html
100644 blob c54a520ec380d5cc77c55f2e40fe921fc5580de5    lab1.md
100644 blob 1b99cc0044f93f556a0f6a599c7edf2f33f4944a    lab2.md
100644 blob 2f8463cc188ec6ca69ae7a0f98d38e132280becb    lab3.md
100644 blob d66a6867f90e48f6f44d9d80821aa1d866a24882    lab4.md
100644 blob 2ff5995a25b74c9c02a143c09a9601ce66001a9f    lab5.md
100644 blob 793bb19cd158fae333205f524eba5adc16718c58    lab6.md
100644 blob 955f5b75215bcc6f01f5c79461c27c2d0cb04414    submission3.md
```
```git cat-file -p 955f5b75215bcc6f01f5c79461c27c2d0cb04414``` to inspect the contents of blob
```sh
    ### Task 1. Understanding Version Control Systems.
```

### Task 2: Practice with Git Reset Command
1. ```git checkout -b git-reset-practice``` switch to a new branch
```sh
   Result: Switched to a new branch 'git-reset-practice'
```
#### 2.Explore Advanced Reset and Reflog Usage:

1. Create first commit:
```sh
echo "First commit" > file.txt
git add file.txt
git commit -m "First commit"
```
Output
```sh
[git-reset-practice f0689fc] First commit
1 file changed, 0 insertions(+), 0 deletions(-)
create mode 100644 file.txt
```

2. Create second commit:
```sh
echo "Second commit" >> file.txt
git add file.txt
git commit -m "Second commit"
```
Output
```sh
[git-reset-practice 73bedb8] Second commit
 1 file changed, 0 insertions(+), 0 deletions(-)
```
3. Create third commit:
```sh
echo "Third commit" >> file.txt
git add file.txt
git commit -m "Third commit"
```
Output
```sh
[git-reset-practice 74b6b14] Third commit
 1 file changed, 0 insertions(+), 0 deletions(-)
```
4.```git reset --soft HEAD~1```
```sh
PS E:\VSandAS\VisualStudioProjects\lab1,2\Sum24-intro-labs> git reset --soft HEAD~1
```
```git reset --hard HEAD~1```
```sh
PS E:\VSandAS\VisualStudioProjects\lab1,2\Sum24-intro-labs> git reset --hard HEAD~1
HEAD is now at f0689fc First commit
```
5.```git reflog```
```sh
PS E:\VSandAS\VisualStudioProjects\lab1,2\Sum24-intro-labs> git reflog
f0689fc (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
73bedb8 HEAD@{1}: reset: moving to HEAD~1
74b6b14 HEAD@{2}: commit: Third commit
73bedb8 HEAD@{3}: commit: Second commit
f0689fc (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
82def08 (origin/lab-3, lab-3) HEAD@{5}: checkout: moving from lab-3 to git-reset-practice
82def08 (origin/lab-3, lab-3) HEAD@{6}: checkout: moving from git-reset-practice to lab-3
82def08 (origin/lab-3, lab-3) HEAD@{7}: checkout: moving from lab-3 to git-reset-practice
82def08 (origin/lab-3, lab-3) HEAD@{8}: commit: Task 1 completed
```
```git reset --hard```
```sh
PS E:\VSandAS\VisualStudioProjects\lab1,2\Sum24-intro-labs> git reset --hard 74b6b14
HEAD is now at 74b6b14 Third commit
```
3.
 ```git reset --soft <commit>``` Moves your HEAD to the specified commit, but keeps all your changes in the staging area.

```git reset --hard <commit>``` Moves your HEAD to the specified commit and discards all changes made since that commit.

```git reflog``` Shows the history of all operations done on the repository, including commits, resets, and merges.