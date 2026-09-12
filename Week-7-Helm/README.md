# Week 7 — Helm ⎈

This week focused on learning **Helm**, the package manager for Kubernetes, and using Helm to deploy, customize, secure, optimize, and manage Kubernetes applications.

## Week 7 objectives

- Understand Helm and Kubernetes package management.
- Install and verify Helm on macOS.
- Deploy applications using Helm charts and repositories.
- Deploy WordPress using the Bitnami Helm repository.
- Create and package a custom Nginx Helm chart.
- Deploy an open-source Helm project on Google Kubernetes Engine (GKE).
- Configure RBAC and restrict Kubernetes permissions.
- Optimize a Helm deployment using replicas, resource requests/limits, and health probes.
- Use Helm upgrade and rollback to manage deployment versions.
- Practice cleaning up Kubernetes and GKE resources after the exercises.

---

## Exercises completed

| Day | Topic | Result |
|---|---|---|
| 1 | Helm Introduction & Installation | Helm installed and verified on macOS |
| 2 | Deploying Applications with Helm | WordPress deployed successfully using a Helm chart |
| 3 | Creating a Custom Helm Chart | Custom Nginx chart created, packaged, and deployed |
| 4 | Open-Source Helm Project | Helm chart deployed successfully on GKE |
| 5 | Optimization, Security & Rollback | RBAC, resource tuning, probes, and rollback completed |

---

# 1. Day 1 — Introduction to Helm and Installation

### Objective
Understand the purpose of Helm and install Helm on macOS.

### Work completed

- Learned that Helm is a package manager for Kubernetes.
- Learned how Helm charts package Kubernetes resources and application configuration.
- Installed Helm using Homebrew.
- Verified the Helm installation.

### Key commands

```bash
brew install helm
helm version
```

Helm version used during the exercise:

```text
v4.3.0
```

### Result

I learned how Helm simplifies Kubernetes application deployment and management by packaging Kubernetes resources into reusable charts.

---

# 2. Day 2 — Deploying Applications with Helm

### Objective
Deploy an application using an existing Helm chart and explore Helm repositories and chart values.

### Work completed

- Added the Bitnami Helm repository.
- Updated the local Helm repository information.
- Searched the repository for the WordPress chart.
- Inspected the WordPress chart values.
- Installed WordPress using Helm.
- Verified the Helm release and Kubernetes Services.
- Opened the WordPress application successfully using Minikube.

### Key commands

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm search repo bitnami/wordpress
helm show values bitnami/wordpress > wordpress-values.yaml
less wordpress-values.yaml
helm install my-wordpress bitnami/wordpress
helm list
kubectl get svc
minikube service my-wordpress
```

### Troubleshooting

Minikube initially failed because the Docker daemon was not running. Docker Desktop was started and the Minikube environment was then able to start and run the WordPress deployment.

The WordPress LoadBalancer displayed `<pending>` in Minikube, which was expected for the local environment. The application was successfully accessed using the Minikube service command.

### Result

I learned how to use an existing Helm chart, manage Helm repositories, inspect chart values, install a Kubernetes application, and verify the resulting resources.

---

# 3. Day 3 — Creating a Custom Helm Chart

### Objective
Create and deploy a custom Helm chart for an Nginx application.

### Work completed

Created a new Helm chart:

```bash
cd ~
helm create my-nginx
```

The chart included:

```text
my-nginx/
├── Chart.yaml
├── values.yaml
├── charts/
└── templates/
```

Customized `values.yaml` for Nginx:

```yaml
image:
  repository: nginx
  pullPolicy: IfNotPresent
  tag: ""

service:
  type: NodePort
  port: 80
  nodePort: 30080
```

Validated and packaged the chart:

```bash
helm lint .
helm package .
```

Installed the packaged chart on Minikube:

```bash
kubectl config current-context
helm install my-custom-nginx ./my-nginx-0.1.0.tgz
helm list
kubectl get svc
minikube service my-custom-nginx-my-nginx
```

### Result

The custom Nginx Helm chart was successfully packaged and deployed. The Nginx application was verified through the browser.

The generated Service template did not directly use the custom `nodePort` value, so Kubernetes automatically assigned a NodePort. The application still deployed and worked correctly.

### Result

I learned how to create a Helm chart from scratch, customize its values, validate it with `helm lint`, package it, install it, and verify the resulting Kubernetes resources.

---

# 4. Day 4 — Working with an Open-Source Helm Project

### Objective
Deploy an open-source Helm project on a managed Kubernetes cluster.

### Environment

- Google Kubernetes Engine (GKE) Autopilot
- GCP project: `project-7e6dd55c-8c5c-4d4e-ab3`
- Cluster: `helm-day4-cluster`
- Location: `us-east1`
- Kubernetes version: `1.35.7-gke.1222000`

### Work completed

Cloned the official Helm examples repository:

```bash
cd ~
git clone https://github.com/helm/examples.git
cd examples
ls
ls charts/hello-world
```

The open-source chart contained:

```text
charts/hello-world/
├── Chart.yaml
├── README.md
├── templates/
└── values.yaml
```

Validated the chart:

```bash
kubectl config current-context
kubectl get nodes
helm lint charts/hello-world
helm show chart charts/hello-world
helm show values charts/hello-world
```

The chart passed Helm validation:

```text
1 chart(s) linted, 0 chart(s) failed
```

Installed the chart:

```bash
helm install hello-world ./charts/hello-world
helm list
kubectl get pods
kubectl get svc
```

Updated the Service to use a LoadBalancer:

```bash
helm upgrade hello-world ./charts/hello-world \
  --set service.type=LoadBalancer
```

Verified the external Service:

```bash
kubectl get svc hello-world
```

The application received a public external IP and displayed the **Nginx Welcome Page** in a browser.

### Troubleshooting

The GKE Autopilot cluster initially had no ready nodes. Creating a temporary Nginx deployment triggered node provisioning, after which the node reached the `NodeReady` state and workloads could run successfully.

### Cleanup

After verification, the Helm release and GKE cluster were deleted to avoid leaving unnecessary cloud resources running.

### Result

I learned how to clone, validate, install, upgrade, expose, troubleshoot, and deploy an open-source Helm chart on a managed Kubernetes cluster.

---

# 5. Day 5 — Optimization, Security & Rollback

### Objective
Secure Helm deployments, restrict Kubernetes permissions, optimize application performance, test Helm rollback, and practice resource cleanup.

## RBAC security

Created a Kubernetes ServiceAccount, Role, and RoleBinding for a Helm deployment account.

### `helm-rbac.yaml`

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: helm-deployer
  namespace: default

---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: helm-deployer-role
  namespace: default
rules:
  - apiGroups: [""]
    resources: ["pods", "services", "configmaps"]
    verbs: ["get", "list", "watch", "create", "update", "patch"]

  - apiGroups: ["apps"]
    resources: ["deployments", "replicasets"]
    verbs: ["get", "list", "watch", "create", "update", "patch"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: helm-deployer-binding
  namespace: default
subjects:
  - kind: ServiceAccount
    name: helm-deployer
    namespace: default
roleRef:
  kind: Role
  name: helm-deployer-role
  apiGroup: rbac.authorization.k8s.io
```

Verified permissions:

```bash
kubectl auth can-i create deployments \
  --as=system:serviceaccount:default:helm-deployer
```

Result:

```text
yes
```

Tested a restricted action:

```bash
kubectl auth can-i delete pods \
  --as=system:serviceaccount:default:helm-deployer
```

Result:

```text
no
```

Also verified that the ServiceAccount could not create cluster-wide Nodes:

```bash
kubectl auth can-i create nodes \
  --as=system:serviceaccount:default:helm-deployer
```

Result:

```text
no
```

### Security result

I demonstrated the principle of least privilege by allowing the Helm deployment account to manage required application resources while denying more powerful operations.

---

## Performance tuning

Updated the `hello-world` chart to improve availability and resource management.

### `values.yaml`

```yaml
replicaCount: 2

image:
  repository: nginx
  pullPolicy: IfNotPresent
  tag: ""

resources:
  requests:
    cpu: 100m
    memory: 128Mi
  limits:
    cpu: 250m
    memory: 256Mi

livenessProbe:
  httpGet:
    path: /
    port: http
  initialDelaySeconds: 10
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /
    port: http
  initialDelaySeconds: 5
  periodSeconds: 5
```

The deployment template was updated to use the configured resources and health probes.

Validated the chart:

```bash
helm lint .
```

Result:

```text
1 chart(s) linted, 0 chart(s) failed
```

Installed the optimized deployment:

```bash
helm upgrade --install hello-world .
```

Verified the deployment:

```bash
kubectl get deployment hello-world
kubectl get pods
```

The deployment successfully reached:

```text
2/2 Ready
```

The deployment included CPU and memory requests/limits and HTTP liveness/readiness probes.

### Result

I learned how replica counts, resource requests and limits, liveness probes, and readiness probes can improve the reliability and resource management of Kubernetes applications.

---

## Helm upgrade and rollback

Created a new release revision by increasing the replica count to three:

```bash
helm upgrade hello-world . --set replicaCount=3
```

Checked the release history:

```bash
helm history hello-world
```

The history showed revision 2 as the upgraded release.

Rolled the deployment back to revision 1:

```bash
helm rollback hello-world 1
```

Verified the rollback:

```bash
helm history hello-world
kubectl get deployment hello-world
```

The final history showed:

```text
REVISION  STATUS      DESCRIPTION
1         superseded  Install complete
2         superseded  Upgrade complete
3         deployed    Rollback to 1
```

The deployment returned to:

```text
READY 2/2
```

### Result

I learned how Helm keeps release revisions and how `helm rollback` can restore a previous working configuration when a newer deployment needs to be reversed.

---

# Cleanup

After completing the Day 5 exercise, the Helm release and temporary Kubernetes resources were removed, followed by deletion of the GKE cluster.

```bash
helm uninstall hello-world
kubectl delete deployment rbac-test

gcloud container clusters delete helm-day5-cluster \
  --location=us-east1

gcloud container clusters list
```

The cluster was removed after the exercise so that unnecessary cloud resources were not left running.

---

# Skills gained

- Helm fundamentals
- Helm CLI
- Helm repositories
- Helm charts
- Helm values
- Helm releases
- WordPress deployment with Helm
- Custom Helm chart creation
- Helm chart packaging and linting
- Open-source Helm project deployment
- GKE Autopilot
- Kubernetes RBAC
- ServiceAccounts, Roles, and RoleBindings
- Least-privilege permissions
- Kubernetes resource requests and limits
- Liveness probes
- Readiness probes
- Helm upgrade
- Helm history
- Helm rollback
- Kubernetes troubleshooting
- GKE resource cleanup

---

# What new skills, information or understanding have I taken away from this week?

This week, I gained a better understanding of how Helm simplifies the deployment and management of applications on Kubernetes. I learned how to use Helm charts, repositories, values, and releases to deploy applications such as WordPress and Nginx. I also learned how to create and customize my own Helm chart and deploy an open-source chart on Google Kubernetes Engine. I improved my understanding of Kubernetes security by configuring RBAC and restricting permissions for specific resources and actions. I learned how to optimize deployments by adjusting replica counts, CPU and memory resources, and liveness and readiness probes. Finally, I learned how Helm revisions and rollbacks work, allowing me to safely return a deployment to a previous working version.
