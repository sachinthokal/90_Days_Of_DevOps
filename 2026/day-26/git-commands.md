## GitHub CLI (gh) Power Tools
### Auth & Setup
* `gh auth login`: Start the interactive authentication process.
* `gh auth status`: Verify which account is currently logged in.

### Repository Operations
* `gh repo create <name> --public`: Create a new repo on GitHub from the CLI.
* `gh repo clone <owner/repo>`: An optimized version of git clone for GitHub repos.
* `gh repo view --web`: Instantly open the current repository in your browser.
* `gh repo delete <repo>`: Delete a repository (requires confirmation).

### Issues & Pull Requests
* `gh issue create --title "Title" --body "Body"`: Open an issue without leaving the terminal.
* `gh issue list --label "bug"`: Filter and view issues by labels.
* `gh pr create --fill`: Open a PR using the last commit info for the title/body.
* `gh pr status`: Get a quick summary of your active PRs and their CI status.
* `gh pr merge --squash`: Merge the current PR and clean up the history.

### Gists & API
* `gh gist create <file>`: Create a GitHub Gist from a local file.
* `gh api <endpoint>`: Make raw GitHub API calls (useful for advanced scripting).
* `gh alias set <nickname> <command>`: Create custom shortcuts for long commands.

### GitHub Actions
* `gh run list`: Show the status of recent workflow runs.
* `gh run watch`: Watch a specific workflow run until it finishes.