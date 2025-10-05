---
layout: post
title: "Git Basics for DevOps"
date: 2025-10-04
---

# Git Basics for DevOps

Git is the **most widely used version control system** in the world. It allows developers and DevOps engineers to **track changes, collaborate on code, and manage project history** efficiently. In DevOps workflows, Git is essential for **CI/CD pipelines, automated deployments, and infrastructure-as-code projects**.

This post will take you from **Git basics to advanced usage**, including all useful commands and real-world best practices.

---

## 1. Why Git?

Version control systems (VCS) allow teams to:

- Track and revert code changes.
- Collaborate efficiently across multiple developers.
- Maintain a complete history of the project.
- Integrate seamlessly with **CI/CD pipelines**.

Git is **distributed**, meaning every developer has a **full repository**, enabling offline work and fast operations.

---

## 2. Installing Git

### Ubuntu
```bash
sudo apt update
sudo apt install git -y
git --version
