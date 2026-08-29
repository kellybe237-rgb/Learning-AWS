# Day 4 — Learn Google Kubernetes Engine (GKE)

## Objective
Understand GKE and deploy a containerized application using managed Kubernetes on Google Cloud.

## Work Completed
- Learned how GKE simplifies Kubernetes cluster management.
- Created a GKE Autopilot cluster named `learning-gke` in `us-central1`.
- Installed/configured the GKE authentication plugin and connected `kubectl` to the cluster.
- Deployed an Nginx containerized application.
- Exposed the Nginx deployment using a Kubernetes LoadBalancer Service and verified the application.

## Key Commands
```bash
gcloud container clusters create-auto learning-gke --location=us-central1
gcloud container clusters get-credentials learning-gke --location=us-central1
kubectl get nodes
kubectl get pods -A
kubectl create deployment nginx --image=nginx
kubectl get pods
kubectl expose deployment nginx --type=LoadBalancer --port=80
kubectl get services
```

## What I Learned
I learned how GKE provides managed Kubernetes, how to connect to a cloud Kubernetes cluster with `kubectl`, and how to deploy and expose a containerized application.
