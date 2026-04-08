📘 GitHub Actions + Terraform Pipeline
🚀 What is GitHub Actions?

GitHub Actions is a CI/CD tool provided by GitHub.

It allows you to:

Automate workflows
Build, test, and deploy code
Run pipelines directly from your repository
🔄 What is a Pipeline?

A pipeline is a sequence of automated steps that:

Fetch code
Build or validate it
Test it
Deploy it

👉 In GitHub Actions, pipelines are called workflows

📂 Your Terraform Workflow
# name: Terraform Deploy

👉 Name of the workflow (visible in GitHub UI)

# on:
#   workflow_dispatch:

👉 Defines trigger

workflow_dispatch = Manual trigger from GitHub UI
✔ No automatic execution
jobs:
  terraform:

👉 Defines a job named terraform

runs-on: ubuntu-latest

👉 Runs job on a Linux virtual machine

🔐 Environment Variables
env:
  AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
  AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
  AWS_DEFAULT_REGION: us-east-1

👉 सेट AWS credentials using GitHub Secrets

Keeps sensitive data secure
Used by Terraform
⚙️ Steps Breakdown
1️⃣ Checkout Code
- name: Checkout
  uses: actions/checkout@v4

👉 Downloads repository code into runner

2️⃣ Setup Terraform
- name: Setup Terraform
  uses: hashicorp/setup-terraform@v3

👉 Installs Terraform CLI

3️⃣ Terraform Init
- name: Terraform Init
  run: terraform init

👉 Initializes Terraform:

Downloads providers
Prepares backend
4️⃣ Terraform Validate
- name: Terraform Validate
  run: terraform validate

👉 Checks syntax and configuration errors

5️⃣ Terraform Plan
- name: Terraform Plan
  run: terraform plan -out=tfplan

👉 Creates execution plan:

Shows what will change
Saves plan to file (tfplan)
6️⃣ Terraform Apply
- name: Terraform Apply
  run: terraform apply -auto-approve tfplan

👉 Applies changes:

Uses saved plan
-auto-approve skips manual confirmation
🔁 Workflow Execution Flow
Manual Trigger
     ↓
Checkout Code
     ↓
Setup Terraform
     ↓
Terraform Init
     ↓
Validate
     ↓
Plan
     ↓
Apply (Deploy Infrastructure)
🧠 Key Concepts
🔹 GitHub Actions Components
Workflow → Full automation (YAML file)
Job → Group of steps (runs on VM)
Step → Individual task
Runner → Machine executing job
🔹 Terraform in CI/CD

Using Terraform in pipelines helps:

Automate infrastructure
Avoid manual errors
Ensure consistency
🔐 Best Practices
Use secrets for credentials
Avoid -auto-approve in production
Add approval step before apply
Store state remotely (S3 + DynamoDB)
Use separate environments (dev/stage/prod)
