# Day 28 - Revision & Confidence Test

#### Revisited Weak Spots

### 1. Linux File Permissions

-   Understood r=4, w=2, x=1
-   755 = rwxr-xr-x
-   Difference between chmod +x and chmod 755
-   Practiced recursive permissions using chmod -R

### 2. Git Reset vs Revert

-   git reset rewrites history
-   git revert creates a new commit to undo changes
-   --hard deletes working directory changes
-   Avoid reset --hard on shared branches

### 3. Process & Port Debugging

-   Used ps -ef and grep to find processes
-   Used lsof -i :8080 to find port usage
-   Used netstat and ss commands
-   Killed processes using kill -9 PID

------------------------------------------------------------------------

## Task 3: Quick-Fire Answers
```bash

1. chmod 755 script.sh

# Owner: rwx (7) Group: r-x (5) Others: r-x (5)

2. Process vs Service

# Process: Running instance of a program Service: Background program
managed by system (starts at boot)

3. Find process using port 8080

# lsof -i :8080

4. set -euo pipefail

# -e → Exit on error -u → Error on undefined variable -o pipefail → Fail
if any command in pipeline fails

5. git reset --hard vs git revert

# reset --hard → Deletes history and working changes revert → Creates new commit to undo changes

6. Recommended Branching Strategy

# Feature branches → develop → main Lightweight Git Flow for weekly releases

7. git stash

# Temporarily saves uncommitted changes

8. Schedule script at 3 AM

# 0 3 \* \* \* /path/to/script.sh

9. git fetch vs git pull

# fetch → Download only pull → Download + merge

10. What is LVM?

# Logical Volume Manager Allows resizing storage dynamically and managing
disks flexibly

```

------------------------------------------------------------------------

## Task 5: Teach Back

### What is Git Branching?
```
Git branching allows developers to work on features independently
without affecting the main codebase. Each feature is developed in a
separate branch and merged once complete. This keeps production stable
and enables structured teamwork.
```