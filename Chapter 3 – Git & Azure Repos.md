# Chapter 3 – Git & Azure Repos

## Introduction

Version control is an essential part of modern software development and DevOps. Before deploying infrastructure using Terraform, we need a reliable way to store, track, and collaborate on our Infrastructure as Code (IaC).

In this chapter, you will learn how to:

* Understand Git and Version Control
* Install Git
* Configure Git
* Create an Azure DevOps Project
* Create an Azure Repos Repository
* Initialize a local Git repository
* Connect the local repository to Azure Repos
* Push Terraform code into Azure Repos
* Understand the Git workflow used in real-world DevOps projects

---

# What is Version Control?

Version Control is a system that records changes to files over time, allowing developers to:

* Track changes
* Restore previous versions
* Collaborate with team members
* Review history
* Resolve conflicts
* Maintain a single source of truth

Without version control, every change is permanent and difficult to track.

---

# Why Git?

Git is the most widely used distributed version control system.

### Benefits

* Open Source
* Distributed Architecture
* Fast Performance
* Easy Branching and Merging
* Supports Team Collaboration
* Integrates with Azure DevOps, GitHub, GitLab and Bitbucket

In this project, Git is used to manage the Terraform source code.

---

# Why Azure Repos?

Azure Repos is Microsoft's Git repository service within Azure DevOps.

It provides:

* Unlimited private Git repositories
* Branch management
* Pull Requests
* Code Reviews
* Repository permissions
* Integration with Azure Pipelines

Azure Repos acts as the central repository where our Terraform code is stored.

---

# Project Architecture

```text
Developer
     │
     ▼
Local Git Repository
     │
     │ git push
     ▼
Azure Repos
     │
     ▼
Azure DevOps Pipeline
     │
     ▼
Terraform Deployment
     │
     ▼
Azure Infrastructure
```

---

# Prerequisites

Before proceeding, ensure you have:

* Azure Subscription
* Azure DevOps Organization
* Azure DevOps Project
* Git installed
* Visual Studio Code installed
* Terraform project files created

---

# Step 1 – Install Git

Download Git from:

```text
https://git-scm.com/downloads
```

Verify the installation:

```bash
git --version
```

Example output:

```text
git version 2.50.1
```

---

# Step 2 – Configure Git

Configure your Git username:

```bash
git config --global user.name "Kiran Kumar"
```

Configure your email address:

```bash
git config --global user.email "your-email@example.com"
```

Verify the configuration:

```bash
git config --list
```

Expected output:

```text
user.name=Kiran Kumar
user.email=your-email@example.com
```

---

# Step 3 – Create an Azure DevOps Project

1. Sign in to Azure DevOps.
2. Click **New Project**.
3. Enter the following details:

| Property     | Value          |
| ------------ | -------------- |
| Project Name | Terraform-Demo |
| Visibility   | Private        |

4. Click **Create**.

Azure DevOps automatically provisions:

* Azure Repos
* Azure Pipelines
* Azure Boards
* Azure Artifacts
* Test Plans

---

# Step 4 – Create an Azure Repos Repository

1. Navigate to **Repos**.
2. Create a new Git repository.
3. Name the repository:

```text
Terraform-Azure-Infrastructure
```

You will receive a repository URL similar to:

```text
https://<organization>@dev.azure.com/<organization>/<project>/_git/Terraform-Azure-Infrastructure
```

Save this URL for the next steps.

---

# Step 5 – Organize the Terraform Project

The project directory should look like:

```text
Terraform-Azure-Infrastructure/
│
├── provider.tf
├── Resource_Group.tf
├── Virtual_Network.tf
├── Network_Security_Group.tf
├── Network_Interface.tf
├── Virtual_Machine.tf
├── variables.tf
├── outputs.tf
├── .gitignore
└── README.md
```

Keeping resources separated into logical files makes the project easier to maintain.

---

# Step 6 – Create a .gitignore File

Create a file named:

```text
.gitignore
```

Add the following content:

```gitignore
# Terraform
.terraform/
*.tfstate
*.tfstate.*
crash.log

# Variable files
*.tfvars
*.tfvars.json

# Terraform plan files
*.tfplan

# Lock file
.terraform.lock.hcl

# VS Code
.vscode/

# OS files
.DS_Store
Thumbs.db
```

## Why use .gitignore?

The `.gitignore` file prevents unnecessary and sensitive files from being committed to the repository.

Examples include:

* Terraform state files
* Provider cache
* Local IDE settings
* Operating system files

---

# Step 7 – Initialize the Local Git Repository

Navigate to the project directory:

```bash
cd Terraform-Azure-Infrastructure
```

Initialize Git:

```bash
git init
```

Expected output:

```text
Initialized empty Git repository
```

This creates a hidden `.git` folder that stores all version history.

---

# Step 8 – Check Repository Status

Run:

```bash
git status
```

Example:

```text
On branch main

No commits yet

Untracked files:

provider.tf
Virtual_Machine.tf
Virtual_Network.tf
```

Git is now aware of your project but has not started tracking the files.

---

# Step 9 – Stage Files

Stage every file:

```bash
git add .
```

Verify:

```bash
git status
```

Example:

```text
Changes to be committed:

provider.tf
Virtual_Machine.tf
Virtual_Network.tf
```

Staging prepares files for committing.

---

# Step 10 – Commit the Changes

Create the first commit:

```bash
git commit -m "Initial Terraform Infrastructure"
```

Example:

```text
[main (root-commit)] Initial Terraform Infrastructure
```

A commit creates a permanent snapshot of the project.

---

# Step 11 – Add Azure Repos as the Remote Repository

Verify existing remotes:

```bash
git remote -v
```

If no remote exists, add one:

```bash
git remote add origin https://<organization>@dev.azure.com/<organization>/<project>/_git/Terraform-Azure-Infrastructure
```

Verify:

```bash
git remote -v
```

Expected output:

```text
origin https://<organization>@dev.azure.com/<organization>/<project>/_git/Terraform-Azure-Infrastructure (fetch)
origin https://<organization>@dev.azure.com/<organization>/<project>/_git/Terraform-Azure-Infrastructure (push)
```

---

# Step 12 – Rename the Branch (Optional)

Rename the default branch:

```bash
git branch -M main
```

---

# Step 13 – Push the Code to Azure Repos

Push the repository:

```bash
git push -u origin main
```

Expected output:

```text
Enumerating objects...
Counting objects...
Writing objects...
To https://...
```

Future pushes only require:

```bash
git push
```

---

# Step 14 – Verify the Repository

Navigate to:

```
Azure DevOps
    └── Repos
          └── Files
```

You should see:

```text
provider.tf
Resource_Group.tf
Virtual_Network.tf
Network_Security_Group.tf
Network_Interface.tf
Virtual_Machine.tf
.gitignore
README.md
```

Your Terraform project is now stored in Azure Repos.

---

# Daily Git Workflow

Every time you make changes, follow this workflow:

```bash
git status
git add .
git commit -m "Describe your changes"
git push
```

This ensures your latest Terraform code is safely stored and ready for deployment.

---

# Git Workflow Diagram

```text
Developer
     │
     ▼
Modify Terraform Files
     │
     ▼
git status
     │
     ▼
git add .
     │
     ▼
git commit
     │
     ▼
git push
     │
     ▼
Azure Repos
     │
     ▼
Azure DevOps Pipeline
```

---

# Common Git Commands

| Command                       | Description                                 |
| ----------------------------- | ------------------------------------------- |
| `git init`                    | Initialize a repository                     |
| `git status`                  | Check repository status                     |
| `git add .`                   | Stage all files                             |
| `git commit -m "message"`     | Create a commit                             |
| `git remote -v`               | View configured remotes                     |
| `git remote add origin <URL>` | Add a remote repository                     |
| `git branch -M main`          | Rename the branch to main                   |
| `git push -u origin main`     | Push the initial commit                     |
| `git pull`                    | Download changes from the remote repository |
| `git log`                     | View commit history                         |

---

# Best Practices

* Commit changes frequently with meaningful commit messages.
* Never commit passwords or secrets.
* Never commit `terraform.tfstate`.
* Always use a `.gitignore` file.
* Keep the `main` branch stable.
* Pull the latest changes before starting new work.

---

# Common Issues

## Remote Already Exists

```text
error: remote origin already exists
```

Solution:

```bash
git remote remove origin
git remote add origin <repository-url>
```

---

## Authentication Failed

Verify:

* Repository URL
* Azure DevOps permissions
* Personal Access Token (if required)

---

## Nothing to Commit

```text
nothing to commit, working tree clean
```

This means there are no new changes to commit.

---

## Push Rejected

```text
Updates were rejected because the remote contains work that you do not have locally.
```

Solution:

```bash
git pull origin main
```

Resolve conflicts if necessary, then:

```bash
git push
```

---

# Summary

In this chapter, you learned how to:

* Understand Git and Version Control
* Configure Git
* Create an Azure DevOps project
* Create an Azure Repos repository
* Initialize a local Git repository
* Stage and commit files
* Connect to Azure Repos
* Push Terraform code
* Follow a standard Git workflow

At this point, your Terraform project is safely stored in Azure Repos and is ready to be consumed by an Azure DevOps pipeline.

---

# What's Next?

In **Chapter 4 – Azure DevOps Service Connection**, you will learn how to:

* Create an Azure Resource Manager Service Connection
* Authenticate Azure DevOps with Azure
* Understand Service Principals
* Configure secure access for Terraform deployments
* Prepare Azure DevOps to deploy infrastructure automatically
