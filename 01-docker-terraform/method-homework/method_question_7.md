# Terraform Workflow Method

This document explains the standard workflow for managing infrastructure using Terraform, specifically addressing Question 7 of the Module 1 Homework.

## ❓ Question

Which of the following sequences, respectively, describes the workflow for:
1.  Downloading the provider plugins and setting up backend,
2.  Generating proposed changes and auto-executing the plan,
3.  Remove all resources managed by terraform.

### Options
- `terraform import, terraform apply -y, terraform destroy`
- `terraform init, terraform plan -auto-apply, terraform rm`
- `terraform init, terraform run -auto-approve, terraform destroy`
- **`terraform init, terraform apply -auto-approve, terraform destroy`**
- `terraform import, terraform apply -y, terraform rm`

---

## ✅ Answer

The correct sequence is: **`terraform init`, `terraform apply -auto-approve`, `terraform destroy`**

---

## 💡 Reason and Method

### 1. `terraform init` (Initialization)
This is the first command that should be run after writing a new Terraform configuration.
- **Function**: It initializes a working directory containing Terraform configuration files.
- **Actions**: It downloads and installs the necessary **provider plugins** (e.g., for GCP, AWS, or Azure) and sets up the **backend** for storing the state file.
- **Analogy**: Similar to `git init` or `npm install`.

### 2. `terraform apply -auto-approve` (Generate & Execute)
Usually, the workflow is `terraform plan` followed by `terraform apply`. However, `apply` can perform both steps.
- **Function**: It creates an execution plan (showing what will be changed) and then applies those changes to reach the desired state.
- **Flag `-auto-approve`**: By default, `apply` asks for a manual "yes" confirmation. Using this flag skips the interactive prompt and executes the plan immediately.

### 3. `terraform destroy` (Cleanup)
When you no longer need the infrastructure, you remove it to stop incurring costs.
- **Function**: It looks at the state file and removes every resource that Terraform created for that specific project.

---

## 🔗 Resources

To learn more about these commands, you can refer to the official documentation:

*   **Official Documentation**: [Terraform CLI Commands](https://developer.hashicorp.com/terraform/cli/commands)
*   **Terraform Init**: [terraform init docs](https://developer.hashicorp.com/terraform/cli/commands/init)
*   **Terraform Apply**: [terraform apply docs](https://developer.hashicorp.com/terraform/cli/commands/apply)
*   **Terraform Destroy**: [terraform destroy docs](https://developer.hashicorp.com/terraform/cli/commands/destroy)
*   **Course Reference**: [Introduction to Terraform (Video)](https://www.youtube.com/watch?v=s2bOYDCKl_M&list=PL3MmuxUbc_hJed7dXYoJw8DoCuVHhGEQb&index=11)
