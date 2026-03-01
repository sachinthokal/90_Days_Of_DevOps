# Day 26: GitHub CLI (gh) & Automation

## Task 1: Authentication
### 1. What authentication methods does `gh` support?
The GitHub CLI supports three primary methods:
* **Web Browser:** The most common method, which opens your default browser to authorize the app.
* **Personal Access Tokens (PAT):** Used primarily for headless environments or servers where a browser isn't available.
* **SSH Keys:** Used for secure, key-based authentication for git operations.

## Task 3: Issue Automation
### 2. How could you use `gh issue` in a script?
`gh issue` is incredibly powerful for automation. For example:
* **Failure Reporting:** A script can monitor a server or a CI build; if a failure occurs, it can automatically run `gh issue create` with the error logs in the body.
* **Bulk Management:** You could write a loop to close all issues labeled "stale" or "obsolete" across multiple repositories at once.

## Task 4: Pull Requests
### 1. What merge methods does `gh pr merge` support?
It supports all standard GitHub merge strategies:
* **--merge**: Create a traditional merge commit.
* **--rebase**: Rebase the commits onto the destination branch.
* **--squash**: Combine all PR commits into one single commit.

### 2. How would you review someone else's PR?
First, run `gh pr list` to find the PR number. Then:
1. `gh pr checkout <number>` to bring their code to your local machine for testing.
2. `gh pr diff` to see the changes in your terminal.
3. `gh pr review --approve` or `gh pr review --comment -b "Nice work!"` to submit your feedback.

## Task 5: GitHub Actions & CI/CD
### 1. Utility of `gh run` and `gh workflow`:
In a CI/CD pipeline, these commands allow you to:
* **Triggering:** Use `gh workflow run` to manually kick off a deployment script.
* **Monitoring:** Use `gh run watch` in a terminal window to see the real-time progress of a build without refreshing a browser page.
* **Logging:** Use `gh run view --log` to fetch failure logs directly into your terminal for quick debugging