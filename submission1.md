# Task 1

- Authenticity: Signing a commit using an SSH key proves that the commit was made by the individual associated with the key, preventing unauthorized modifications or impersonation.
- Integrity: The signature guarantees that the commit’s content hasn’t been tampered with after it was signed. This ensures that the code, message, and metadata remain unchanged.

# Task 2

## Standart merge

__Pros:__
* Creates a merge commit that clearly documents the merge event.
* Provides a complete history of all branches involved in the merge. 

__Cons:__
* Can create a more complex commit history with multiple merge commits.
* Might introduce conflicts if changes overlap in different branches.

## Squash and merge

__Pros:__

* Creates a single commit representing the entire feature branch, simplifying the commit history.
* Suitable for small features or bug fixes where the commit history is less relevant.

__Cons:__

* Loses individual commit history of the feature branch.
* Difficult to revert specific changes as they are all combined into one commit.

## Rebase and Merge

__Pros:__

* Creates a linear commit history, making it easier to understand the development flow.
* Can be used to clean up and reorder commits before merging.

__Cons:__

* Can rewrite commit history, making it harder to track changes and collaborate with others.
* May introduce conflicts if changes are reapplied on top of existing commits.

## Why Standard Merge is preferred

The standard merge strategy is often preferred in collaborative environments due to its transparency and ability to maintain a clear and traceable commit history. 
     