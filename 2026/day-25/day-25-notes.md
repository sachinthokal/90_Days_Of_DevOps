# Day 25: Undoing Mistakes & Branching Strategies

## Task 1: Git Reset
### 1. Difference between --soft, --mixed, and --hard:
* **--soft**: Moves the HEAD pointer back to a previous commit, but leaves your files changed and **staged** (ready to be committed again).
* **--mixed (Default)**: Moves the HEAD back and **unstages** your changes. Your work is still in the folder, but you have to `git add` them again.
* **--hard**: Moves the HEAD back and **deletes all changes** in the staging area and working directory. Your files revert exactly to how they were at that commit.

### 2. Which one is destructive?
**--hard** is destructive. It permanently deletes any uncommitted work in your working directory. Use it with extreme caution.

### 3. Should you use reset on pushed commits?
**No.** Reset rewrites history. If you push a reset that deletes commits others have already pulled, it will cause major synchronization errors for the rest of the team.

## Task 2: Git Revert
### 1. How is revert different from reset?
Reset moves the timeline backward (deleting history), whereas **revert** moves the timeline forward by adding a *new* commit that does the opposite of the one you want to undo.

### 2. Why is revert safer?
Because it doesn't delete anything from the history. It is a "public-friendly" undo that plays nicely with shared branches and remote repositories.

## Task 3: Comparison Table

| Feature | git reset | git revert |
| :--- | :--- | :--- |
| **Action** | Removes commits from history | Adds a new "undo" commit |
| **Safe for Remotes?** | No (History mismatch) | Yes (Preserves history) |
| **Use Case** | Fixing local, unpushed typos | Undoing a bug in production |

## Task 4: Branching Strategies

### GitFlow
* **How it works**: Uses a `develop` branch for integration and a `main` branch for production, with specific side-branches for `features`, `releases`, and `hotfixes`.
* **Pros/Cons**: Very structured; great for large teams. However, it can be slow and complex.
* **Best for**: Large teams with scheduled, versioned releases (e.g., mobile apps).

### GitHub Flow
* **How it works**: A simple model where everything in `main` is deployable. Features are built on short-lived branches and merged via Pull Requests.
* **Pros/Cons**: Fast and simple. Not great for managing multiple versions of software at once.
* **Best for**: Startups and web services (CI/CD).

### Trunk-Based Development
* **How it works**: Developers push small, frequent updates to a single `main` branch (the "trunk").
* **Pros/Cons**: Extremely fast; avoids "merge hell." Requires high-quality automated testing.
* **Best for**: High-performing DevOps teams.

### Strategy Choice:
* **Startup shipping fast**: GitHub Flow.
* **Large team with scheduled releases**: GitFlow.
* **Favorite Open Source Project**: Most (e.g., Kubernetes or Linux) use a variation of Trunk-Based Development with strict code reviews.