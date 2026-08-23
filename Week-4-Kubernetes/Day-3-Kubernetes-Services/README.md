# Day 3 — Kubernetes Services

## Objective
Learn how to expose Kubernetes applications using Services.

## Work completed
- Created a Service manifest.
- Applied the Service to the Kubernetes cluster.
- Connected the Service to the Nginx Pods using labels.
- Exposed the application with NodePort.
- Accessed the application through a browser.
- Practiced troubleshooting application connectivity.

## Service manifest

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
```

With Minikube, obtain the Service URL:

```bash
minikube service nginx-service --url
```

The returned URL was opened in the browser to verify that the Nginx application was accessible.

## Result

This exercise demonstrated how a Kubernetes Service provides a stable endpoint for Pods and how labels connect the Service to the correct workload.

## Key skills

- Kubernetes Services
- NodePort
- Labels and selectors
- Application exposure
- Port mapping
- Browser verification
- Connectivity troubleshooting
