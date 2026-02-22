# The Ultimate Git Reference Sheet (Days 22-25)

## 1. Setup & Config
* `git init`: Initialize a new local repository.
* `git config --global user.name "Name"`: Set your identity.
* `git config --list`: Verify settings.

## 2. Basic Workflow
* `git status`: See the state of your project.
* `git add <file>`: Move changes to the Staging Area.
* `git commit -m "msg"`: Save changes to the Repository.
* `git log --oneline --graph`: View a clean history.
* `git diff`: See what has changed but isn't staged yet.

## 3. Branching & Remotes
* `git branch <name>`: Create a new branch.
* `git switch <name>`: Switch to a branch.
* `git push origin <branch>`: Send local commits to GitHub.
* `git pull origin <branch>`: Fetch and merge remote changes.
* `git clone <url>`: Download an existing repository.
* `git remote add origin <url>`: Connect local repo to remote.

## 4. Merging & Integration
* `git merge <branch>`: Combine branch into the current one.
* `git rebase <branch>`: Replay your commits on top of another branch.
* `git merge --squash <branch>`: Condense a branch into one commit.
* `git cherry-pick <hash>`: Grab one specific commit from another branch.

## 5. Stashing (Context Switching)
* `git stash`: Hide your "work in progress" changes.
* `git stash pop`: Bring stashed changes back and delete the stash.
* `git stash list`: View all hidden work.

## 6. Undoing Mistakes
* `git reset --soft HEAD~1`: Undo last commit, keep changes staged.
* `git reset --hard <hash>`: Wipe everything back to a specific point.
* `git revert <hash>`: Create a new commit that undoes a previous one.
* `git reflog`: The "God Mode" log that shows every action, even deleted ones.