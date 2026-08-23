# Day 4 — Namespaces and ConfigMaps

## Objective
Learn how Kubernetes organizes resources with Namespaces and manages application configuration with ConfigMaps.

## Work completed
- Created a dedicated Namespace.
- Verified Kubernetes Namespaces.
- Created and applied a ConfigMap.
- Verified ConfigMap data.
- Practiced making ConfigMap values available to a Pod as environment variables.

## Create a Namespace

```bash
kubectl create namespace my-namespace
kubectl get namespaces
```

## ConfigMap manifest

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

## Using ConfigMap values in a Pod

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

## Result

I learned how Namespaces separate and organize Kubernetes resources and how ConfigMaps provide configuration independently from the application image.

## Key skills

- Namespaces
- ConfigMaps
- Resource organization
- Environment variables
- Kubernetes YAML
- Application configuration
