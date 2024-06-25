# Task 1
## The current version of tree exploration
### Command
$git cat-file -p a1dfe0321d3225f7c6a2606e5f7fbaaf47b5f32f
### Output
100644 blob ede183da8ef201e5f5737eea502edc77fd8a9bdc	README.md
100644 blob 5738bc15a0416ad2624df13badfb235052777e79	index.html
100644 blob c54a520ec380d5cc77c55f2e40fe921fc5580de5	lab1.md
100644 blob 1b99cc0044f93f556a0f6a599c7edf2f33f4944a	lab2.md
100644 blob 2f8463cc188ec6ca69ae7a0f98d38e132280becb	lab3.md
100644 blob d66a6867f90e48f6f44d9d80821aa1d866a24882	lab4.md
100644 blob 2ff5995a25b74c9c02a143c09a9601ce66001a9f	lab5.md
100644 blob 793bb19cd158fae333205f524eba5adc16718c58	lab6.md
100644 blob 25a7f1b257a4a4374f396b7d95d00a3c9758b0b8	test1
100644 blob 2a5709a11d9dde44b35fffdf327b5faec6a6f4e9	test2
100644 blob a8d6adad416380e4316c473f7e9bc3e3fb574a0e	test3

## The blob exploration
### Command
$git cat-file -p 25a7f1b257a4a4374f396b7d95d00a3c9758b0b8
### Output
test1 commit1

## The last commit exploration
### Command
$git cat-file -p ad1605d
### Output
tree a1dfe0321d3225f7c6a2606e5f7fbaaf47b5f32f
parent 2a34ac412bbd30478c49832029f4c7f1dcc4958c
author Alina1906 <airgear1906@gmail.com> 1719341185 +0300
committer Alina1906 <airgear1906@gmail.com> 1719341185 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgZnW4eRYaOHLK3epzvhtVomz9GF
 0sg2s5jUxy/WEo+nkAAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQLwvbnsFjD3zVNbLyJgNtsjD9I/4lo4VZrw2+4OvuvEN2PzE/1HyNBuFoQJjm6Fn2Z
 dLqm9WmuuslRmNA1ILBwc=
 -----END SSH SIGNATURE-----

added test3 file

# Task 2
## Steps performed
### 1. I created a series of commits. With each new commit I added a row to the file "file.txt" corresponded to the number of the commit.

**Commands and outputs:**<br>
$echo "First commit" > file.txt

$git add file.txt

$git commit -m "First commit"

[git-reset-practice 5c63476] First commit
 1 file changed, 1 insertion(+)
 create mode 100644 file.txt

$echo "Second commit" >> file.txt

$git add file.txt

$git commit -m "Second commit"

[git-reset-practice de75740] Second commit
 1 file changed, 1 insertion(+)

$echo "Third commit" >> file.txt

$git add file.txt

$git commit -m "Third commit"

[git-reset-practice bb775cf] Third commit
 1 file changed, 1 insertion(+)

$cat file.txt

First commit
Second commit
Third commit

### 2. Using the "reset" command, I moved to the 1st commit so that the changed I made in the 2nd and 3d commits have been dropped.

**Commands and outputs:**<br>
$git reset --soft HEAD~1

$git reset --hard HEAD~1

HEAD is now at 5c63476 First commit

$cat file.txt

First commit

### 3. Then, using the history of commits with the command "reflog", I got the hash of the commit I made before the reset to rollback the changes.

**Commands and outputs:**<br>
$git reflog

$git reset --hard bb775cf

HEAD is now at bb775cf Third commit

$cat file.txt

First commit
Second commit
Third commit

**Final reflog output:**<br>
bb775cf (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to bb775cf<br>
5c63476 HEAD@{1}: reset: moving to HEAD~1<br>
de75740 HEAD@{2}: reset: moving to HEAD~1<br>
bb775cf (HEAD -> git-reset-practice) HEAD@{3}: commit: Third commit<br>
de75740 HEAD@{4}: commit: Second commit<br>
5c63476 HEAD@{5}: commit: First commit<br>
ad1605d (lab3) HEAD@{6}: checkout: moving from lab3 to git-reset-practice<br>
