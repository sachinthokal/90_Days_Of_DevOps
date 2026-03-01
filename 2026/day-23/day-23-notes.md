# Day 23: Git Branching & GitHub Notes

## Task 1: Understanding Branches

### 1. What is a branch in Git?
A branch is a lightweight, movable pointer to a specific commit. It represents an independent line of development, allowing you to diverge from the main project to work on features or fixes without affecting the "stable" code.

### 2. Why do we use branches instead of committing everything to main?
Using branches keeps the `main` branch clean and deployable at all times. It allows for "Isolated Development," meaning you can experiment, break things, and fix them in a feature branch without disrupting your teammates or the production environment.

### 3. What is HEAD in Git?
`HEAD` is a symbolic reference (a pointer) to the branch you are currently working on. Think of it as the "active" marker. When you switch branches, `HEAD` moves to the latest commit of that new branch.

### 4. What happens to your files when you switch branches?
Git updates your **Working Directory** to match the snapshot of the branch you switched to. Files that only exist on your other branch will disappear, and files specific to the current branch will appear or change.

---

## Task 3 & 4: GitHub & Remotes

### What is the difference between origin and upstream?
* **origin**: The default name for *your* fork or the remote repository you cloned. It’s where you have write access.
* **upstream**: Generally refers to the original "source" repository from which you forked. You usually pull updates from `upstream` to keep your fork current.

### What is the difference between git fetch and git pull?
* **git fetch**: Downloads the latest changes/metadata from the remote repository but **does not** merge them into your local files. It just lets you see what others have done.
* **git pull**: A combination of `git fetch` and `git merge`. It downloads the changes and immediately attempts to integrate them into your current local branch.

---

## Task 5: Clone vs Fork

### What is the difference between clone and fork?
* **Fork**: A GitHub-level action that creates a copy of someone else's repository under your own GitHub account.
* **Clone**: A Git-level action that downloads a repository (your own or someone else's) to your local machine.

### When would you clone vs fork?
* **Clone**: When you want to work on a project you already have access to on your local computer.
* **Fork**: When you want to contribute to an open-source project or use someone else's code as a starting point for your own project where you don't have direct write permissions.

### How do you keep your fork in sync?
You add the original repository as a remote named `upstream`, fetch the changes, and merge them:
1. `git remote add upstream <original-repo-url>`
2. `git fetch upstream`
3. `git merge upstream/main`.