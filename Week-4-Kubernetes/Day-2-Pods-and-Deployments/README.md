# Day 2 — Pods and Deployments

## Objective
Learn how Kubernetes uses Pods and Deployments to run, manage, and scale applications.

## Work completed
- Created a Deployment manifest.
- Deployed Nginx using a Deployment.
- Verified Pods managed by the Deployment.
- Scaled the Deployment to 5 replicas.
- Confirmed the desired replicas were running.

## Deployment manifest

### `deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
```

Apply the Deployment:

```bash
kubectl apply -f deployment.yaml
kubectl get deployments
kubectl get pods
```

Scale the Deployment to five replicas:

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

Verify the replicas:

```bash
kubectl get deployment nginx-deployment
kubectl get pods -l app=nginx
```

## Result

The Deployment maintained five Nginx replicas. This demonstrated how Kubernetes uses Deployments to manage Pods and how applications can be scaled by changing the desired replica count.

## Key skills

- YAML manifests
- Deployments
- Replica management
- Application scaling
- kubectl resource management
