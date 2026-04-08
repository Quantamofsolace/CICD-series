GitHub Actions + Terraform Pipeline
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

📂 Terraform Workflow Example
name: Terraform Deploy

on:
  workflow_dispatch:   # Manual trigger only

jobs:
  terraform:
    runs-on: ubuntu-latest

    env:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      AWS_DEFAULT_REGION: us-east-1

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3

      - name: Terraform Init
        run: terraform init

      - name: Terraform Validate
        run: terraform validate

      - name: Terraform Plan
        run: terraform plan -out=tfplan

      - name: Terraform Apply
        run: terraform apply -auto-approve tfplan
🧾 Explanation (Step-by-Step)
🔹 Workflow Name
name: Terraform Deploy

👉 Name shown in GitHub UI

🔹 Trigger
on:
  workflow_dispatch:

👉 Manual trigger from GitHub UI
✔ No automatic execution

🔹 Job Definition
jobs:
  terraform:

👉 Creates a job named terraform

🔹 Runner
runs-on: ubuntu-latest

👉 Runs on a Linux virtual machine

🔐 Environment Variables
env:
  AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
  AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
  AWS_DEFAULT_REGION: us-east-1

👉 Uses GitHub Secrets to securely store:

AWS Access Key
AWS Secret Key

👉 Used by Terraform

⚙️ Steps Breakdown
1️⃣ Checkout Code
- name: Checkout
  uses: actions/checkout@v4

👉 Downloads repository code into the runner

2️⃣ Setup Terraform
- name: Setup Terraform
  uses: hashicorp/setup-terraform@v3

👉 Installs Terraform CLI

3️⃣ Terraform Init
- name: Terraform Init
  run: terraform init

👉 Initializes Terraform:

Downloads providers
Sets up backend
4️⃣ Terraform Validate
- name: Terraform Validate
  run: terraform validate

👉 Checks configuration syntax

5️⃣ Terraform Plan
- name: Terraform Plan
  run: terraform plan -out=tfplan

👉 Creates execution plan:

Shows changes
Saves plan as tfplan
6️⃣ Terraform Apply
- name: Terraform Apply
  run: terraform apply -auto-approve tfplan

👉 Applies infrastructure changes
⚠️ -auto-approve skips manual confirmation

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
Job → Group of steps
Step → Individual task
Runner → Machine executing the job
🔹 Terraform in CI/CD

Using Terraform in pipelines helps:

Automate infrastructure
Avoid manual errors
Ensure consistency
🔐 Best Practices
Use GitHub Secrets for credentials
Avoid -auto-approve in production
Add manual approval before apply
Store state remotely (S3 + DynamoDB)
Use separate environments (dev/stage/prod)
