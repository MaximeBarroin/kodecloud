An application currently running on the Kubernetes cluster employs the nginx web server. The Nautilus application development team has introduced some recent changes that need deployment. They've crafted an image nginx:1.18 with the latest updates.


Execute a rolling update for this application, integrating the nginx:1.18 image. The deployment is named nginx-deployment.

Ensure all pods are operational post-update.

```bash
kubectl set image deployment/nginx-deployment nginx-container=nginx:1.18 --record
```
After executing the rolling update command, you can verify the status of the deployment and ensure that all pods are running correctly by using the following commands:

```bash
kubectl rollout status deployment/nginx-deployment
kubectl get pods -l app=nginx
```