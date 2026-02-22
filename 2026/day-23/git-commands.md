## Branching & Switching
* **`git branch`**: Lists all local branches in the repository.
    * Example: `git branch`
* **`git branch <name>`**: Creates a new branch at the current commit.
    * Example: `git branch feature-1`
* **`git checkout -b <name>`**: Creates a new branch and switches to it immediately.
    * Example: `git checkout -b feature-2`
* **`git switch <name>`**: The modern, dedicated command for switching branches.
    * Example: `git switch main`
    * *Note: Unlike `checkout`, `switch` only handles branches and doesn't risk accidentally overwriting files.*
* **`git branch -d <name>`**: Deletes a branch that has been merged.
    * Example: `git branch -d old-feature`

## Working with Remotes (GitHub)
* **`git remote add origin <url>`**: Connects your local repository to a remote server.
    * Example: `git remote add origin https://github.com/user/repo.git`
* **`git push -u origin <branch>`**: Uploads local branch commits to the remote and sets it as the default tracking branch.
    * Example: `git push -u origin main`
* **`git pull`**: Fetches changes from the remote and merges them into the current branch.
    * Example: `git pull origin main`
* **`git fetch`**: Downloads updates from the remote without changing local files.
    * Example: `git fetch origin`