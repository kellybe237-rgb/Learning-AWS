# Week 5 — Google Cloud Platform (GCP) ☁️

This week focused on the fundamentals of Google Cloud Platform, Compute Engine, Kubernetes Engine (GKE), and deploying applications on Google Cloud.

## Day 1 — Basics of GCP and Deploy Applications on Google Cloud

### Objective
Learn the basics of GCP and prepare the Google Cloud environment for hands-on deployment.

### Work completed
- Created and configured a Google Cloud project.
- Installed/configured the Google Cloud SDK (gcloud CLI).
- Authenticated the Google Cloud CLI and configured the active project.
- Learned the basic structure of GCP projects and cloud resources.

### Key commands
```bash
gcloud auth login
gcloud projects list
gcloud config set project PROJECT_ID
gcloud config get-value project
```

## Day 2 — Learn GCP Compute Engine

### Objective
Learn how Google Cloud Compute Engine provides virtual machines and understand machine types, zones, and regions.

### Work completed
- Created a Compute Engine VM named `gcp-day2-vm`.
- Used the `us-east1-b` zone.
- Learned how to manage the VM through the gcloud CLI.
- Connected to the VM using SSH.

### Key commands
```bash
gcloud compute instances create gcp-day2-vm \
  --zone=us-east1-b \
  --machine-type=e2-micro \
  --image-family=ubuntu-2204-lts \
  --image-project=ubuntu-os-cloud

gcloud compute instances list
gcloud compute ssh gcp-day2-vm --zone=us-east1-b
```

## Day 3 — Deploy a Simple Web App on GCP

### Objective
Deploy a basic web server on the Compute Engine VM and access it from a browser.

### Work completed
- Connected to `gcp-day2-vm` using SSH.
- Installed Nginx on the Ubuntu VM.
- Started and verified the Nginx service.
- Retrieved the VM's external IP address.
- Accessed the Nginx web page from a browser using the VM's public IP.

### Key commands
```bash
sudo apt update
sudo apt install nginx -y
sudo systemctl status nginx
```

Get the external IP from the local terminal:

```bash
gcloud compute instances describe gcp-day2-vm \
  --zone=us-east1-b \
  --format="get(networkInterfaces[0].accessConfigs[0].natIP)"
```

Then open:

```text
http://EXTERNAL_IP
```

## Day 4 — Learn Google Kubernetes Engine (GKE)

### Objective
Understand how GKE simplifies Kubernetes cluster management and learn the basics of deploying containerized applications on GKE.

### Work completed
- Selected the correct GCP project using the gcloud CLI.
- Enabled the Kubernetes Engine API.
- Resolved the required GKE service-account permission.
- Created a GKE Autopilot cluster named `learning-gke` in `us-central1`.
- Installed/configured the GKE authentication plugin.
- Connected `kubectl` to the GKE cluster.
- Deployed an Nginx containerized application.
- Exposed the Nginx deployment using a Kubernetes LoadBalancer Service.
- Verified that the application was working.

### Key commands
```bash
gcloud config set project project-7e6dd55c-8c5c-4d4e-ab3

gcloud services enable container.googleapis.com

gcloud container clusters create-auto learning-gke \
  --location=us-central1

gcloud container clusters get-credentials learning-gke \
  --location=us-central1

kubectl get nodes
kubectl get pods -A
kubectl create deployment nginx --image=nginx
kubectl get pods
kubectl expose deployment nginx --type=LoadBalancer --port=80
kubectl get services
```

After completing the exercise, the GKE cluster was deleted to avoid leaving unnecessary cloud resources running.

## Day 5 — Open-Source Project Deployment

### Objective
Clone an open-source Flask application from GitHub and deploy it on the Compute Engine VM created earlier.

### Work completed
- Started `gcp-day2-vm` after finding that it was stopped.
- Connected to the VM using SSH.
- Cloned an open-source Flask application from GitHub.
- Installed the required Flask software.
- Started the Flask application on port `5000`.
- Created a GCP firewall rule allowing TCP traffic on port `5000`.
- Added the appropriate network tag to the VM.
- Retrieved the VM's external IP address.
- Successfully opened the Flask application in a web browser.

### Key commands
```bash
gcloud compute instances start gcp-day2-vm --zone=us-east1-b
gcloud compute ssh gcp-day2-vm --zone=us-east1-b

git clone https://github.com/mmumshad/simple-webapp-flask.git
cd simple-webapp-flask

sudo apt update
sudo apt install python3-flask -y
export FLASK_APP=app.py
flask run --host=0.0.0.0 --port=5000
```

GCP firewall configuration:

```bash
gcloud compute firewall-rules create allow-flask-5000 \
  --network=default \
  --allow=tcp:5000 \
  --source-ranges=0.0.0.0/0 \
  --target-tags=flask

gcloud compute instances add-tags gcp-day2-vm \
  --zone=us-east1-b \
  --tags=flask
```

The application was tested using:

```text
http://EXTERNAL_IP:5000
```

## What new skills, information or understanding have I taken away from this week?

This week, I gained a better understanding of Google Cloud Platform and cloud-based application deployment. I learned how to create and manage GCP resources using the gcloud CLI and how Compute Engine provides virtual machines for hosting applications. I also learned how to create a GKE Autopilot cluster, connect to it with kubectl, and deploy a containerized Nginx application. In addition, I learned how to clone and deploy an open-source Flask application from GitHub onto a cloud VM. I gained practical experience with GCP firewall rules and learned how network access affects applications running on cloud servers. Overall, the exercises improved my understanding of cloud infrastructure, Kubernetes, Linux servers, networking, and application deployment.
