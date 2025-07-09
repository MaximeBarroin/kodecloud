There exists a deployment named nginx-deployment; initiate a rollback to the previous revision.
 
 ```bash
 kubectl rollout undo deployment/nginx-deployment
    ```

```bash
kubectl get deployments
kubectl describe deployment nginx-deployment
```

