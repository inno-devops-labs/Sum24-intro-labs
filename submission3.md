## Lab 3 report
Kirill Glinskiy k.glinsky@innopolis.university
TG: @amrtized
### Task 1
First, i've made some comits in lab3 branch and pushed them to the origin.

```shell
touch dummy.txt
```
```shell
git add --all
git commit -m "minor: added empty .txt"
git push --set-upstream origin lab3
```
Next, I checked the hash of the current commit in HEAD. 
```shell
 git rev-parse HEAD

dd10c3fabdb52058e3e7d6f115c86004e8f17422
```

Let's check the content of hash:

```shell
git cat-file -p dd10c3fabdb52058e3e7d6f115c86004e8f17422
```
```
tree e7e37c59d9a07d3f2fc9faf179e5f03117a3198b
parent 5916f2682554fb755d1b38992d1875cb948561f3
author Kirill <k.glinsky@innopolis.university> 1719340754 +0300
committer Kirill <k.glinsky@innopolis.university> 1719340754 +0300

minor: added text to dummy.txt
```

Here we can find the hash of the tree. Let's inspect it:

```shell
git cat-file -p e7e37c59d9a07d3f2fc9faf179e5f03117a3198b
```
```
100644 blob ede183da8ef201e5f5737eea502edc77fd8a9bdc	README.md
100644 blob edaff9260ede06dbc15b1ec165f14d002cb400f3	dummy.txt
100644 blob 5738bc15a0416ad2624df13badfb235052777e79	index.html
100644 blob c54a520ec380d5cc77c55f2e40fe921fc5580de5	lab1.md
100644 blob 1b99cc0044f93f556a0f6a599c7edf2f33f4944a	lab2.md
100644 blob 2f8463cc188ec6ca69ae7a0f98d38e132280becb	lab3.md
100644 blob d66a6867f90e48f6f44d9d80821aa1d866a24882	lab4.md
100644 blob 2ff5995a25b74c9c02a143c09a9601ce66001a9f	lab5.md
100644 blob 793bb19cd158fae333205f524eba5adc16718c58	lab6.md
```

Let's inspect the blob of the latest file:

```shell
git cat-file -p edaff9260ede06dbc15b1ec165f14d002cb400f3
```
```
some dummy text
```
### Task 2
First we create new branch. For now it is stored locally, not up to date with main from origin.
```
git checkout -b git-reset-practice
```
```
Switched to a new branch 'git-reset-practice'
```
Next, we add series of commits to this branch. Commits go one by one.

```
echo "First commit" > file.txt
git add file.txt
git commit -m "First commit"
```
```
[git-reset-practice 5b1253a] First commit
 1 file changed, 1 insertion(+)
 create mode 100644 file.txt
```
```
echo "Second commit" >> file.txt
git add file.txt
git commit -m "Second commit"
```
```
[git-reset-practice f9451af] Second commit
 1 file changed, 1 insertion(+)
```
```
echo "Third commit" >> file.txt
git add file.txt
git commit -m "Third commit"
```
```
[git-reset-practice 415b65f] Third commit
 1 file changed, 1 insertion(+)
```

After that, we use ```git reset --soft HEAD~1``` to remove last commit, but still keep changes locally in our working directoryy.
After that, we use ```git reset --hard HEAD~1``` to remove both last commit and local changes.

```HEAD is now at 5b1253a First commit```

Now we are in the commit with the hash 5b1253a - our first insertion to file.txt. 

Let's use **reflog** to see how our HEAD have changed with time. It includes all changes of HEAD starting from the cloning of repo:

```
git reflog
```
```shell
5b1253a (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
f9451af HEAD@{1}: reset: moving to HEAD~1
415b65f HEAD@{2}: commit: Third commit
f9451af HEAD@{3}: commit: Second commit
5b1253a (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
dd10c3f (origin/lab3, lab3) HEAD@{5}: checkout: moving from lab3 to git-reset-practice
dd10c3f (origin/lab3, lab3) HEAD@{6}: commit: minor: added text to dummy.txt
5916f26 HEAD@{7}: commit: minor: added empty .txt
73e47a9 (origin/master, origin/HEAD, master) HEAD@{8}: checkout: moving from master to lab3
73e47a9 (origin/master, origin/HEAD, master) HEAD@{9}: clone: from https://github.com/PurplePegasuss/Sum24-intro-labs.git
```

Here we can see exactly what happened - 3 new commits + 2 resets reverting back to the 5b1253a.

Let's switch back to the times before those 3 commits:

```
git reset --hard  dd10c3f
```
```
HEAD is now at dd10c3f minor: added text to dummy.txt
```

That's it!

**reflog** is used to see how our HEAD have changed with time.

**git reset** is used to move the HEAD pointer to the chosen hash\head_id commit + removes files in working directory if --hard is chosen, and doesn't remove if --soft is chosen.
