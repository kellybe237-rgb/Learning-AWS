# Week 4 — Google Cloud Platform (GCP) ☁️

This week focused on deploying and managing applications using Google Cloud Platform. The exercises included creating a managed Kubernetes cluster with Google Kubernetes Engine (GKE) and deploying an open-source Flask application on Google Compute Engine.

## Exercises completed

| Day | Topic | Result |
|---|---|---|
| Day 4 | Google Kubernetes Engine (GKE) | Created a GKE Autopilot cluster, connected kubectl, deployed Nginx, and exposed the application |
| Day 5 | Open-Source Project Deployment | Cloned and deployed a Flask application on a Compute Engine VM and accessed it from a browser |

---

## Day 4 — Learn Google Kubernetes Engine (GKE)

### Objective

Learn how GKE simplifies Kubernetes cluster management and understand the basics of deploying containerized applications on Google Cloud.

### Work completed

I logged into Google Cloud using the `gcloud` CLI and selected my GCP project. I enabled the Kubernetes Engine API and resolved the required service-account permission. I then created a GKE Autopilot cluster named `learning-gke` in `us-central1`.

### Create the GKE cluster

```bash
gcloud container clusters create-auto learning-gke \
  --location=us-central1
```

### Verify the cluster

```bash
gcloud container clusters list
```

The cluster was successfully created with a `RUNNING` status.

### Connect kubectl to GKE

```bash
gcloud container clusters get-credentials learning-gke \
  --location=us-central1
```

Verify the Kubernetes connection:

```bash
kubectl get nodes
kubectl get pods -A
```

The GKE authentication plugin was also installed so that `kubectl` could authenticate with the GKE cluster.

### Deploy a containerized application

```bash
kubectl create deployment nginx --image=nginx
```

Verify the deployment:

```bash
kubectl get pods
kubectl get deployments
```

Expose the application:

```bash
kubectl expose deployment nginx \
  --type=LoadBalancer \
  --port=80
```

Verify the Service:

```bash
kubectl get services
```

### Result

The Nginx application was successfully deployed to GKE. This exercise demonstrated how Google Cloud provides a managed Kubernetes environment and how standard Kubernetes commands can be used to deploy and manage containerized applications in the cloud.

---

## Day 5 — Open-Source Project Deployment

### Objective

Clone an open-source Flask application from GitHub and deploy it on the Google Cloud Compute Engine VM created earlier.

### Work completed

I connected to the Compute Engine VM using the `gcloud` CLI. The VM was initially stopped, so I started it before connecting. I then cloned a simple open-source Flask application from GitHub, installed the required software, and prepared the application to run on the VM.

### Start and connect to the VM

```bash
gcloud compute instances start gcp-day2-vm \
  --zone=us-east1-b
```

Connect to the VM:

```bash
gcloud compute ssh gcp-day2-vm \
  --zone=us-east1-b
```

### Clone the Flask application

```bash
git clone https://github.com/mmumshad/simple-webapp-flask.git
cd simple-webapp-flask
```

Check the project files:

```bash
ls
```

### Install Flask

```bash
sudo apt update
sudo apt install python3-flask -y
```

Set the Flask application:

```bash
export FLASK_APP=app.py
```

### Run the Flask application

```bash
flask run --host=0.0.0.0 --port=5000
```

### Configure the GCP firewall

A firewall rule was created to allow external traffic to the Flask application on TCP port `5000`:

```bash
gcloud compute firewall-rules create allow-flask-5000 \
  --network=default \
  --allow=tcp:5000 \
  --source-ranges=0.0.0.0/0 \
  --target-tags=flask
```

The VM was given the matching network tag:

```bash
gcloud compute instances add-tags gcp-day2-vm \
  --zone=us-east1-b \
  --tags=flask
```

Get the VM external IP:

```bash
gcloud compute instances describe gcp-day2-vm \
  --zone=us-east1-b \
  --format="get(networkInterfaces[0].accessConfigs[0].natIP)"
```

The Flask application was then accessed using:

```text
http://EXTERNAL_IP:5000
```

### Result

The open-source Flask application was successfully deployed on the Compute Engine VM and accessed through a web browser using the VM's external IP address and port `5000`.

---

## What I learned this week

This week, I gained practical experience using Google Cloud for both Kubernetes and virtual-machine application deployment. I learned how to create and manage a GKE Autopilot cluster, connect to it with `kubectl`, and deploy a containerized Nginx application. I also learned how to clone an open-source application from GitHub and deploy it on a Compute Engine VM. Working with the GCP firewall improved my understanding of how network rules control access to applications running on cloud infrastructure. Overall, these exercises strengthened my understanding of cloud deployment, Kubernetes, Linux, Git, networking, and application troubleshooting.
