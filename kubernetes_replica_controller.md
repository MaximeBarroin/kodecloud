The Nautilus DevOps team is establishing a ReplicationController to deploy multiple pods for hosting applications that require a highly available infrastructure. Follow the specifications below to create the ReplicationController:


1. Create a ReplicationController using the nginx image with latest tag, and name it nginx-replicationcontroller.

2. Assign labels app as nginx_app, and type as front-end. Ensure the container is named nginx-container and set the replica count to 3.

3. All pods should be running state post-deployment.

Note: The kubectl utility on jump_host is configured to operate with the Kubernetes cluster.

```bash
thor@jump_host ~$ kubectl create -f - <<EOF
apiVersion: v1
kind: ReplicationController
metadata:
  name: nginx-replicationcontroller
spec:
  replicas: 3
  selector:
    app: nginx_app
    type: front-end
  template:
    metadata:
      labels:
        app: nginx_app
        type: front-end
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest
        ports:
        - containerPort: 80
EOF
```