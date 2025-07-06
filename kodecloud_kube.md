 Create a pod named pod-nginx using the nginx image with the latest tag. Ensure to specify the tag as nginx:latest.

Set the app label to nginx_app, and name the container as nginx-container.

Note: The kubectl utility on jump_host is configured to operate with the Kubernetes cluster.


Answer:
```bash
kubectl run pod-nginx --image=nginx:latest --labels="app=nginx_app" --overrides='{"spec":{"containers":[{"name":"nginx-container","image":"nginx:latest"}]}}'
```

or create a YAML file and apply it:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-nginx
  labels:
    app: nginx_app
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
```

Then apply it using:

```bash     
kubectl apply -f pod-nginx.yaml
```

