# Week 8 — CI/CD & Terraform 🚀

This week, I expanded my DevOps skills by working with GitHub Actions, Terraform, Google Kubernetes Engine (GKE), AWS, remote Terraform state, security, and Infrastructure as Code (IaC).

## Day 1 — CI/CD with GitHub Actions

### Objective
Build a basic CI/CD pipeline using GitHub Actions.

### Work completed
- Created the GitHub repository `github-actions-cicd-demo`.
- Created a Python application in `app.py`.
- Installed and configured GitHub CLI on macOS.
- Authenticated GitHub CLI.
- Created a GitHub Actions workflow in `.github/workflows/main.yml`.
- Configured the workflow to run when code is pushed to `main`.
- Used `actions/checkout@v4` and `actions/setup-python@v5`.
- Ran the Python application automatically through GitHub Actions.
- Added a deployment simulation step.
- Verified that the workflow completed successfully.

### Key workflow
```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"

      - name: Run application
        run: python app.py

      - name: Deployment simulation
        run: echo "Deployment successful!"
```

### What I learned
I learned how GitHub Actions can automatically run application tasks when code is pushed to a repository. I also learned how workflow files define jobs, runners, actions, and commands used in a CI/CD pipeline.

---

## Day 2 — Terraform Fundamentals

### Objective
Learn the fundamentals of Terraform and Infrastructure as Code.

### Work completed
- Installed Terraform on macOS using Homebrew.
- Created a Terraform project in `~/terraform-day2`.
- Configured the HashiCorp Random provider.
- Created a `random_pet` resource.
- Used:
  - `terraform init`
  - `terraform plan`
  - `terraform apply`
  - `terraform show`
  - `terraform destroy`
- Inspected Terraform state using `terraform show`.
- Successfully destroyed the test resource.

### Terraform example
```hcl
terraform {
  required_providers {
    random = {
      source = "hashicorp/random"
    }
  }
}

provider "random" {}

resource "random_pet" "example" {
  length = 2
}

output "pet_name" {
  value = random_pet.example.id
}
```

### What I learned
I learned how Terraform uses providers, resources, configuration files, and state to manage infrastructure. I practiced the complete Terraform workflow from initialization and planning through deployment, inspection, and destruction.

---

## Day 3 — Terraform + GKE

### Objective
Use Terraform to provision a Kubernetes cluster on a cloud provider.

### Work completed
- Created the Terraform project `~/terraform-gke-day3`.
- Configured the Google Terraform provider.
- Authenticated Terraform using Google Cloud Application Default Credentials.
- Created a GKE Autopilot cluster named `terraform-gke-day3` in `us-east1`.
- Used `terraform init`, `terraform plan`, and `terraform apply`.
- Connected `kubectl` to the Terraform-created GKE cluster.
- Verified the Kubernetes node was in a Ready state.
- Learned how GKE deletion protection can prevent Terraform from destroying a cluster.
- Set `deletion_protection = false` and successfully ran `terraform destroy`.

### What I learned
I learned how Terraform can provision managed Kubernetes infrastructure and how Terraform authentication connects infrastructure code to GCP. I also learned how lifecycle protections can affect resource deletion.

---

## Day 4 — Open-Source Terraform Project on AWS

### Objective
Deploy an open-source Terraform project and explore modules, variables, outputs, scalability, and security.

### Work completed
- Installed and configured the AWS CLI.
- Created an IAM user for Terraform learning and configured AWS CLI credentials.
- Verified AWS authentication with `aws sts get-caller-identity`.
- Cloned the open-source repository:
  `terraform-aws-modules/terraform-aws-s3-bucket`
- Used the repository's ACL example.
- Changed the example region from `eu-west-1` to `us-east-1`.
- Ran `terraform init`, `terraform validate`, `terraform plan`, and `terraform apply`.
- Deployed S3 buckets and an S3 object using reusable Terraform modules.
- Verified S3 Public Access Block settings.
- Added an `environment` variable to make resource naming more flexible.
- Used `terraform plan` to understand how changing names would cause resource replacement.
- Ran `terraform destroy` and successfully removed the deployed resources.

### What I learned
I learned how to clone and deploy an open-source Terraform project instead of building every resource from scratch. I also learned how modules make Terraform configurations reusable and how variable changes can affect resource lifecycle and replacement.

---

## Day 5 — Security, Optimization & Documentation

### Objective
Implement Terraform security best practices, improve configuration flexibility, use a remote backend, review Kubernetes RBAC, and cleanly document the week's work.

### Security work completed

I created a dedicated AWS S3 bucket for Terraform remote state:

`terraform-day5-states-1789769454`

I enabled AES-256 server-side encryption and verified the configuration.

I also enabled all four S3 Public Access Block protections:

- `BlockPublicAcls = true`
- `IgnorePublicAcls = true`
- `BlockPublicPolicy = true`
- `RestrictPublicBuckets = true`

### Remote Terraform backend

I configured an S3 backend using:

```hcl
terraform {
  backend "s3" {
    bucket = "terraform-day5-states-1789769454"
    key    = "day5/terraform.tfstate"
    region = "us-east-1"
  }
}
```

Terraform successfully initialized the S3 backend and stored the Terraform state remotely.

### Kubernetes RBAC

I reviewed the RBAC work completed during Week 7 and verified least-privilege permissions using `kubectl auth can-i`.

The service account was allowed to create deployments but denied permission to delete pods or create nodes.

### Optimization

I used a `variables.tf` file to make Terraform configuration more flexible. During Day 4, I added an `environment` variable for resource naming and used Terraform's plan output to understand how configuration changes can cause resources to be replaced.

### Cleanup

I tested `terraform destroy` and successfully removed the temporary AWS resources. I also deleted the temporary Terraform state bucket after completing the exercise, leaving no Day 5 AWS resources behind.

### What I learned

I learned how to secure Terraform state by storing it in an encrypted AWS S3 remote backend. I learned how public access controls help protect Terraform state and how Kubernetes RBAC can restrict actions according to assigned permissions. I also learned how variables improve Terraform configuration flexibility and how remote backends can support collaboration. Finally, I practiced the complete Terraform lifecycle and cleaned up the temporary infrastructure after testing.

---

# Week 8 — Skills Gained

By completing Week 8, I gained practical experience with:

- GitHub Actions CI/CD
- GitHub CLI
- Python workflow automation
- Terraform installation and configuration
- Infrastructure as Code (IaC)
- Terraform providers and resources
- Terraform state
- Terraform variables and outputs
- Terraform modules
- Terraform lifecycle management
- Google Kubernetes Engine provisioning
- AWS S3 infrastructure
- Open-source Terraform projects
- AWS CLI authentication
- S3 encryption
- S3 Public Access Block
- Terraform S3 remote backends
- Kubernetes RBAC
- Infrastructure security
- Infrastructure optimization
- Terraform planning and resource replacement
- Terraform destroy and cloud resource cleanup

# Week 8 Summary

This week, I learned how to combine CI/CD automation, Terraform, Kubernetes, and cloud infrastructure into a practical DevOps workflow. I built a GitHub Actions pipeline, learned the Terraform workflow, provisioned a GKE cluster with Terraform, and deployed an open-source Terraform project on AWS. I improved my understanding of Terraform modules, variables, state, remote backends, and infrastructure lifecycle management. I also practiced security techniques including encrypted Terraform state, S3 Public Access Block, and Kubernetes RBAC. I learned how to review Terraform plans carefully before applying changes, especially when configuration changes can force resources to be replaced. Finally, I practiced cleaning up cloud infrastructure with Terraform so that temporary learning resources do not remain running unnecessarily.
