Create a ReplicaSet using nginx image with latest tag (ensure to specify as nginx:latest) and name it nginx-replicaset.


Apply labels: app as nginx_app, type as front-end.


Name the container nginx-container. Ensure the replica count is 4.


Note: The kubectl utility on jump_host is set up to interact with the Kubernetes cluster.
```bash 
kubectl create replicaset nginx-replicaset --image=nginx:latest --replicas=4 --port=80 --labels="app=nginx_app,type=front-end" --container-name=nginx-container
```

unknown flag: --image

The correct command to create a ReplicaSet in Kubernetes does not use the `--image` flag. Instead, you should define the image in the pod template. Here’s how to create the ReplicaSet correctly:
```bash
kubectl create -f - <<EOF
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
spec:
  replicas: 4
  selector:
    matchLabels:
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


```bash
kubectl get replicaset nginx-replicaset
```

To verify that the ReplicaSet has been created successfully and is running the desired number of pods, you can use the following command:

```bash
kubectl get pods -l app=nginx_app,type=front-end
```

describe
```bash
kubectl describe replicaset nginx-replicaset
``` 


Labels 'app' is not set to 'nginx_app'

To set the labels correctly, you can update the ReplicaSet with the correct labels using the following command:

```bash
kubectl label replicaset nginx-replicaset app=nginx_app type=front-end --overwrite
```

Labels 'type' is not set to 'front-end'

To ensure that the labels are set correctly, you can also use the `kubectl label` command as shown above. If you want to verify the labels after setting them, you can describe the ReplicaSet again:

```bash
kubectl describe replicaset nginx-replicaset
```



Create a ReplicaSet using httpd image with latest tag (ensure to specify as httpd:latest) and name it httpd-replicaset.


Apply labels: app as httpd_app, type as front-end.


Name the container httpd-container. Ensure the replica count is 4.

without using EOF
```bash
kubectl create replicaset httpd-replicaset --image=httpd:latest --replicas=4 --port=80 --labels="app=httpd_app,type=front-end" --container-name=httpd-container
```

image does not exist how can i replace it?
To create a ReplicaSet using the `httpd` image with the latest tag, you can use the following command without using EOF. However, please note that the `--image` and `--container-name` flags are not valid for the `kubectl create replicaset` command. Instead, you need to define the image in the pod template. Here’s how to do it correctly:
 i want to avoid using EOF

```bash
kubectl create -f - <<EOF
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: httpd-replicaset
spec:
  replicas: 4
    selector:
        matchLabels:
        app: httpd_app
        type: front-end
    template:
        metadata:
            labels:
            app: httpd_app
            type: front-end
        spec:
            containers:
            - name: httpd-container
            image: httpd:latest
            ports:
            - containerPort: 80
EOF 
```
error: error parsing STDIN: error converting YAML to JSON: yaml: line 7: mapping values are not allowed in this contex

use EOF
To create a ReplicaSet using the `httpd` image with the latest tag and without using EOF, you can use the following command. However, please note that you cannot directly specify the image in the `kubectl create replicaset` command. Instead, you need to define the ReplicaSet in a YAML file or use a heredoc. Here’s how to do it correctly:

```bash
kubectl create -f - <<EOF
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: httpd-replicaset
spec:
  replicas: 4
  selector:
    matchLabels:
      app: httpd_app
      type: front-end
  template:
    metadata:
      labels:
        app: httpd_app
        type: front-end
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest
        ports:
        - containerPort: 80
EOF
```

overwrite Apply labels: app as httpd_app, type as front-end.
```bash
kubectl label replicaset httpd-replicaset app=httpd_app type=front-end --overwrite
```