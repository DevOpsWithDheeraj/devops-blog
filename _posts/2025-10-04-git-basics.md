---
layout: post
title: "Git Basics for DevOps"
date: 2025-10-04
---

# Git Basics for DevOps

Git is the **most widely used version control system** and an essential tool for **DevOps engineers**. It allows you to **track changes, collaborate with teams, and manage project history** efficiently. Understanding Git is fundamental for **CI/CD pipelines, automated deployments, and infrastructure-as-code projects**.

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
# Set your name
`git config --global user.name "Dheeraj Singh"`

# Set your email
`git config --global user.email "sdheerajsingh2498@gmail.com"`

# Enable colored output for better readability
`git config --global color.ui auto`

# Verify your configuration
`git config --list`







