# Week 4 — Kubernetes ☸️

This week focused on learning **Kubernetes**, using a local Kubernetes environment on my Mac with Docker, Minikube, and kubectl. The exercises progressed from deploying a basic Pod to creating Deployments, Services, Namespaces, ConfigMaps, a multi-container application, and exploring Ingress and Helm.

## Week 4 objectives

- Understand Kubernetes Pods, Nodes, Deployments, Services, and Namespaces.
- Set up a local Kubernetes cluster with Minikube.
- Use kubectl to create, inspect, scale, and troubleshoot workloads.
- Write Kubernetes YAML manifests.
- Expose applications using Services.
- Use Namespaces and ConfigMaps for organization and configuration.
- Deploy a multi-container application using Kubernetes manifests.
- Explore Ingress and Helm.

---

## Exercises completed

| Day | Topic | Result |
|---|---|---|
| 1 | Kubernetes Introduction | Minikube and kubectl configured; Nginx Pod deployed |
| 2 | Pods and Deployments | Deployment created and scaled to 5 replicas |
| 3 | Kubernetes Services | Application exposed and verified through a browser |
| 4 | Namespaces and ConfigMaps | Namespace and ConfigMap created and used |
| 5 | Hands-On Consolidation | Multi-container application deployed with Kubernetes manifests |
| 6 | Advanced Kubernetes | Ingress and Helm concepts explored |

---

# 1. Kubernetes setup

The Kubernetes exercises were completed locally on macOS. Docker was used as the container runtime and Minikube provided the local Kubernetes cluster.

```bash
minikube start
kubectl cluster-info
kubectl get nodes
kubectl get pods -A
```

---

# 2. Day 1 — Kubernetes Introduction

The first exercise introduced the basic Kubernetes object used to run a container: a **Pod**.

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

Apply and verify:

```bash
kubectl apply -f pod.yaml
kubectl get pods
kubectl describe pod nginx-pod
kubectl port-forward pod/nginx-pod 8080:80
```

The Nginx application was verified through the browser on local port `8080`.

### Result

I learned how Kubernetes runs a container inside a Pod and how kubectl is used to create and inspect Kubernetes resources.

---

# 3. Day 2 — Pods and Deployments

This exercise introduced **Deployments**, which manage replicated Pods.

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

Apply and inspect:

```bash
kubectl apply -f deployment.yaml
kubectl get deployments
kubectl get pods
```

Scale to five replicas:

```bash
kubectl scale deployment nginx-deployment --replicas=5
kubectl get deployment nginx-deployment
kubectl get pods -l app=nginx
```

### Result

The Deployment maintained five Nginx replicas, demonstrating Kubernetes application scaling.

---

# 4. Day 3 — Kubernetes Services

A **Service** provides a stable way to access Pods.

### `service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: NodePort
```

Apply and verify:

```bash
kubectl apply -f service.yaml
kubectl get services
kubectl describe service nginx-service
minikube service nginx-service --url
```

The returned URL was opened in a browser to verify the application.

### Result

I learned how Services connect users to Pods and provide a stable application endpoint.

---

# 5. Day 4 — Namespaces and ConfigMaps

Namespaces provide logical separation of Kubernetes resources.

Create a Namespace:

```bash
kubectl create namespace my-namespace
kubectl get namespaces
```

### `configmap.yaml`

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
  namespace: my-namespace
data:
  APP_ENV: "development"
  APP_MESSAGE: "Hello from Kubernetes ConfigMap"
```

Apply and verify:

```bash
kubectl apply -f configmap.yaml
kubectl get configmaps -n my-namespace
kubectl describe configmap app-config -n my-namespace
```

Example of consuming the ConfigMap as environment variables:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: config-demo
  namespace: my-namespace
spec:
  containers:
    - name: app
      image: nginx:latest
      env:
        - name: APP_ENV
          valueFrom:
            configMapKeyRef:
              name: app-config
              key: APP_ENV
        - name: APP_MESSAGE
          valueFrom:
            configMapKeyRef:
              name: app-config
              key: APP_MESSAGE
```

### Result

I learned how Namespaces organize resources and how ConfigMaps provide application configuration without hard-coding values into an image.

---

# 6. Day 5 — Hands-On Consolidation

The consolidation exercise combined Kubernetes concepts to deploy a **multi-container WordPress + MySQL application** using Kubernetes manifests.

### MySQL Deployment and Service

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

### WordPress Deployment and Service

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

Apply and verify:

```bash
kubectl apply -f mysql.yaml
kubectl apply -f wordpress.yaml
kubectl get pods
kubectl get deployments
kubectl get services
minikube service wordpress --url
```

### Result

This exercise demonstrated how multiple Kubernetes resources work together to deploy an application stack and how Services allow application components to communicate and be accessed.

---

# 7. Day 6 — Advanced Kubernetes

## Kubernetes Ingress

Ingress provides HTTP/HTTPS routing to Services.

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
```

## Helm

Helm is a package manager for Kubernetes. Example commands practiced/explored:

```bash
helm version
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm search repo bitnami
helm install my-release bitnami/nginx
helm list
kubectl get pods
```

### Result

I learned the purpose of Ingress for HTTP/HTTPS routing and Helm for packaging and managing Kubernetes applications.

---

# Troubleshooting

Useful commands used during troubleshooting included:

```bash
kubectl get pods
kubectl get services
kubectl get deployments
kubectl describe pod <pod-name>
kubectl describe service <service-name>
kubectl logs <pod-name>
kubectl get events
```

These commands helped identify resource status, configuration problems, and connectivity issues.

---

# Skills gained

- Kubernetes fundamentals
- Minikube
- kubectl
- Pods
- Deployments
- Replica scaling
- Services and NodePort
- Namespaces
- ConfigMaps
- Kubernetes YAML
- Multi-container application deployment
- Ingress fundamentals
- Helm fundamentals
- Application troubleshooting
- Container orchestration

---

# Key takeaway

Week 4 moved my learning from individual Docker containers into **container orchestration with Kubernetes**. I learned how Kubernetes manages workloads with Pods and Deployments, exposes applications through Services, separates resources with Namespaces, provides configuration through ConfigMaps, and supports advanced management through Ingress and Helm.

The hands-on work strengthened my ability to write Kubernetes YAML manifests, use kubectl, scale applications, verify resources, expose services, and troubleshoot deployment and connectivity problems.
