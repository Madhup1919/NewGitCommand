# Git Learning Notes - February 24, 2026

## Table of Contents
1. [Git Workflow Overview](#git-workflow-overview)
2. [The Three Git Areas](#the-three-git-areas)
3. [Essential Git Commands](#essential-git-commands)
4. [Common Workflows](#common-workflows)
5. [Authentication & Permissions](#authentication--permissions)
6. [Synchronization](#synchronization)

---

## Git Workflow Overview

Git is a distributed version control system that manages code changes across three main areas:
- **Local Working Directory** → Changes you make to files
- **Staging Area** → Files ready to be committed
- **Repository** → Permanent version history

The workflow follows: Working Directory → Staging Area → Local Repository → Remote Repository

---

## The Three Git Areas

### 1. Working Directory
- Your local file system where you edit code
- Most volatile state - changes here are NOT tracked by Git yet
- Only exists on your computer
- **When you modify a file**: It appears as "modified" in `git status`

### 2. Staging Area (Index/Cache)
- An intermediate holding area between working directory and repository
- Allows selective commits - you choose which changes to include
- Provides fine-grained control over what gets committed
- **Action**: `git add .` or `git add filename`
- **Benefit**: Can modify multiple files but commit only specific ones

### 3. Local Repository (`.git` folder)
- Your complete version history stored on your machine
- Contains all commits with unique SHA-1 hashes
- Each commit is permanent and immutable
- Forms the basis for collaboration
- **Action**: `git commit -m "message"`

### 4. Remote Repository (GitHub)
- Centralized server storing the shared code
- Accessible to all team members
- Single source of truth for the project
- **Action**: `git push origin branchname`

---

## Essential Git Commands

### Configuration
```bash
git config --global user.name "Your Name"      # Set global username
git config --global user.email "email@example.com"  # Set global email
```

### Syncing with Remote
```bash
git fetch --all              # Download all remote changes (safe - no merging)
git pull                     # Fetch + merge remote changes into current branch
git pull origin main         # Pull specific remote branch
```

### Staging & Committing
```bash
git add .                    # Stage all changes in working directory
git add filename             # Stage specific file
git commit -m "message"      # Create permanent snapshot with message
```

### Pushing Changes
```bash
git push origin branchname   # Send local commits to remote repository
```

### Checking Status
```bash
git status                   # Show current branch status and changes
git log                      # View commit history
git branch -vv               # Show all branches with tracking info
git remote -v                # Show remote repositories
```

---

## Common Workflows

### Workflow 1: Making & Pushing Changes
```bash
# 1. Make changes to files (in working directory)
# 2. Stage changes
git add .

# 3. Commit to local repository
git commit -m "Add new feature"

# 4. Push to remote repository
git push origin working
```

### Workflow 2: Pulling Latest Changes
```bash
# 1. Fetch all remote changes
git fetch --all

# 2. Pull and merge into current branch
git pull
```

### Workflow 3: Setting Up Branch Tracking
```bash
# Set current branch to track a remote branch
git branch --set-upstream-to=origin/main myworkingbranch

# Then use git pull without specifying branch
git pull
```

---

## Authentication & Permissions

### Common Issues

**Error**: `Permission denied to <username>. The requested URL returned error: 403`

**Cause**: 
- You're logged in as wrong GitHub user
- Credentials cached in Windows Credential Manager
- Don't have push access to the repository

### Solutions

#### Option 1: Update Credentials
```bash
# List stored credentials
cmdkey /list | Select-String "github"

# Delete old credentials
cmdkey /delete:LegacyGeneric:target=https://github.com/

# Next push will prompt for new credentials
git push origin branchname
```

#### Option 2: Use Personal Access Token
- Create token at: https://github.com/settings/tokens
- Use token instead of password when prompted

#### Option 3: Check Repository Access
- Ensure the repository owner has added you as a collaborator
- Verify you're using correct GitHub account credentials

---

## Synchronization

### Making Local & Remote in Sync

```bash
# Step 1: Fetch all updates from remote (safe operation)
git fetch --all
# Downloads latest information without modifying your files

# Step 2: Check current status
git status
# Shows if your branch is ahead/behind remote

# Step 3: Pull changes if needed
git pull
# Merges remote changes into your local branch

# Verify sync
git branch -vv
# Shows tracking relationship and sync status
```

### Checking Sync Status
```bash
git status
# Output: "Your branch is up to date with 'origin/main'"
# OR
# Output: "Your branch is ahead of 'origin/main' by X commits"
```

---

## Key Takeaways

✅ **Always fetch before pushing** - Ensures you have latest remote changes
✅ **Use staging area wisely** - Allows selective commits
✅ **Write meaningful commit messages** - Helps team understand changes
✅ **Keep credentials updated** - Prevents authentication errors
✅ **Check git status frequently** - Know where your changes are
✅ **Use `git pull` for sync** - Combines fetch and merge in one command

---

## Practice Commands Summary

| Action | Command |
|--------|---------|
| Check status | `git status` |
| Stage changes | `git add .` |
| Commit changes | `git commit -m "message"` |
| Push to remote | `git push origin branch` |
| Fetch updates | `git fetch --all` |
| Pull updates | `git pull` |
| View branches | `git branch -vv` |
| Check remotes | `git remote -v` |

---

## Resources
- [Git Documentation](https://git-scm.com/doc)
- [GitHub Help](https://docs.github.com/)
- [Git Branching Model](https://nvie.com/posts/a-successful-git-branching-model/)

---

**Last Updated**: February 24, 2026
