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

### Week 4 — Google Cloud Platform ☁️

Worked with Google Cloud Platform to create and manage GKE Kubernetes infrastructure and deploy an open-source Flask application on Compute Engine.

**Week 4 highlights:**

- Logged into and managed Google Cloud using the `gcloud` CLI.
- Enabled the Kubernetes Engine API and configured GKE permissions.
- Created a GKE Autopilot cluster named `learning-gke` in `us-central1`.
- Connected `kubectl` to the GKE cluster.
- Deployed an Nginx containerized application on GKE.
- Exposed the Nginx application using a Kubernetes LoadBalancer Service.
- Started and connected to the `gcp-day2-vm` Compute Engine instance.
- Cloned an open-source Flask application from GitHub.
- Deployed Flask on the Compute Engine VM using port `5000`.
- Configured a GCP firewall rule and successfully accessed the application from a browser.

## Repository structure

```text
Learning-AWS/
├── README.md
├── Week-2-AWS-Infrastructure/
├── Week-3-Docker/
│   ├── README.md
│   ├── Day-1-Docker-Introduction/
│   ├── Day-2-Docker-Images/
│   ├── Day-3-Docker-Containers/
│   ├── Day-4-Nginx/
│   ├── Day-5-Docker-Management/
│   ├── Day-6-Docker-Workflow/
│   └── Day-7-Advanced-Docker/
├── Week-4-Kubernetes/
└── Week-4-GCP/
    ├── README.md
    ├── Day-4-GKE/
    └── Day-5-Flask-on-Compute-Engine/
```

## Goal

Continue developing practical cloud engineering skills by combining cloud infrastructure, Linux, containers, Kubernetes, networking, automation, and deployment workflows.
