# Task 1

## Output for <blob_hash> objects

```bash
tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3)
$ git hash-object learning_git.txt
2732766c2e051f49a59bfb1777beffc9832bcbba
```

```bash
tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3)
$ git cat-file -p 2732766c2e051f49a59bfb1777beffc9832bcbba
This file was created to learn git vcs)
```

## Output for <tree_hash> structures

```bash
tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3)
$ git rev-parse HEAD
920312dd30e9d5c19ac7f39164a90299defe6a9a
```

```bash
tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3)
$ git cat-file -p 920312dd30e9d5c19ac7f39164a90299defe6a9a
tree d59f3f77a00557283a6f68e191dd76ec1398eda8
...
tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3)
$ git cat-file -p d59f3f77a00557283a6f68e191dd76ec1398eda8
100644 blob ede183da8ef201e5f5737eea502edc77fd8a9bdc    README.md
100644 blob 5738bc15a0416ad2624df13badfb235052777e79    index.html
100644 blob 2f8463cc188ec6ca69ae7a0f98d38e132280becb    lab3.md
100644 blob d66a6867f90e48f6f44d9d80821aa1d866a24882    lab4.md
100644 blob 2732766c2e051f49a59bfb1777beffc9832bcbba    learning_git.txt
```

## Output for <commit_hash> information

```bash
tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3)
$ git log -2
commit 920312dd30e9d5c19ac7f39164a90299defe6a9a (HEAD -> lab3, origin/lab3)
Author: Timmmich19 <tg.akhmatov@gmail.com>
Date:   Wed Jun 26 01:43:49 2024 +0300

    Created a file

commit 886c5198c10a3ecd3186dc2dc2ad701167dab5ac
Author: Timmmich19 <tg.akhmatov@gmail.com>
Date:   Wed Jun 26 01:40:07 2024 +0300

    Remooving some files from branch
```

```bash
tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3)
`$ git cat-file -p 886c5198c10a3ecd3186dc2dc2ad701167dab5ac`
tree 4fc88202e398c3b7bfc3b0694ce35d50732e166d
parent 73e47a96362163df885d217f65567b4def9f4727
author Timmmich19 <tg.akhmatov@gmail.com> 1719355207 +0300
committer Timmmich19 <tg.akhmatov@gmail.com> 1719355207 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAAZcAAAAHc3NoLXJzYQAAAAMBAAEAAAGBALJ5Ijuem2tRJ9+Ik5scuU
 mFMeBO34EWES4DeCqOk8dS6lPto9ZxhuE0aaX/SRST51Uar1KlxgOLQxmsockDnN5XJdIg
 VAtLr71lM7HtnSKTMVxPnhaC7OSUjPLY7jD7FJ09E1d4GsX78rM4K4tdCemVAWZBjZg8CW ...
 -----END SSH SIGNATURE-----

Remooving some files from branch

```

# Task 2

## Output

```bash
tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3|REBASE)
$ git checkout -b git-reset-practice
Switched to a new branch 'git-reset-practice'

tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3|REBASE)
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
[git-reset-practice 65aefb7] First commit
 1 file changed, 1 insertion(+)
 create mode 100644 file.txt
warning: in the working copy of 'file.txt', LF will be replaced by CRLF the next time Git touches it
[git-reset-practice ec55271] Second commit
 1 file changed, 1 insertion(+)
warning: in the working copy of 'file.txt', LF will be replaced by CRLF the next time Git touches it
[git-reset-practice fd2de40] Third commit
 1 file changed, 1 insertion(+)
```

## Reseting

```bash
tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3|REBASE)
$ git reset --soft HEAD~1

tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3|REBASE)
$ git reset --hard HEAD~1
HEAD is now at 65aefb7 First commit

tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3|REBASE)
$ git reflog
65aefb7 (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
ec55271 HEAD@{1}: reset: moving to HEAD~1
fd2de40 (origin/git-reset-practice) HEAD@{2}: commit: Third commit
ec55271 HEAD@{3}: commit: Second commit
65aefb7 (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
920312d (origin/lab3, lab3) HEAD@{5}: checkout: moving from lab3 to git-reset-practice
920312d (origin/lab3, lab3) HEAD@{6}: checkout: moving from git-reset-practiceclear to lab3
920312d (origin/lab3, lab3) HEAD@{7}: checkout: moving from lab3 to git-reset-practiceclear
920312d (origin/lab3, lab3) HEAD@{8}: commit: Created a file
886c519 HEAD@{9}: commit: Remooving some files from branch
73e47a9 (upstream/master, origin/master, origin/HEAD, master) HEAD@{10}: checkout: moving from master to lab3
73e47a9 (upstream/master, origin/master, origin/HEAD, master) HEAD@{11}: checkout: moving from lab1 to master
c621468 (origin/lab1, lab1) HEAD@{12}: checkout: moving from lab1 to lab1
c621468 (origin/lab1, lab1) HEAD@{13}: checkout: moving from master to lab1
73e47a9 (upstream/master, origin/master, origin/HEAD, master) HEAD@{14}: merge upstream/master: Fast-forward
44a900d HEAD@{15}: checkout: moving from master to master
44a900d HEAD@{16}: checkout: moving from master to master

tgakh@TIMMMICH MINGW64 ~/Documents/Projects/Sum24-intro-labs (lab3|REBASE)
$ git reset --hard fd2de40
HEAD is now at fd2de40 Third commit

```
