## Advanced Integration
* **`git merge <branch>`**: Combines changes from another branch into the current one.
    * Example: `git merge feature-login`
* **`git merge --squash <branch>`**: Condenses all branch commits into one single commit before merging.
    * Example: `git merge --squash feature-profile`
* **`git rebase <branch>`**: Moves the entire feature branch so it begins on the tip of the specified branch.
    * Example: `git rebase main`
* **`git cherry-pick <hash>`**: Applies the changes from a specific commit ID to your current branch.
    * Example: `git cherry-pick a1b2c3d4`

## Stashing & Context Switching
* **`git stash`**: Temporarily stores modified, tracked files to give you a clean working directory.
    * Example: `git stash`
* **`git stash list`**: Shows all your saved stashes.
* **`git stash pop`**: Restores the most recent stash and removes it from the list.
* **`git stash apply stash@{n}`**: Restores a specific stash from the list without deleting it.

## Visualization
* **`git log --oneline --graph --all`**: Displays a visual "tree" of your branches and how they connect.