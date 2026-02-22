# Git Commands Reference

A collection of essential Git commands used during the DevOps journey.

## Setup & Config
* **`git init`**: Initializes a new local Git repository in the current folder.
    * Example: `git init`
* **`git config`**: Configures user information like name and email for commits.
    * Example: `git config --global user.name "Your Name"`

## Basic Workflow
* **`git status`**: Shows the state of the working directory and the staging area (untracked, modified, or staged files).
    * Example: `git status`
* **`git add`**: Adds a change in the working directory to the staging area.
    * Example: `git add git-commands.md`
* **`git commit`**: Saves the staged snapshot to the project history with a descriptive message.
    * Example: `git commit -m "Add initial documentation"`

## Viewing Changes
* **`git log`**: Displays the history of all commits made in the repository.
    * Example: `git log --oneline`
* **`git diff`**: Shows the specific line-by-line changes made to files that are not yet staged.
    * Example: `git diff`