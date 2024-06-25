# Lab 1 
## Task 1

### Summary

Signing commits provides several key benefits:

* Authenticity: Signing commits with a cryptographic key ensures that the commits were made by the person who owns the key. This verifies the identity of the author, preventing impersonation.
* Integrity: Signed commits protect the integrity of the code. Any alterations to the commit after it has been signed will invalidate the signature, signaling potential tampering.
* Accountability: By signing commits, developers take responsibility for their changes. This accountability can improve code quality and foster a sense of ownership among contributors.
* Trust: Signed commits build trust within the development community. Other developers can be confident that the changes come from a verified source and that the codebase has not been compromised.
* Security: Signing commits is an important security measure in open-source and collaborative projects, where the code is exposed to a larger group. It helps prevent malicious actors from introducing unauthorized changes.
_____________________________________

## Task 2

### Summary

#### Standard Merge:

* **Process**: Integrates changes from a feature branch into the main branch with a merge commit.
* **History**: Preserves the complete commit history from the feature branch.
* **Benefits**: Retains detailed history of individual changes, useful for tracking and debugging.
* **Drawbacks**: Can lead to a cluttered commit history with many small or redundant commits.

#### Squash Merge:

* **Process**: Combines all commits from a feature branch into a single commit before merging into the main branch.
* **History**: Condenses multiple commits into one, simplifying the commit history.
* **Benefits**: Produces a cleaner, more readable commit history, ideal for small, self-contained features.
* **Drawbacks**: Loses detailed commit history of the feature branch, which may obscure the development process.

#### Rebase and Merge:

* **Process**: Reapplies commits from the feature branch onto the base branch, followed by a fast-forward merge.
* **History**: Linearizes commit history, eliminating merge commits.
* **Benefits**: Creates a linear, easier-to-follow commit history, simplifying history traversal and debugging.
* **Drawbacks**: Can be complex and risky if conflicts arise; rebasing can rewrite commit history, which may cause issues in collaborative environments if not handled carefully.