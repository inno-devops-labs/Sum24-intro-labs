# Lab 1: Introduction to DevOps with Git

## Task 1: SSH Commit Signature Verification

Write a brief summary explaining the benefits of signing commits.

1. Verifies the author's identity, ensuring that the commit was indeed made by the claimed individual.

2. Provides assurance that the commit hasn't been tampered with since it was signed.

3. Signing commits ensures that code changes can be audited and traced back to authorized contributors.

## Task 2: Merge Strategies in Git

Write a brief summary comparing these merge strategies.

1. Standard Merge: This strategy combines changes from one branch into another. It creates a new commit in the target branch, preserving the commit history of both branches. This retains all individual commits, making the history clearer but potentially more cluttered.

2. Squash and Merge: This strategy condenses all changes from one branch into a single commit before merging it into another branch. It's useful for keeping the commit history clean and concise, especially for feature branches with many small, incremental commits. However, it loses the granularity of individual changes, which may make it **harder to trace back specific changes** in the history.

3. Rebase and Merge: With this strategy, changes from one branch are applied onto another branch by reapplying each commit on top of the target branch. It results in a linear history without merge commits, potentially making the history cleaner. However, it **can rewrite commit history**, which may cause issues if the branch is shared with others.

![Merge settings](/images/merge.png)