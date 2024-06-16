# Lab 1: Introduction to DevOps with Git
## Anton Buguev, a.buguev@innopolis.university, M23-RO-01

### Task 1. The benefits of signing commits:

Commit signing is neccessary to verify that the person who is really working on the project made the commit. It is possible to use other person name and email to commit some changes. However, signatures allow to see that this commit has not come from trusted source.

### Task 2. Merge Strategies:

1. **Standart merge**: simply combines branches together keeping history of each commit of each branch.
    - **Advantages**: 
        - Stored history: allows to see all changes and trace them back in case of conflicts or errors.
    - **Disadvantages**: 
        - *Feature* branch may have large number of small commits that can actually complicate the trace process.
        - resolving conflicts may be complex if branches diverged significantly.

2. **Squash and Merge:**: merges all commits from *feature* branch into single commit (without keeping the history) and then merges branches.
    - **Advantages**: 
        - Single commit summarizes the main reason of that branch, *e.g.* bug fix or new feature.
        - Since history of commits of *feature* branch is not preserved, the main commit history is much cleaner.
    -  **Disadvantages**:
        - Since history is not stored, it makes much harder to trace back the errors.

3. **Rebase and Merge**: applies commits of the *feature* branch to the main branch as if they were applied directly and like *feature* branch never existed.
    - **Advantages**: 
        - The whole history of changes is linear that may be easier to understand the process.
    -  **Disadvantages**:
        - Rebase conflicts may be hard to resolve compared to standard merging.

#### Conclusion

Concluding we can say that **Standard Merge** may be the best option compared to others mainly because this method stores the whole history of changes of all branches that may be crucial since in case of some conflicts developers will be able to trace back the error and fix it.