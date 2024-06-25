# Task 1: Understanding Version Control Systems

## Initial Commits and Inspections

### Initial Commit

# Output of git log
```sh
commit fabfea9c5a1f9901594495c9683d6df767171906 (HEAD -> lab3)
Author: ayodeko <akindekoayooluwa@gmail.com>
Date:   Wed Jun 26 01:32:52 2024 +0300

    Add submission3.md
```
### Inspecting the Commit
#### Output of git cat-file -p <commit_hash>
```sh
# Output of git cat-file -p <tree_hash>
tree 2a46ffeaec615f2beb2e2dd720595e0d77cd80a9
parent 73e47a96362163df885d217f65567b4def9f4727
author ayodeko <akindekoayooluwa@gmail.com> 1719354772 +0300
committer ayodeko <akindekoayooluwa@gmail.com> 1719354772 +0300
gpgsig -----BEGIN SSH SIGNATURE----- ******* 
 -----END SSH SIGNATURE-----
```

### Inspecting the Tree
```sh
# Output of git cat-file -p <tree_hash>
f2beb2e2dd720595e0d77cd80a9
100644 blob ede183da8ef201e5f5737eea502edc77fd8a9bdc    README.md
100644 blob 5738bc15a0416ad2624df13badfb235052777e79    index.html
100644 blob c54a520ec380d5cc77c55f2e40fe921fc5580de5    lab1.md
100644 blob 1b99cc0044f93f556a0f6a599c7edf2f33f4944a    lab2.md
100644 blob 2f8463cc188ec6ca69ae7a0f98d38e132280becb    lab3.md
100644 blob d66a6867f90e48f6f44d9d80821aa1d866a24882    lab4.md
100644 blob 2ff5995a25b74c9c02a143c09a9601ce66001a9f    lab5.md
100644 blob 793bb19cd158fae333205f524eba5adc16718c58    lab6.md
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    submission3.md

```
# Task 2: Practice with Git Reset Command

## Creating a New Branch
```sh
# Commands executed
git checkout -b git-reset-practice
```

## Created some commits

## Performing Soft Reset
```sh
# Commands executed
git reset --soft HEAD~1
```
## Performing Hard Reset
```sh
# Commands executed
git reset --hard HEAD~1
```
## Recovering Commits using Reflog
```sh
# Commands executed
git reflog
git reset --hard e69de29bb2d1d6434b8b29ae775ad8c2e48c5391
```
## Explanation of Reset and Reflog Process

- **Soft Reset**: Moves the HEAD pointer to the specified commit but leaves the index and working directory unchanged.
- **Hard Reset**: Moves the HEAD pointer to the specified commit and resets the index and working directory to match that commit.
- **Reflog**: Keeps a log of where the HEAD has been, allowing recovery of commits that might otherwise be lost after a reset.

