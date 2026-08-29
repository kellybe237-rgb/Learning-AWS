# Day 4 — Learn Google Kubernetes Engine (GKE) ☸️

## Objective

- Learn how GKE simplifies Kubernetes cluster management.
- Explore the basics of deploying containerized applications on GKE.
- Create a GKE cluster using the Google Cloud CLI.

## Work completed

I logged into Google Cloud using the `gcloud` CLI and selected my GCP project. I enabled the Kubernetes Engine API and configured the required service-account permission. I created a GKE Autopilot cluster named `learning-gke` in `us-central1`, configured `kubectl`, deployed Nginx, and exposed the application using a Kubernetes LoadBalancer Service.

## Create the GKE cluster

```bash
gcloud container clusters create-auto learning-gke \
  --location=us-central1
```

## Verify the cluster

```bash
gcloud container clusters list
```

## Connect kubectl

```bash
gcloud container clusters get-credentials learning-gke \
  --location=us-central1
```

Verify the connection:

```bash
kubectl get nodes
kubectl get pods -A
```

## Deploy Nginx

```bash
kubectl create deployment nginx --image=nginx
kubectl get deployments
kubectl get pods
```

## Expose Nginx

```bash
kubectl expose deployment nginx \
  --type=LoadBalancer \
  --port=80
```

Verify the Service:

```bash
kubectl get services
```

## Result

The GKE Autopilot cluster was successfully created and connected to `kubectl`. An Nginx containerized application was deployed and exposed through a Kubernetes Service, demonstrating the basic workflow for running applications on GKE.

## Key skills

- Google Cloud CLI (`gcloud`)
- Google Kubernetes Engine (GKE)
- GKE Autopilot
- `kubectl`
- Kubernetes Deployments
- Kubernetes Services
- Containerized application deployment
