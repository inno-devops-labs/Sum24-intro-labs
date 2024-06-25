# Lab 3: Version Control
## Anton Buguev, a.buguev@innopolis.university, M23-RO-01

### Task 1. Understanding Version Control Systems.
1. Check info about commits:
```sh
git log
```
Result:
```sh
commit 185111351c7203cea469a70ab53923f477e76593 (HEAD -> lab3_solution, origin/lab3_solution)
Author: Anton <albugg2001@gmail.com>
Date:   Mon Jun 24 22:02:40 2024 +0300

    Create submission file
```
2. Copy commit hash and run

```sh
git cat-file -p 185111351c7203cea469a70ab53923f477e76593
```
Rsult:

```sh
tree 14ecc679ef9772e3025a4a1afbf5fcbc888ccbb0
parent 73e47a96362163df885d217f65567b4def9f4727
author Anton <albugg2001@gmail.com> 1719255760 +0300
committer Anton <albugg2001@gmail.com> 1719255760 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
<SSH SIGNATURE>
-----END SSH SIGNATURE-----

Create submission file
```
3. Copy tree hash and run
```sh
git cat-file -p 14ecc679ef9772e3025a4a1afbf5fcbc888ccbb0
```
Result:
```sh
100644 blob ede183da8ef201e5f5737eea502edc77fd8a9bdc	README.md
100644 blob 5738bc15a0416ad2624df13badfb235052777e79	index.html
100644 blob c54a520ec380d5cc77c55f2e40fe921fc5580de5	lab1.md
100644 blob 1b99cc0044f93f556a0f6a599c7edf2f33f4944a	lab2.md
100644 blob 2f8463cc188ec6ca69ae7a0f98d38e132280becb	lab3.md
100644 blob d66a6867f90e48f6f44d9d80821aa1d866a24882	lab4.md
100644 blob 2ff5995a25b74c9c02a143c09a9601ce66001a9f	lab5.md
100644 blob 793bb19cd158fae333205f524eba5adc16718c58	lab6.md
100644 blob 51c4a9ee2271d822dc1b6843a7c20051ee767760	submission3.md
```
4. Copy blob hash and run
```sh
git cat-file -p 51c4a9ee2271d822dc1b6843a7c20051ee767760
```
Result:
```sh
# Lab 3: Version Control
## Anton Buguev, a.buguev@innopolis.university, M23-RO-01

### Task 1. Understanding Version Control Systems.
```
### Task 2.

#### Part 1. Create commits.
1. Create branch:
```sh
$ git checkout -b git-reset-practice
```
Result:
```sh
Switched to a new branch 'git-reset-practice'
```

2. Create first commit:
```sh
$ echo "First commit" > file.txt
$ git add file.txt
$ git commit -m "First commit"
```
Result:
```sh
[git-reset-practice 8232ddd] First commit
 1 file changed, 1 insertion(+)
 create mode 100644 file.txt
 ```

3. Create second commit:
```sh   
$ echo "Second commit" >> file.txt
$ git add file.txt
$ git commit -m "Second commit"
```
Result:
```sh
[git-reset-practice 56e05ed] Second commit
 1 file changed, 1 insertion(+), 1 deletion(-)
```

4. Create third commit:
```sh
$ echo "Third commit" >> file.txt
$ git add file.txt
$ git commit -m "Third commit"
```
Result:
```sh
[git-reset-practice 5f9be81] Third commit
 1 file changed, 1 insertion(+), 1 deletion(-)
```

#### Part 2. GIT Reset.
1. Run **soft** reset:
```sh
$ git reset --soft HEAD~1
$ git log
```
Result:
```sh
commit 56e05ed70308e8d9046f69f719221fc15d2456b8 (HEAD -> git-reset-practice)
Author: Anton <albugg2001@gmail.com>
Date:   Mon Jun 24 22:25:25 2024 +0300

    Second commit

commit 8232dddf8e1bc858ca93d40f137ab34884a58799
Author: Anton <albugg2001@gmail.com>
Date:   Mon Jun 24 22:25:03 2024 +0300

    First commit
```
2. Run **hard** reset:
```sh
$ git reset --hard HEAD~1
```
Result:
```sh
HEAD is now at 8232ddd First commit
``` 

#### Part 3. Recover after reset.
1. Run
```sh
$ git reflog
```
Result:
```sh
8232ddd (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
56e05ed HEAD@{1}: reset: moving to HEAD~1
5f9be81 HEAD@{2}: commit: Third commit
56e05ed HEAD@{3}: commit: Second commit
8232ddd (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
d0a3fce (origin/lab3_solution, lab3_solution) HEAD@{5}: checkout: moving from lab3_solution to git-reset-practice
```
2. Recover after hard reset:
```sh
$  git reset --hard 5f9be81
```
Result:
```sh
HEAD is now at 5f9be81 Third commit
```

#### Part 4. Reset and reflog processes explained.
`git reset` allows to undo the commits and revert changes:

- `git reset --soft` cleans commits history but keeps files unchanged;

- `git reset --hard` cleans commits and reverts files to their state at reset commit.

`git reflog` shows all local changes at the branches. Such history allows to, for example, undo `git reset`.

