# Lab 1: Introduction to DevOps with Git

## Task 1: SSH Commit Signature Verification

- Authenticity - Signing commits with a cryptographic key ensures that the commit was made by the person who claims authorship, and not an impersonator.

- Integrity - A signed commit guarantees that the contents of the commit have not been tampered with since it was created.
  Accountability - Signed commits make it harder for someone to disavow their work, as the signature provides proof of who made the commit.

- Security - Signing commits with a private key that is kept secure makes it very difficult for an attacker to forge commits in someone else's name.
- Verification - Git hosting platforms like GitHub and GitLab can automatically verify signed commits, displaying a "Verified" badge to indicate the commit's authenticity.

![SSH signature for commits](/media/SSHsign.png)

## Task 2: Merge Strategies in Git

### Standard Merge

#### Combines two branches by creating a merge commit.

Pros:

- Preserves the commit history of both branches.
- Allows for easy tracking of changes.

Cons:

- Creates a new merge commit, which can lead to a cluttered commit history.

### Squash and Merge

#### Combines all commits from a feature branch into a single commit before merging.

Pros:

- Simplifies the commit history by reducing the number of commits.
- Makes it easier to review changes.

Cons:

- Loses the commit history of the feature branch.
- Can be difficult to track changes.

### Rebase and Merge

#### Reapplies commits from a feature branch onto the base branch.

Pros:

- Simplifies the commit history by reducing the number of commits.
- Makes it easier to track changes.

Cons:

- Changes the commit history of the feature branch.
- Can be difficult to track changes.\

### Why Standard Merge is Preferred

#### In collaborative environments, the standard merge strategy is often preferred because it:

Preserves the commit history of both branches, making it easier to track changes.
Allows for easy tracking of changes.
Does not alter the commit history of the feature branch.
In summary, the choice of merge strategy depends on the desired outcome and the complexity of the merge. While Squash and Merge and Rebase and Merge can simplify the commit history, they also have significant drawbacks. The standard merge strategy is often preferred in collaborative environments because it preserves the commit history and allows for easy tracking of changes.

![Merge settings](/media/merge.png)
