# Day 1 — Kubernetes Introduction ☸️

## Objective
Learn the fundamentals of Kubernetes and set up a local Kubernetes environment.

## Work completed
- Set up Docker, Minikube, and kubectl on macOS.
- Started a local Kubernetes cluster.
- Verified the cluster and node.
- Created and deployed an Nginx Pod.
- Verified the Pod was running.

## Kubernetes setup

```bash
minikube start
kubectl cluster-info
kubectl get nodes
kubectl get pods -A
```

## Pod manifest

### `pod.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```

Apply the Pod:

```bash
kubectl apply -f pod.yaml
kubectl get pods
kubectl describe pod nginx-pod
```

Test the Nginx application locally:

```bash
kubectl port-forward pod/nginx-pod 8080:80
```

The application was then opened in the browser using local port `8080`.

## Result

The exercise demonstrated the basic Kubernetes workflow: start a cluster, create a Pod from YAML, deploy it with kubectl, inspect the resource, and access the application.

## Key skills

- Kubernetes cluster setup
- Minikube
- kubectl
- Pods
- Kubernetes YAML
- Basic application deployment
- Resource verification
