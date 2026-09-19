# My Server Architect Internship Journey 🚀

This repository documents my hands-on server architecture, cloud, DevOps, and infrastructure learning journey, organized by week.

## Weekly progress

### Week 1 — AWS Foundations

Built a foundation in AWS cloud infrastructure, including EC2, security groups, web servers, Lightsail, Elastic IP addresses, and AMIs.

### Week 2 — AWS Infrastructure

Continued building practical AWS infrastructure skills through hands-on EC2 and networking exercises.

### Week 3 — Docker 🐳

Learned Docker on Ubuntu EC2, progressing from installation and basic containers to custom images, Nginx, Docker Swarm, Docker Compose, and a multi-container WordPress + MySQL application.

**Week 3 highlights:**

- Installed and verified Docker on Ubuntu EC2.
- Ran the Docker `hello-world` container.
- Pulled and managed Docker images.
- Built a custom Nginx-based Docker image.
- Published a containerized web application and verified it in a browser.
- Practiced the Docker container lifecycle.
- Initialized Docker Swarm and deployed an Nginx service.
- Used Docker Compose to run WordPress and MySQL together.
- Explored volumes, networks, environment variables, and resource inspection.

### Week 5 — Google Cloud Platform ☁️

Worked with Google Cloud Platform to learn GCP fundamentals, Compute Engine, GKE, and cloud application deployment.

**Week 5 highlights:**

- Set up a GCP project and configured the `gcloud` CLI.
- Created and managed the `gcp-day2-vm` Compute Engine VM.
- Deployed Nginx on the VM and accessed it through the VM's public IP.
- Created a GKE Autopilot cluster named `learning-gke` in `us-central1`.
- Connected `kubectl` to the GKE cluster and deployed Nginx.
- Exposed the Nginx application using a Kubernetes LoadBalancer Service.
- Cloned and deployed an open-source Flask application on Compute Engine.
- Configured a GCP firewall rule to allow Flask traffic on port `5000`.
- Successfully tested the Flask application from a web browser.

### Week 6 — Microsoft Azure ☁️

Worked with Microsoft Azure to learn Azure fundamentals, virtual machines, networking, web application deployment, open-source projects, security, monitoring, performance optimization, and cloud resource cleanup.

**Week 6 highlights:**

- Set up and configured Azure using the Azure Portal and Azure CLI.
- Learned Azure Virtual Machines, resource groups, networking, and AKS fundamentals.
- Created and connected to Linux Azure VMs using SSH keys.
- Deployed Nginx and verified a web server through a VM's public IP.
- Cloned and deployed an open-source Node.js application from GitHub.
- Troubleshot a PM2 log permission error and configured application access on port `3000`.
- Reviewed Azure Monitor and VM performance.
- Secured a VM by verifying that only SSH port `22` was allowed inbound through its NSG.
- Enabled Auto-shutdown to reduce unnecessary VM running costs.
- Cleaned up Azure resources after completing the exercises.

### Week 7 — Helm ⎈

Worked with Helm to package, deploy, secure, optimize, and manage Kubernetes applications using Helm charts and releases.

**Week 7 highlights:**

- Installed and verified Helm `v4.3.0` on macOS.
- Added and explored the Bitnami Helm repository.
- Deployed WordPress using a Helm chart and verified it through Minikube.
- Created, customized, linted, packaged, and deployed a custom Nginx Helm chart.
- Cloned and deployed the open-source Helm examples `hello-world` chart on GKE Autopilot.
- Exposed the GKE application using a LoadBalancer Service and verified the Nginx Welcome Page.
- Configured Kubernetes RBAC with a ServiceAccount, Role, and RoleBinding using least-privilege permissions.
- Verified allowed and denied Kubernetes actions using `kubectl auth can-i`.
- Optimized a Helm deployment with two replicas, CPU and memory requests/limits, liveness probes, and readiness probes.
- Tested Helm upgrades, release history, and rollback to a previous working revision.
- Cleaned up the Helm releases, temporary Kubernetes resources, and GKE cluster after completing the exercises.

### Week 8 — CI/CD & Terraform 🚀

Worked with GitHub Actions and Terraform to build CI/CD automation, practice Infrastructure as Code, provision GKE infrastructure, deploy an open-source Terraform project on AWS, secure remote Terraform state, review Kubernetes RBAC, and optimize cloud infrastructure configurations.

**Week 8 highlights:**

- Built and verified a GitHub Actions CI/CD workflow using Python.
- Installed and used GitHub CLI for repository and workflow development.
- Installed Terraform and practiced the complete `init`, `plan`, `apply`, `show`, and `destroy` workflow.
- Used Terraform to provision a GKE Autopilot cluster on Google Cloud.
- Connected `kubectl` to the Terraform-created GKE cluster and verified a Ready node.
- Learned how GKE deletion protection affects Terraform resource destruction.
- Cloned and deployed the open-source `terraform-aws-modules/terraform-aws-s3-bucket` project on AWS.
- Explored Terraform modules, variables, resources, state, and configuration changes.
- Added an environment variable to make Terraform resource naming more flexible.
- Configured an encrypted AWS S3 remote backend for Terraform state.
- Enabled AES-256 encryption and S3 Public Access Block protections for the Terraform state bucket.
- Reviewed Kubernetes RBAC and least-privilege permissions.
- Tested `terraform destroy` and cleaned up temporary AWS and GCP infrastructure.

## Repository structure

```text
My-Server-Architect-Internship-Journey/
├── README.md
├── Week-2-AWS-Infrastructure/
├── Week-3-Docker/
├── Week-5-GCP/
│   └── README.md
├── Week-6-Azure/
│   └── README.md
├── Week-7-Helm/
│   └── README.md
└── Week-8-CICD-Terraform/
    └── README.md
```

## Goal

Continue developing practical server architecture and cloud engineering skills by combining AWS, GCP, and Azure infrastructure with Linux, containers, Kubernetes, Helm, automation, security, monitoring, Infrastructure as Code, CI/CD, and deployment workflows.
