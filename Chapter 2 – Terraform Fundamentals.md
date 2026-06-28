# Chapter 2 - Terraform Fundamentals

# Introduction

Before deploying infrastructure to Microsoft Azure, it is important to understand the basic concepts of Terraform.

Terraform is an **Infrastructure as Code (IaC)** tool developed by **HashiCorp** that allows engineers to define, provision, update, and manage infrastructure using configuration files instead of manually creating resources through cloud portals.

Terraform supports multiple cloud providers such as:

* Microsoft Azure
* Amazon Web Services (AWS)
* Google Cloud Platform (GCP)
* Oracle Cloud
* VMware
* Kubernetes
* GitHub
* Docker

One of Terraform's biggest advantages is that the same language (HCL) is used across different cloud providers.

---

# What is Infrastructure as Code (IaC)?

Infrastructure as Code (IaC) is the practice of managing infrastructure through code rather than manually creating resources.

Instead of:

1. Logging into Azure Portal
2. Clicking "Create Resource"
3. Filling forms
4. Clicking Next
5. Reviewing
6. Creating resources

You simply write Terraform code:

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "Dev-RG01"
  location = "Central India"
}
```

Then execute:

```bash
terraform apply
```

Terraform creates the infrastructure automatically.

---

# Benefits of Infrastructure as Code

* Repeatable deployments
* Version control
* Automation
* Easy rollback
* Team collaboration
* Reduced human errors
* Faster deployments
* Standardized environments
* Auditability

---

# What is Terraform?

Terraform is an open-source Infrastructure as Code tool.

It allows you to:

* Create infrastructure
* Modify infrastructure
* Destroy infrastructure
* Import existing resources
* Manage multiple cloud providers

Terraform uses a declarative approach.

Instead of telling Terraform **how** to create resources, you tell it **what** infrastructure you want.

Terraform figures out **how** to build it.

---

# Terraform Architecture

```text
                   Terraform CLI
                         │
                         ▼
                Terraform Configuration
                    (*.tf files)
                         │
                         ▼
                Terraform Provider
                         │
                         ▼
                  Azure Resource Manager
                         │
                         ▼
                  Azure Infrastructure
```

---

# Terraform Workflow

Terraform always follows the same lifecycle.

```text
Write Code
     │
     ▼
terraform init
     │
     ▼
terraform validate
     │
     ▼
terraform plan
     │
     ▼
terraform apply
     │
     ▼
Azure Resources Created
```

---

# Terraform Configuration Files

Terraform stores infrastructure inside **.tf** files.

Example project:

```text
TerraformProject/
│
├── provider.tf
├── Resource_Group.tf
├── Virtual_Network.tf
├── Network_Security_Group.tf
├── Network_Interface.tf
├── Virtual_Machine.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
└── README.md
```

Terraform automatically loads every `.tf` file in the working directory.

There is no execution order based on file names.

Terraform builds a dependency graph internally.

---

# HashiCorp Configuration Language (HCL)

Terraform uses **HCL (HashiCorp Configuration Language)**.

Example:

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "Dev-RG01"
  location = "Central India"
}
```

HCL is:

* Human-readable
* Declarative
* Easy to learn
* Version controllable

---

# Terraform Block

Every Terraform project starts with a Terraform block.

Example:

```hcl
terraform {
  required_version = ">= 1.5"

  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~>4.0"
    }
  }
}
```

## Purpose

The Terraform block defines:

* Required Terraform version
* Required providers
* Backend configuration (optional)

---

# Provider Block

The provider tells Terraform which cloud platform to use.

Example:

```hcl
provider "azurerm" {
  features {}
}
```

Purpose:

* Connects Terraform to Azure.
* Enables Azure Resource Manager API.
* Manages Azure resources.

Without a provider, Terraform cannot communicate with Azure.

---

# Resource Block

A resource block defines infrastructure.

Syntax:

```hcl
resource "<RESOURCE_TYPE>" "<LOCAL_NAME>" {

}
```

Example:

```hcl
resource "azurerm_resource_group" "rg01" {
  name     = "Dev-RG01"
  location = "Central India"
}
```

Explanation:

| Part                   | Meaning              |
| ---------------------- | -------------------- |
| resource               | Terraform keyword    |
| azurerm_resource_group | Azure resource type  |
| rg01                   | Local Terraform name |
| name                   | Azure resource name  |
| location               | Azure region         |

---

# Resource Naming

Terraform resources have two names.

Example:

```hcl
resource "azurerm_virtual_network" "TestVnet01" {
  name = "Dev-VNet01"
}
```

| Name       | Purpose              |
| ---------- | -------------------- |
| TestVnet01 | Terraform local name |
| Dev-VNet01 | Azure resource name  |

Terraform references use the local name:

```hcl
azurerm_virtual_network.TestVnet01.id
```

Azure Portal displays:

```
Dev-VNet01
```

---

# Resource Dependencies

Resources often depend on one another.

Example:

```text
Resource Group
      │
      ▼
Virtual Network
      │
      ▼
Subnet
      │
      ▼
Network Interface
      │
      ▼
Virtual Machine
```

Terraform automatically detects dependencies through resource references.

Example:

```hcl
resource_group_name = azurerm_resource_group.TestRG01.name
```

Because the virtual network references the resource group, Terraform knows it must create the resource group first.

---

# Variables

Variables make Terraform code reusable.

Example:

```hcl
variable "location" {
  type = string
}
```

Used as:

```hcl
location = var.location
```

Benefits:

* Avoid hardcoding values
* Easier environment management
* Reusable code

---

# Outputs

Outputs display useful information after deployment.

Example:

```hcl
output "vm_private_ip" {
  value = azurerm_network_interface.nic01.private_ip_address
}
```

Outputs are useful for:

* IP addresses
* Resource IDs
* VM names
* Storage account names

---

# Terraform State

Terraform keeps track of infrastructure using a **state file**.

```
terraform.tfstate
```

Purpose:

* Tracks deployed resources
* Detects configuration drift
* Determines required changes
* Maps Terraform resources to Azure resources

Without the state file, Terraform cannot manage existing infrastructure.

---

# Terraform Lifecycle Commands

## terraform init

Purpose:

* Initialize the working directory.
* Download providers.
* Configure backend.

Example:

```bash
terraform init
```

---

## terraform validate

Purpose:

* Validate Terraform syntax.
* Verify configuration correctness.

Example:

```bash
terraform validate
```

---

## terraform plan

Purpose:

* Compare desired infrastructure with current state.
* Generate an execution plan.

Example:

```bash
terraform plan
```

Typical output:

```text
Plan:
6 to add
0 to change
0 to destroy
```

---

## terraform apply

Purpose:

* Execute the plan.
* Create or modify Azure resources.

Example:

```bash
terraform apply
```

To skip confirmation:

```bash
terraform apply -auto-approve
```

---

## terraform destroy

Purpose:

Delete all infrastructure managed by Terraform.

Example:

```bash
terraform destroy
```

---

# Common Terraform Commands

| Command              | Purpose                        |
| -------------------- | ------------------------------ |
| terraform init       | Initialize project             |
| terraform fmt        | Format Terraform code          |
| terraform validate   | Validate configuration         |
| terraform plan       | Preview infrastructure changes |
| terraform apply      | Deploy infrastructure          |
| terraform destroy    | Remove infrastructure          |
| terraform show       | Display current state          |
| terraform output     | Show output values             |
| terraform state list | List resources in state        |

---

# Terraform Best Practices

* Organize resources into separate `.tf` files.
* Use variables instead of hardcoded values.
* Never commit `terraform.tfstate`.
* Use `.gitignore` for sensitive files.
* Store state remotely in production.
* Use descriptive resource names.
* Keep code modular and reusable.
* Validate before applying changes.
* Review execution plans before deployment.

---

# Common Beginner Mistakes

* Forgetting to run `terraform init`.
* Hardcoding passwords or secrets.
* Committing `terraform.tfstate` to Git.
* Using incorrect Azure image SKUs.
* Incorrect resource references.
* Not using variables.
* Deleting the state file accidentally.
* Ignoring `terraform plan` output.

---

# Summary

In this chapter, you learned:

* What Infrastructure as Code (IaC) is.
* What Terraform is and why it is used.
* Terraform architecture and workflow.
* HCL syntax.
* Terraform blocks.
* Providers.
* Resources.
* Variables.
* Outputs.
* Terraform state.
* Terraform lifecycle commands.
* Best practices.
* Common beginner mistakes.

These concepts form the foundation for the rest of the project.

---

# What's Next?

In **Chapter 3 – Environment Setup**, we will prepare the development environment by:

* Installing Terraform.
* Installing Git.
* Installing Visual Studio Code.
* Configuring Azure CLI.
* Creating an Azure Subscription.
* Creating an Azure DevOps Project.
* Creating an Azure Repos repository.
* Verifying all required tools before writing the infrastructure code.

By the end of Chapter 3, your development environment will be fully configured and ready to build and deploy Azure infrastructure using Terraform and Azure DevOps.
