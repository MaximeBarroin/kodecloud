Create a namespace named dev and deploy a POD within it. Name the pod dev-nginx-pod and use the nginx image with the latest tag. Ensure to specify the tag as nginx:latest.

```bash
kubectl create namespace dev
kubectl run dev-nginx-pod --image=nginx:latest --namespace=dev --labels="app=nginx_app" --overrides='{"spec":{"containers":[{"name":"nginx-container","image":"nginx:latest"}]}}'
```

