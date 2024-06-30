# SSH Commit Signature Verification

## Task 1

Signing commits enhances security by cryptographically verifying the identity of the commit author, ensuring that changes are made by authorized individuals. It acts as a extra level of security for a repo as it insures the commit is done from a trusted source.

## Task 2

### Standard Merge

**Standard Merge** creates a merge commit that brings together the changes from the feature branch and the main branch. This merge commit has two parent commits, preserving the history of both branches.

**Pros:**

- Preserves the complete history of both branches.
- Clear and traceable history of merges.
- Easy to understand the context of changes.

**Cons:**

- Can create a cluttered history with many merge commits.
- History can become less linear and harder to follow over time.

**Use Case:**
Standard merge is often preferred in collaborative environments because it preserves the context of changes and makes it easier to trace the history of the project, which is crucial for collaboration and code reviews.

### Squash and Merge

**Squash and Merge** combines all the changes from the feature branch into a single commit and then merges that commit into the main branch. This method creates a linear history by squashing multiple commits into one.

**Pros:**

- Produces a clean, linear history.
- Easier to revert changes if needed.
- Reduces the number of commits in the history.

**Cons:**

- Loses the detailed history of individual commits from the feature branch.
- Harder to trace the evolution of changes.

**Use Case:**
Squash and merge is useful for projects where a clean and linear history is preferred, and the detailed history of individual commits is not as important.

### Rebase and Merge

**Rebase and Merge** replays the changes from the feature branch onto the main branch. This process involves moving the entire feature branch to the tip of the main branch and applying the changes on top.

**Pros:**

- Maintains a linear history.
- Integrates changes as if they were developed on top of the main branch.
- Avoids merge commits, keeping history clean.

**Cons:**

- Can be risky if not done carefully, as it rewrites history.
- Potentially more complex and time-consuming conflict resolution.
- Can obscure the original context of changes.

**Use Case:**
Rebase and merge is suitable for projects where a linear history is essential and contributors are comfortable with potentially complex conflict resolution.
