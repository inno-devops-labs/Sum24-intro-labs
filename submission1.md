# DevOps Lab 1

## Task 1: SSH Commit Signature Verification

Benefits of signing commits include:

- **Integrity**: Signing commits help improve the integrity of the commits proving that the changes come from the expected source.
- **Identity Protection**: Since it is easy to [impersonate a user](https://mikegerwitz.com/papers/git-horror-story.html), signed commits can help identify commit forgeries.
- **Commit Policies**: GitHub and other distributed VCS support rules and policies to accept/reject signed and unsigned commits. This can increase the security of the codebase.

## Task 2: Merge Strategies in Git

### Summary of Git Merge Strategies

- **Standard Merge** produces a non-linear commit history with each merge resulting in a separate merge commit. It is simple, familiar, and maintains the full context of branches, ensuring every action is traceable without rewriting history. However, the history can become cluttered with merge commits, making it harder to read and identify specific features or bug fixes.

- **Squash and Merge** consolidates all commits from a feature branch into a single commit before merging. This simplifies the commit history, reducing noise and making it easier to follow. However, it loses the granularity of individual commits, which can make understanding the incremental development process more difficult.

- **Rebase and Merge** reapplies commits from a feature branch onto the base branch, resulting in a linear history without creating new merge commits. It streamlines complex history and allows squashing of intermediate commits, presenting work as a cohesive change. Nevertheless, rebasing rewrites history, which can be dangerous and requires force-pushing, complicating collaboration.

In collaborative environments, the standard merge strategy is often preferred due to its simplicity and transparency. It maintains the full history of commits, allowing team members to understand the evolution of the codebase, track down issues, and revert changes if necessary. While it can lead to a cluttered commit history, this is a worthwhile trade-off for the benefits of traceability and context retention. Implicit merge strategies like rebasing, though cleaner, introduce risks and complexities that can disrupt collaboration. Therefore, the standard merge strategy strikes a balance between simplicity, transparency, and collaboration efficiency.
