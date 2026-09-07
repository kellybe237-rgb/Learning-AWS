# AWS Cloud Internship – Learning Journey 🚀

This repository documents my hands-on AWS and cloud learning journey, organized by week.

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

## Repository structure

```text
Learning-AWS/
├── README.md
├── Week-2-AWS-Infrastructure/
├── Week-3-Docker/
├── Week-5-GCP/
│   └── README.md
└── Week-6-Azure/
    └── README.md
```

## Goal

Continue developing practical cloud engineering skills by combining AWS, GCP, and Azure infrastructure with Linux, containers, Kubernetes, networking, automation, security, monitoring, and deployment workflows.
