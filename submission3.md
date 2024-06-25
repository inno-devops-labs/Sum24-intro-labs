## Task 1

### <commit_hash>:
```
git cat-file -p e40234e217e6d057108ebbe49c52ee3cfd8a3c0d
```
tree a48cb2589d5f58753e7e198a3df4dde8780cf1bd \
parent 44a900da28ed3ec9baed3e250a322bfd48d0dd78 \
author Dmitriy Creed <creed@soramitsu.co.jp> 1718740524 +0300 \
committer Dmitriy Creed <creed@soramitsu.co.jp> 1718740524 +0300 

Upload lab3 & lab4 

Signed-off-by: Dmitriy Creed <creed@soramitsu.co.jp>

### <tree_hash>:
```
git cat-file -p a48cb2589d5f58753e7e
```
100644 blob ede183da8ef201e5f5737eea502edc77fd8a9bdc    README.md \
100644 blob 5738bc15a0416ad2624df13badfb235052777e79    index.html \
100644 blob c54a520ec380d5cc77c55f2e40fe921fc5580de5    lab1.md \
100644 blob 1b99cc0044f93f556a0f6a599c7edf2f33f4944a    lab2.md \
100644 blob 2f8463cc188ec6ca69ae7a0f98d38e132280becb    lab3.md \
100644 blob ee2e111d04704f3b786d6de30381034edc0fefb6    lab4.md 

### <blob_hash>:
```
git cat-file -p 5738bc15a0416
```
```
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
</html>
```


## Task 2

### Simulate three commits

![alt text](/screens/commits3.png)

### Two Soft Resets
Accidently I made soft reset on one commit two times. Result is file sttay the same and contains text "Third commit", so command just moves the position of the HEAD without touching stage area.

![alt text](/screens/2softreset.png)

### One Hard Reset
Since i have spend two previous commits, I made hard reset on commit when "file.txt" file was not created. I didn't screen explorer, but as evidence I leave screen of git log, which says that I was on commit after completing Task 1 of this lab. Hard reset in difference with soft reset, do not just moves HEAD pointer but also deletes passed commits, which reflects on working area. In my case "file.txt" disapeared, because at the moment of completing of the first task it didn't exist.

![alt text](/screens/1hardreset.png)

### Reflog
Git redflog shows journal of actions made, reset command too.

![alt text](/screens/reflog.png)


### Reset reseted three commits
Reset command pointing to reflog hash, returns changes made after this. In my case, I have hard reseted my previous 2 soft and 1 hard reset. And come back to working stage with "file.txt" with text "Third commit".
![alt text](/screens/fileHealed.png)