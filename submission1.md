# Week 1 - Lab 1.
## Task 1.

### Benefits of signing commits
Commits can be signed locally to give confidence about origin of the made change, as you as well as the others can verify the integrity, authenticity, and origin of the code changes.
For individual users, GPG or SSH is considered as the best choices for signing commits.

## Task 2
### Standard Merge

Standard merge integrates the entire history of one branch into another, including all the individual commits from the feature branch. This strategy retains the commit history from the feature branch.

### Squash and Merge

Squash and Merge retains the changes but omits the individual commits from history. It combines all the commits on a single feature into a single commit on the master branch.

### Rebase and Merge

Rebase and Merge moves the entire branch and rewrites the history to reflect this. It incorporates all the new commits in the master branch, making it suitable for updating a feature branch that is not shared with others.

### Comparison
Standard merge retains the commit history from the feature branch, squash and merge combines all commits into a single commit, and rebase and merge moves the entire branch and rewrites the history to reflect this.