# Lab 3 : Version Control

## Task 1: Understanding Version Control Systems

#### Adding a new directory and file to the repository.
```
suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (lab_three)
$ mkdir testFolder

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (lab_three)
$ ls
index.html  lab1.md  lab2.md  lab3.md  lab4.md  lab5.md  lab6.md  README.md  testFolder/

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (lab_three)
$ cd testFolder/

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs/testFolder (lab_three)
$ echo "hello world" > test.txt

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs/testFolder (lab_three)
$ ls
test.txt

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (lab_three)
$ git status
On branch lab_three
Your branch is up to date with 'origin/lab_three'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        testFolder/

nothing added to commit but untracked files present (use "git add" to track)

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (lab_three)
$ git add .
warning: in the working copy of 'testFolder/test.txt', LF will be replaced by CRLF the next time Git touches it

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (lab_three)
$ git commit -m "add test dir"
[lab_three 7b69c0a] add test dir
 1 file changed, 1 insertion(+)
 create mode 100644 testFolder/test.txt

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (lab_three)
$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 12 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (4/4), 563 bytes | 563.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:Suwi-inc/Sum24-intro-labs.git
   73e47a9..7b69c0a  lab_three -> lab_three

```
####  Inspecting the contents of blobs, trees, and commits.
```
suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (lab_three)
$ git rev-parse HEAD:testFolder/test.txt
3b18e512dba79e4c8300dd08aeb37f8e728b8dad

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (lab_three)
$ git cat-file -p 3b18e512dba79e4c8300dd08aeb37f8e728b8dad
hello world
```
```
suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (lab_three)
$ git rev-parse HEAD:testFolder
c3b8bb102afeca86037d5b5dd89ceeb0090eae9d

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (lab_three)
$ git cat-file -p c3b8bb102afeca86037d5b5dd89ceeb0090eae9d
100644 blob 3b18e512dba79e4c8300dd08aeb37f8e728b8dad    test.txt
```
```
suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (lab_three)
$ git cat-file -p 7b69c0a
tree c558622357846dcbd9419026c2f5db297a38b7f2
parent 73e47a96362163df885d217f65567b4def9f4727
author Suwi-inc <suwilanjisilwamba@gmail.com> 1719300383 +0300
committer Suwi-inc <suwilanjisilwamba@gmail.com> 1719300383 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgjC54SdeBdUFKlf8h+WLw/pARjr
 WJOobDGJrnHtL1TlEAAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQD5alr9RtSzYBtXFMFjzrFjSyHv8nc5oxlaiUzxZJUuwKfk2QICjd8HJdxdIxEkGKj
 BKKSpa3OwIWtVYaC0argY=
 -----END SSH SIGNATURE-----

add test dir
```
## Task 2: Practice with Git Reset Command

#### Checking out to git-reset-practice.
```
suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (master)
$ git checkout git-reset-practice
Switched to a new branch 'git-reset-practice'
branch 'git-reset-practice' set up to track 'origin/git-reset-practice'.

```
#### Making three commits.
```
suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ echo "First commit" > file.txt
git add file.txt
git commit -m "First commit"

echo "Second commit" >> file.txt
git add file.txt
git commit -m "Second commit"

echo "Third commit" >> file.txt
git add file.txt
git commit -m "Third commit"
warning: in the working copy of 'file.txt', LF will be replaced by CRLF the next time Git touches it
[git-reset-practice 06c6b10] First commit
 1 file changed, 1 insertion(+)
 create mode 100644 file.txt
warning: in the working copy of 'file.txt', LF will be replaced by CRLF the next time Git touches it
[git-reset-practice f262d94] Second commit
 1 file changed, 1 insertion(+)
warning: in the working copy of 'file.txt', LF will be replaced by CRLF the next time Git touches it
[git-reset-practice 9b164bc] Third commit
 1 file changed, 1 insertion(+)

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ git status
On branch git-reset-practice
Your branch is ahead of 'origin/git-reset-practice' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

```

#### Using ```git reset --soft HEAD~1``` removes the last commit from the current branch, but the file changes will stay in the working tree. In addition the changes will remain on the index.
```
suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ git reset --soft HEAD~1

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ git status
On branch git-reset-practice
Your branch is ahead of 'origin/git-reset-practice' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   file.txt

```
#### Checking the contents of the file shows that the working tree remains unchanged.
```
suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ cat file.txt
First commit
Second commit
Third commit
```
#### Using ```git reset --soft HEAD~1``` will remove all uncommited changes and all untracked files as well as the changes introduced in the last commit. The changes won't stay the your working tree.
```
suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ git reset --hard HEAD~1
HEAD is now at 06c6b10 First commit

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ git status
On branch git-reset-practice
Your branch is ahead of 'origin/git-reset-practice' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
#### The last commit after the soft reset was second commit, after running a hard reset this commit is removed and only first commit remains. The working tree has also been cleard.
```
suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ ls
file.txt  index.html  lab1.md  lab2.md  lab3.md  lab4.md  lab5.md  lab6.md  README.md

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ cat file.txt
First commit

```
#### git reflog shows the history of modifications made to the repository's HEAD pointer.
```
suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ git reflog
06c6b10 (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
f262d94 HEAD@{1}: reset: moving to HEAD~1
9b164bc HEAD@{2}: commit: Third commit
f262d94 HEAD@{3}: commit: Second commit
06c6b10 (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
73e47a9 (origin/master, origin/git-reset-practice, origin/HEAD, master) HEAD@{5}: checkout: moving from master to git-reset-practice

```
#### Running ```git reset --hard ``` with the commit hash reverts the changes back to this commit.
```
suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ git reset --hard 9b164bc
HEAD is now at 9b164bc Third commit

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ git status
On branch git-reset-practice
Your branch is ahead of 'origin/git-reset-practice' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

suwil@SUWILANJI-PCV3 MINGW64 ~/Desktop/First Year Masters/Third Semester/Devops/Lab 1/Sum24-intro-labs (git-reset-practice)
$ cat file.txt
First commit
Second commit
Third commit
```



