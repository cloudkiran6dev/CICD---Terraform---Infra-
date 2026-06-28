# Chapter 1 - Project Introduction

# Azure Infrastructure Deployment using Terraform and Azure DevOps (Classic Pipeline)

## Project Overview

This project demonstrates how to provision Microsoft Azure infrastructure using **Terraform** and automate the deployment using an **Azure DevOps Classic Pipeline**.

Instead of creating Azure resources manually through the Azure Portal, we define the entire infrastructure as code using Terraform. The Terraform code is stored in Azure Repos and automatically deployed through Azure DevOps CI/CD.

This project follows modern DevOps practices such as:

* Infrastructure as Code (IaC)
* Version Control
* Continuous Integration
* Continuous Deployment
* Automation
* Repeatable Infrastructure Deployment

By the end of this project, you will have deployed a complete Azure infrastructure consisting of:

* Azure Resource Group
* Virtual Network
* Public Subnet
* Private Subnet
* Network Security Group
* Network Interface
* Linux Virtual Machine

Everything will be deployed automatically through an Azure DevOps Pipeline.

---

# Project Objectives

The primary objectives of this project are:

* Learn Infrastructure as Code (IaC)
* Learn Terraform fundamentals
* Deploy Azure resources automatically
* Understand Azure DevOps Classic Pipelines
* Learn Git and Azure Repos
* Learn Azure Service Connections
* Build a production-style deployment pipeline
* Understand the Terraform deployment lifecycle
* Gain hands-on Azure DevOps experience

---

# What You Will Learn

After completing this project, you will understand:

### Terraform

* Provider Configuration
* Resource Blocks
* Dependencies
* Terraform Workflow
* Terraform State
* Terraform Lifecycle
* Infrastructure Provisioning

### Azure

* Resource Groups
* Virtual Networks
* Subnets
* Network Security Groups
* Network Interfaces
* Linux Virtual Machines

### Azure DevOps

* Azure Repos
* Classic Pipelines
* Hosted Agents
* Service Connections
* Pipeline Tasks
* Continuous Deployment

### Git

* Repository Initialization
* Git Commit
* Git Push
* Version Control

---

# Project Architecture

```
                        Developer
                            │
                            │
                     Write Terraform Code
                            │
                            ▼
                     Local Git Repository
                            │
                            │ git push
                            ▼
                      Azure Repos (Git)
                            │
                            ▼
                Azure DevOps Classic Pipeline
                            │
                            ▼
                 Microsoft Hosted Ubuntu Agent
                            │
        ┌───────────────────┼────────────────────┐
        │                   │                    │
        ▼                   ▼                    ▼
 Terraform Init      Terraform Validate   Terraform Plan
                            │
                            ▼
                    Terraform Apply
                            │
                            ▼
                     Azure Subscription
                            │
                            ▼
                Azure Resource Manager (ARM)
                            │
                            ▼
         Resource Group
                │
                ▼
         Virtual Network
                │
        ┌───────┴────────┐
        ▼                ▼
 Public Subnet     Private Subnet
        │                │
        └───────┬────────┘
                ▼
        Network Security Group
                │
                ▼
       Network Interface (NIC)
                │
                ▼
        Linux Virtual Machine
```

---

# Project Workflow

The project consists of the following stages.

```
Step 1
Write Terraform Code
        │
        ▼
Step 2
Store Code in Azure Repos
        │
        ▼
Step 3
Create Azure DevOps Pipeline
        │
        ▼
Step 4
Install Terraform
        │
        ▼
Step 5
Terraform Init
        │
        ▼
Step 6
Terraform Validate
        │
        ▼
Step 7
Terraform Plan
        │
        ▼
Step 8
Terraform Apply
        │
        ▼
Step 9
Azure Infrastructure Created
```

---

# Prerequisites

Before starting this project, ensure the following are available.

## Azure

* Active Azure Subscription
* Owner or Contributor access to the subscription

---

## Azure DevOps

* Azure DevOps Organization
* Azure DevOps Project
* Azure Repos Repository

---

## Local Machine

Install the following software:

* Git
* Visual Studio Code
* Terraform CLI
* Azure CLI (Optional but Recommended)

---

# Required Knowledge

Basic understanding of:

* Azure Portal
* Virtual Machines
* Networking
* Git Commands
* Terraform Basics
* Azure DevOps Basics

No advanced Terraform knowledge is required because every concept will be explained throughout the project.

---

# Software Used

| Software           | Purpose                |
| ------------------ | ---------------------- |
| Azure Portal       | Cloud Management       |
| Terraform          | Infrastructure as Code |
| Azure DevOps       | CI/CD                  |
| Azure Repos        | Git Repository         |
| Git                | Version Control        |
| Visual Studio Code | Code Editor            |

---

# Azure Resources Created

This project provisions the following resources.

| Resource               | Purpose                                |
| ---------------------- | -------------------------------------- |
| Resource Group         | Logical container for Azure resources  |
| Virtual Network        | Private Azure network                  |
| Public Subnet          | Hosts public-facing resources          |
| Private Subnet         | Hosts internal resources               |
| Network Security Group | Controls inbound and outbound traffic  |
| Network Interface      | Connects VM to the virtual network     |
| Linux Virtual Machine  | Ubuntu server deployed using Terraform |

---

# Why Terraform?

Traditionally, Azure resources are created manually using the Azure Portal.

Manual deployments become difficult because:

* Time consuming
* Human errors
* Difficult to reproduce
* No version control
* Difficult to audit

Terraform solves these problems by allowing infrastructure to be written as code.

Benefits include:

* Automated deployment
* Version-controlled infrastructure
* Repeatable deployments
* Easy rollback
* Team collaboration
* Consistent environments

---

# Why Azure DevOps?

Terraform alone can deploy infrastructure.

However, in enterprise environments, engineers rarely execute Terraform manually from their laptops.

Instead, organizations use Azure DevOps to:

* Store source code
* Automate deployments
* Enforce approvals
* Track deployment history
* Integrate with Git
* Enable Continuous Integration and Continuous Deployment (CI/CD)

This project demonstrates that enterprise deployment workflow.

---

# Expected Outcome

After completing this project, you will have:

* A complete Terraform project.
* Azure infrastructure deployed automatically.
* Terraform source code stored in Azure Repos.
* A working Azure DevOps Classic Pipeline.
* Practical experience with Infrastructure as Code.
* Hands-on experience with CI/CD automation.
* A portfolio-ready Azure DevOps project suitable for interviews.

---

# Project Roadmap

This guide is organized into the following chapters.

| Chapter    | Description                      |
| ---------- | -------------------------------- |
| Chapter 1  | Project Introduction             |
| Chapter 2  | Environment Setup                |
| Chapter 3  | Terraform Fundamentals           |
| Chapter 4  | Creating Azure Infrastructure    |
| Chapter 5  | Git and Azure Repos              |
| Chapter 6  | Azure DevOps Service Connections |
| Chapter 7  | Azure DevOps Classic Pipeline    |
| Chapter 8  | CI/CD Deployment                 |
| Chapter 9  | Troubleshooting                  |
| Chapter 10 | Best Practices                   |
| Chapter 11 | Interview Questions              |
| Chapter 12 | Future Enhancements              |

---

# End of Chapter 1

In the next chapter, we will prepare the development environment by installing Terraform, Git, Visual Studio Code, creating an Azure DevOps project, and setting up the Azure subscription required for the deployment.
