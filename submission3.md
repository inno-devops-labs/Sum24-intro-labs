# Lab4: Version Control

## Task 1: Understanding Version Control Systems

```
igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git cat-file -p lab3^{tree}
100644 blob ede183da8ef201e5f5737eea502edc77fd8a9bdc	README.md
040000 tree 07753f428765ac1afe2020b24e40785869bd4a85	dir
100644 blob 5738bc15a0416ad2624df13badfb235052777e79	index.html
100644 blob c54a520ec380d5cc77c55f2e40fe921fc5580de5	lab1.md
100644 blob 1b99cc0044f93f556a0f6a599c7edf2f33f4944a	lab2.md
100644 blob 2f8463cc188ec6ca69ae7a0f98d38e132280becb	lab3.md
100644 blob ee2e111d04704f3b786d6de30381034edc0fefb6	lab4.md

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git cat-file -p 5738bc15a0416ad2624df13badfb235052777e79
<!DOCTYPE html> 
<!-- You can modify it as you wish -->
<html>
<head>
    <title>My Simple Website</title>
</head>
<body>
    <h1>Welcome to My Simple Website</h1>
    <p>This is the content of the folder.</p>
    <ul>
        <li>File 1</li>
        <li>File 2</li>
        <li>File 3</li>
    </ul>
</body>

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git cat-file -p 07753f428765ac1afe2020b24e40785869bd4a85
100644 blob d95f3ad14dee633a758d2e331151e950dd13e4ed	file

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git cat-file -p 812574642245295d1e15dadb9f626ec3d4f9f387
tree 660b6631ea7335eb2ebddf27fcac012c813318eb
parent e40234e217e6d057108ebbe49c52ee3cfd8a3c0d
author Igor Parfenov <parfenov_2001@mail.ru> 1718783718 +0300
committer Igor Parfenov <parfenov_2001@mail.ru> 1718783718 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgWstC+Ugqc+0/arEKonRS7kshk+
 MHhZmiKlxJgglVpIYAAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQEbmLR6onCF86fLk9tgEDAFZGsN5macD+c2YzGRFt0D40engNHfzMTKhB6liJ8SfUh
 2s0ZhRXVK/wuhcRZ4zmQA=
 -----END SSH SIGNATURE-----

Add a directory
```

## Task 2: Practice with Git Reset Command

```
igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git checkout -b git-reset-practice
Switched to a new branch 'git-reset-practice'

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ echo "First commit" > file.txt
git add file.txt
git commit -m "First commit"

echo "Second commit" >> file.txt
git add file.txt
git commit -m "Second commit"

echo "Third commit" >> file.txt
git add file.txt
git commit -m "Third commit"
[git-reset-practice 510c10c] First commit
 1 file changed, 1 insertion(+)
 create mode 100644 file.txt
[git-reset-practice 308037d] Second commit
 1 file changed, 1 insertion(+)
[git-reset-practice 9a689fc] Third commit
 1 file changed, 1 insertion(+)

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git reset --soft HEAD~1

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git reflog
308037d (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
9a689fc HEAD@{1}: commit: Third commit
308037d (HEAD -> git-reset-practice) HEAD@{2}: commit: Second commit
510c10c HEAD@{3}: commit: First commit
8125746 (lab3) HEAD@{4}: checkout: moving from lab3 to git-reset-practice
...

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git reset --hard 9a689fc
HEAD is now at 9a689fc Third commit

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git reflog
9a689fc (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to 9a689fc
308037d HEAD@{1}: reset: moving to HEAD~1
9a689fc (HEAD -> git-reset-practice) HEAD@{2}: commit: Third commit
308037d HEAD@{3}: commit: Second commit
510c10c HEAD@{4}: commit: First commit
8125746 (lab3) HEAD@{5}: checkout: moving from lab3 to git-reset-practice
...

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git reset --hard HEAD~1
HEAD is now at 308037d Second commit

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git reflog
308037d (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
9a689fc HEAD@{1}: reset: moving to 9a689fc
308037d (HEAD -> git-reset-practice) HEAD@{2}: reset: moving to HEAD~1
9a689fc HEAD@{3}: commit: Third commit
308037d (HEAD -> git-reset-practice) HEAD@{4}: commit: Second commit
510c10c HEAD@{5}: commit: First commit
8125746 (lab3) HEAD@{6}: checkout: moving from lab3 to git-reset-practice
...

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git reset --hard 9a689fc
HEAD is now at 9a689fc Third commit

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ git reflog
9a689fc (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to 9a689fc
308037d HEAD@{1}: reset: moving to HEAD~1
9a689fc (HEAD -> git-reset-practice) HEAD@{2}: reset: moving to 9a689fc
308037d HEAD@{3}: reset: moving to HEAD~1
9a689fc (HEAD -> git-reset-practice) HEAD@{4}: commit: Third commit
308037d HEAD@{5}: commit: Second commit
510c10c HEAD@{6}: commit: First commit
8125746 (lab3) HEAD@{7}: checkout: moving from lab3 to git-reset-practice
...
```