Create a pod named httpd-pod with a container named httpd-container. Use the httpd image with the latest tag (specify as httpd:latest). Set the following resource limits:

Requests: Memory: 15Mi, CPU: 100m

Limits: Memory: 20Mi, CPU: 100m

```bash
kubectl run httpd-pod --image=httpd:latest --overrides='{"spec":{"containers":[{"name":"httpd-container","image":"httpd:latest","resources":{"requests":{"memory":"15Mi","cpu":"100m"},"limits":{"memory":"20Mi","cpu":"100m"}}}]}}'
```
or create a YAML file and apply it:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
    resources:
      requests:
        memory: "15Mi"
        cpu: "100m"
      limits:
        memory: "20Mi"
        cpu: "100m"
```

Then apply it using:

```bash
kubectl apply -f httpd-pod.yaml
```
 verify the pod creation with:
```bash
kubectl get pods
```
 
verify the pod details with:
```bash
kubectl describe pod httpd-pod
```
