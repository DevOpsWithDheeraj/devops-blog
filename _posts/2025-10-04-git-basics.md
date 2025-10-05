---
layout: post
title: "Git Basics for DevOps"
date: 2025-10-04
---

Git is the **most widely used version control system** and an essential tool for **DevOps engineers**. It allows you to **track changes, collaborate with teams, and manage project history** efficiently. 

Understanding Git is fundamental for **CI/CD pipelines, automated deployments, and infrastructure-as-code projects**.

This guide takes you from **basic Git concepts to advanced commands**, including a complete list of **useful commands for daily DevOps tasks**.

---

## 1. Why Git?

Git provides:

- **Version control**: Track and revert code changes.
- **Collaboration**: Multiple developers can work on the same project.
- **History**: Full history of code evolution.
- **Integration with CI/CD**: Automate builds, tests, and deployments.

Git is **distributed**, so every developer has a full repository locally, enabling **offline work** and **faster operations**.

---

## 2. Git Installation

### Ubuntu
```bash
sudo apt update
sudo apt install git -y
git --version
```

## 3. Git Configuration
```
git config --global user.name "Dheeraj Singh"
git config --global user.email "sdheerajsingh2498@gmail.com"
git config --global color.ui auto
git config --list
```

## 4. Basic Git Workflow
### Initialize Repository
```
git init
```     
### Clone Repository
```
git clone https://github.com/DevOpsWithDheeraj/myproject.git
```
### Check Status
```
git status
```
### Stage and Commit Changes
```
git add filename.txt       # Stage a file
git add .                  # Stage all files
git commit -m "Add initial project structure"
```
### Push and Pull
```
git push origin main       # Push commits to remote
git pull origin main       # Fetch and merge remote changes
```
## 5. Branching & Merging
### Create & Switch Branch
```
git checkout -b feature-login
```
### Switch to Existing Branch
```
git checkout main
```
### Merge Branch
```
git merge feature-login
```
### Delete Branch
```
git branch -d feature-login
```
## 6. Working with Remotes
```
git remote add origin <repo-url>   # Add remote repository
git remote -v                       # View remote repos
git fetch origin                     # Fetch remote changes without merging
git pull origin main                 # Pull and merge changes
git push origin feature-login        # Push branch to remote
```
## 7. Inspecting History & Changes
```
git log                               # View full commit history
git log --oneline                     # Compact view
git log --graph --all --decorate      # Visual graph
git diff                               # Show unstaged changes
git diff --staged                      # Show staged changes
git show <commit_id>                   # Show details of a specific commit
```
## 8. Undo & Reset
```
git restore filename.txt               # Discard unstaged changes
git restore --staged filename.txt     # Unstage staged file
git revert <commit_id>                # Revert specific commit
git reset --soft <commit_id>          # Move HEAD, keep staged changes
git reset --hard <commit_id>          # Move HEAD, discard changes
```
## 9. Stashing
```
git stash                             # Temporarily save changes
git stash list                        # List stashed changes
git stash pop                         # Apply and remove stash
git stash apply <stash_id>            # Apply stash without removing
```
## 10. Tags & Releases
```
git tag                               # List tags
git tag v1.0                           # Lightweight tag
git tag -a v1.0 -m "Release version 1.0"  # Annotated tag
git push origin v1.0                   # Push a specific tag
git push origin --tags                 # Push all tags
```
## 11. Git Collaboration Workflow (DevOps Style)
1. Clone repository or fork project.
2. Create a feature branch.
3. Make commits locally.
4. Push branch to remote.
5. Open a Pull Request (PR).
6. Code review and merge into main branch.
7. CI/CD pipelines automatically trigger builds, tests, and deployments.

This ensures safe collaboration, isolated development, and automation.

## 12. Advanced Commands & Tips
```
# Rename branch
git branch -m old-name new-name

# Show remote branch info
git branch -r

# Cherry-pick a commit
git cherry-pick <commit_id>

# Rebase current branch onto another
git rebase main

# Squash commits during rebase
git rebase -i HEAD~3

# Check differences between branches
git diff main feature-login

# Delete remote branch
git push origin --delete feature-login
```

## 13. All Useful Git Commands Cheat Sheet
```
| Command                             | Description                   |
| ----------------------------------- | ----------------------------- |
| `git init`                          | Initialize a new repo         |
| `git clone <repo>`                  | Clone remote repo             |
| `git status`                        | Show repo status              |
| `git add <file>`                    | Stage changes                 |
| `git add .`                         | Stage all files               |
| `git commit -m "msg"`               | Commit staged changes         |
| `git push origin <branch>`          | Push changes to remote        |
| `git pull origin <branch>`          | Pull and merge remote changes |
| `git checkout -b <branch>`          | Create & switch branch        |
| `git checkout <branch>`             | Switch branch                 |
| `git merge <branch>`                | Merge branch                  |
| `git branch -d <branch>`            | Delete branch                 |
| `git log`                           | Show commit history           |
| `git log --oneline`                 | Compact history               |
| `git log --graph --all --decorate`  | Graphical history             |
| `git diff`                          | Show unstaged changes         |
| `git diff --staged`                 | Show staged changes           |
| `git restore <file>`                | Discard changes               |
| `git restore --staged <file>`       | Unstage file                  |
| `git reset --soft <commit>`         | Soft reset                    |
| `git reset --hard <commit>`         | Hard reset                    |
| `git stash`                         | Temporarily save changes      |
| `git stash pop`                     | Apply stashed changes         |
| `git tag`                           | List tags                     |
| `git tag -a v1.0 -m "msg"`          | Annotated tag                 |
| `git push origin --tags`            | Push all tags                 |
| `git fetch origin`                  | Fetch remote changes          |
| `git cherry-pick <commit>`          | Apply specific commit         |
| `git rebase <branch>`               | Rebase branch                 |
| `git branch -m old new`             | Rename branch                 |
| `git push origin --delete <branch>` | Delete remote branch          |
```








