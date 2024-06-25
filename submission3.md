# DevOps Lab 3
## Task 1: Understanding Version Control Systems
### The output:
```bash
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git cat-file -p 38fba9ea8dbfd553fcd642bb1b414ac8c4e21f24
tree f2ebbf7fec89fd4f0bdad6a977e1c4fa7ca3d889
parent 3439b8580f57cbf816393416797d0a06d3dc4d6c
author ro1ven <ku_ku_2018@bk.ru> 1719330918 +0300
committer ro1ven <ku_ku_2018@bk.ru> 1719330918 +0300

third commit
```

## Task 2:
### git reset output:
```bash
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git add .
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git commit -m "task1 is completed"
[rybaev-ilya-lab-3 c7360d8] task1 is completed
 1 file changed, 12 insertions(+)
 create mode 100644 submission3.md
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git checkout -b git-reset-practice
Switched to a new branch 'git-reset-practice'
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ echo "First commit" > file.txt
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git add file.txt
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git commit -m "Task2 First commit"
[git-reset-practice 6b1055f] Task2 First commit
 1 file changed, 1 insertion(+)
 create mode 100644 file.txt
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ echo "Second commit" >> file.txt
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git add file.txt
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git commit -m "Task2 Second commit"
[git-reset-practice 4a47ff0] Task2 Second commit
 1 file changed, 1 insertion(+)
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ echo "Third commit" >> file.txt
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git add file.txt
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git commit -m "Task3 Third commit"
[git-reset-practice e627eaa] Task3 Third commit
 1 file changed, 1 insertion(+)
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git reset --soft HEAD~1
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git reset --hard HEAD~1
HEAD is now at 6b1055f Task2 First commit
```
### git reset description:
1. **git reset --soft <commit>**: This option resets the HEAD to the specified commit but keeps the changes from that commit in the working directory and index. This allows you to make changes and recommit them.

2. **git reset --mixed <commit>**: By default, if no parameter is specified, --mixed is used. This mode resets the HEAD to the specified commit and unstages changes in the index but leaves the working directory untouched. You keep your changes, but they are not staged.

3. **git reset --hard <commit>**: This mode resets the HEAD to the specified commit and completely resets both the index and working directory to the state of the specified commit. All unsaved changes will be lost irretrievably.
### git reflog output:
```bash
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git reflog
6b1055f (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
4a47ff0 HEAD@{1}: reset: moving to HEAD~1
e627eaa HEAD@{2}: commit: Task3 Third commit
4a47ff0 HEAD@{3}: commit: Task2 Second commit
6b1055f (HEAD -> git-reset-practice) HEAD@{4}: commit: Task2 First commit
c7360d8 (rybaev-ilya-lab-3) HEAD@{5}: checkout: moving from rybaev-ilya-lab-3 to git-reset-practice
c7360d8 (rybaev-ilya-lab-3) HEAD@{6}: commit: task1 is completed
38fba9e HEAD@{7}: commit: third commit
3439b85 HEAD@{8}: commit: second commit
e358649 HEAD@{9}: commit: first commit
73e47a9 (origin/master, origin/HEAD, master) HEAD@{10}: checkout: moving from master to rybaev-ilya-lab-3
73e47a9 (origin/master, origin/HEAD, master) HEAD@{11}: clone: from github.com:Aardes-Roiven/Sum24-intro-labs.git
```
### git reflog --hard output:
```bash
roiven@DESKTOP-A1GU1QC:~/DEVOPS$ git reset --hard e627eaa
HEAD is now at e627eaa Task3 Third commit
```
`The result - the third commit came back`
### git reflog description:
git reflog is a Git command that allows to view and manage the history of references (refs) in the repository. It shows the history of HEAD and other references, such as branches and tags, even if you have changed or reset them.
