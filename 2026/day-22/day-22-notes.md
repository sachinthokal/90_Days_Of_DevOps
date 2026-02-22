# Day 22: Git Fundamentals Notes

## Git Workflow Questions

### 1. What is the difference between `git add` and `git commit`?
`git add` moves changes from the working directory to the **staging area**, essentially marking them to be included in the next "snapshot." `git commit` takes everything in the staging area and permanently records it into the **repository history**.

### 2. What does the staging area do? Why doesn't Git just commit directly?
The staging area (or "Index") acts as a buffer. It allows you to be selective. If you have worked on three different features at once, you can stage and commit them one by one to keep your history clean and organized, rather than committing everything in one messy pile.

### 3. What information does `git log` show you?
`git log` provides a chronological list of commits. Each entry includes:
* **Commit Hash:** A unique 40-character ID (SHA-1).
* **Author:** Name and email of the person who made the change.
* **Date:** When the commit was created.
* **Message:** The description of what was changed.

### 4. What is the `.git/` folder and what happens if you delete it?
The `.git/` folder is the "brain" of the repository. It contains all the metadata, history, branches, and configuration. If you delete it, the project is no longer a Git repo; you lose all your version history and your ability to revert to previous states.

### 5. What is the difference between a working directory, staging area, and repository?
* **Working Directory:** The actual files you see and edit on your computer.
* **Staging Area:** A hidden file that lists what changes are prepared for the next commit.
* **Repository:** The permanent database (inside `.git/`) that stores all versions of your project.