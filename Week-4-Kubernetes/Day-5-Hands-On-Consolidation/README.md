# Day 5 — Hands-On Consolidation

## Objective
Combine Kubernetes concepts to deploy and manage a multi-container application.

## Project
The consolidation exercise used a **WordPress + MySQL** application to combine Deployments, Services, container configuration, and application networking.

## MySQL manifest

### `mysql.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
        - name: mysql
          image: mysql:8.0
          env:
            - name: MYSQL_ROOT_PASSWORD
              value: rootpassword
            - name: MYSQL_DATABASE
              value: wordpress
          ports:
            - containerPort: 3306
---
apiVersion: v1
kind: Service
metadata:
  name: mysql
spec:
  selector:
    app: mysql
  ports:
    - port: 3306
      targetPort: 3306
```

## WordPress manifest

### `wordpress.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: wordpress
spec:
  replicas: 1
  selector:
    matchLabels:
      app: wordpress
  template:
    metadata:
      labels:
        app: wordpress
    spec:
      containers:
        - name: wordpress
          image: wordpress:latest
          env:
            - name: WORDPRESS_DB_HOST
              value: mysql:3306
            - name: WORDPRESS_DB_USER
              value: root
            - name: WORDPRESS_DB_PASSWORD
              value: rootpassword
            - name: WORDPRESS_DB_NAME
              value: wordpress
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: wordpress
spec:
  selector:
    app: wordpress
  ports:
    - port: 80
      targetPort: 80
  type: NodePort
```

## Deploy and verify

```bash
kubectl apply -f mysql.yaml
kubectl apply -f wordpress.yaml
kubectl get pods
kubectl get deployments
kubectl get services
```

Open the WordPress Service with Minikube:

```bash
minikube service wordpress --url
```

## Result

This exercise brought together the Kubernetes concepts learned during the week. The application used separate workloads for WordPress and MySQL and Services to provide communication and access.

## Key skills

- Multi-container application deployment
- Kubernetes Deployments
- Kubernetes Services
- Application networking
- YAML manifests
- Resource verification
- Troubleshooting
