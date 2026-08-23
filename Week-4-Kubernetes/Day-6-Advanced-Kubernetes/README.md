# Day 6 — Advanced Kubernetes

## Objective
Explore advanced Kubernetes features used for application routing and package management.

## Part 1 — Kubernetes Ingress

Ingress provides HTTP/HTTPS routing from an external request to a Kubernetes Service.

### `ingress.yaml`

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
spec:
  rules:
    - host: myapp.local
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: nginx-service
                port:
                  number: 80
```

Apply and verify:

```bash
kubectl apply -f ingress.yaml
kubectl get ingress
kubectl describe ingress app-ingress
```

## Part 2 — Helm

Helm is a package manager for Kubernetes. It uses reusable charts to simplify application installation and management.

Example commands:

```bash
helm version
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm search repo bitnami
```

Example chart installation:

```bash
helm install my-release bitnami/nginx
```

Verify the Helm release and Kubernetes resources:

```bash
helm list
kubectl get pods
kubectl get services
```

## Result

This exercise introduced two important Kubernetes ecosystem tools. Ingress provides a way to route HTTP/HTTPS traffic to Services, while Helm simplifies the packaging and management of Kubernetes applications.

## Key skills

- Kubernetes Ingress
- HTTP/HTTPS routing concepts
- Helm
- Helm repositories and charts
- Kubernetes application management
