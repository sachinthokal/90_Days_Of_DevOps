# Day 24: Advanced Git Workflows

## Task 1: Merging Logic
### 1. What is a fast-forward merge?
A fast-forward merge occurs when the `main` branch hasn't changed since you created your feature branch. Git simply moves the `main` pointer forward to the latest commit on your feature branch. No "merge commit" is created.

### 2. When does Git create a merge commit instead?
If `main` has moved forward (received new commits) while you were working on your feature branch, Git must perform a **three-way merge**. This creates a new "Merge Commit" that ties the two histories together.

### 3. What is a merge conflict?
A conflict happens when Git cannot automatically decide which changes to keep—usually because the same line in the same file was modified differently in both branches. You must manually edit the file to resolve it.

---

## Task 2: Rebase vs. Merge
### 1. What does rebase actually do?
Rebase takes all the commits from your feature branch, "lifts" them up, and re-replays them one by one on top of the latest commit of the `main` branch. 

### 2. How is the history different?
* **Merge:** Shows a non-linear history with "train tracks" where branches diverge and join back. It preserves the exact historical context.
* **Rebase:** Creates a perfectly linear, straight-line history. It looks as if you developed the feature starting from the very latest version of `main`.

### 3. The Golden Rule: Why never rebase shared commits?
Rebasing **rewrites history** (it creates new commit IDs). If you rebase commits that others have already pulled, their local history will no longer match the remote, leading to a massive mess of duplicate commits and broken repos.

---

## Task 3: Squash Merging
### 1. What does squash merging do?
It takes all the commits from a feature branch (e.g., 10 "work in progress" commits) and condenses them into a single, clean commit on the `main` branch.

### 2. Trade-offs:
* **Pro:** Keeps the `main` history extremely clean and high-level.
* **Con:** You lose the granular history of *how* the feature was built (the individual steps and trial-and-error).

---

## Task 4: Git Stash
### 1. `pop` vs. `apply`:
* **`git stash pop`**: Applies the most recent stash and **removes** it from the stash list.
* **`git stash apply`**: Applies the stash but **keeps** it in the list for future use.

### 2. Real-world usage:
Use stash when you are halfway through a feature and a "hotfix" emergency comes in. You can't commit half-broken code, so you stash it, fix the bug on another branch, then come back and "pop" your work back into existence.

---

## Task 5: Cherry Picking
### 1. What is it?
Cherry-picking allows you to grab a **single commit** from one branch and apply it to another, without merging the entire branch.

### 2. Use case:
If you accidentally fixed a critical bug on a "experimental" branch that isn't ready for release yet, you can cherry-pick just that bug-fix commit into `main`.