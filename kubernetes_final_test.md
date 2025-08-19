The Nautilus application development team aims to test a Pod creation by creating a httpd based Pod on the Kubernetes cluster. The specifications for the same are as follows:


Create a Pod named httpd-test-t1q4 using httpd:alpine3.19 image, it must have a label app: httpd

```bash
kubectl run httpd-test-t1q4 --image=httpd:alpine3.19 --labels="app=httpd"
```
pod/httpd-test-t1q4 created

```bash
kubectl get pods
```

a. Create a pod named pod-httpd-t1q1 utilizing the httpd image, ensuring the use of the latest tag, denoted as httpd:latest (remember to mention tag name while defining the image).

b. Set the app label to httpd_app_t1q1, and name the container as httpd-container-t1q1.

```bash
kubectl run pod-httpd-t1q1 --image=httpd:latest --labels="app=httpd_app_t1q1" --container-name=httpd-container-t1q1
```

error: unknown flag: --container-name

- The --container-name flag is not valid for the kubectl run command. Instead, you can specify the container name in the pod specification.

so we have to use
```yaml
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: pod-httpd-t1q1
  labels:
    app: httpd_app_t1q1
spec:
  containers:
  - name: httpd-container-t1q1
    image: httpd:latest
EOF
```

pod/pod-httpd-t1q1 created

```bash
kubectl get pods
```
NAME              READY   STATUS    RESTARTS   AGE
httpd-test-t1q4   1/1     Running   0          4m25s
pod-httpd-t1q1    1/1     Running   0          7s

```bash
kubectl describe pod pod-httpd-t1q1
```

Name:             pod-httpd-t1q1
Namespace:        default
Priority:         0
Service Account:  default
Node:             kodekloud-control-plane/172.17.0.2
Start Time:       Tue, 19 Aug 2025 13:26:40 +0000
Labels:           app=httpd_app_t1q1
Annotations:      <none>
Status:           Running
IP:               10.244.0.6
IPs:
  IP:  10.244.0.6
Containers:
  httpd-container-t1q1:
    Container ID:   containerd://211e56a997f60d5c2209be58ae1cb3ef9fea10d1073796150131b51217103883
    Image:          httpd:latest
    Image ID:       docker.io/library/httpd@sha256:3198c1839e1a875f8b83803083758a7635f1ae999f0601f30f2f3b8ce2ac99e3
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Tue, 19 Aug 2025 13:26:45 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-s4qk8 (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  kube-api-access-s4qk8:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  2m13s  default-scheduler  Successfully assigned default/pod-httpd-t1q1 to kodekloud-control-plane
  Normal  Pulling    2m13s  kubelet            Pulling image "httpd:latest"
  Normal  Pulled     2m8s   kubelet            Successfully pulled image "httpd:latest" in 4.582902623s (4.582923598s including waiting)
  Normal  Created    2m8s   kubelet            Created container httpd-container-t1q1
  Normal  Started    2m8s   kubelet            Started container httpd-container-t1q1




There is an application deployed on Kubernetes cluster. Recently, the Nautilus application development team developed a new version of the application that needs to be deployed now. As per new updates some new changes need to be made in this existing setup. So update the deployment and service as per details mentioned below:


We already have a deployment named nginx-deployment1-t2q3 and service named nginx-service1-t2q3. Some changes need to be made in this deployment and service, make sure not to delete the deployment and service.

Change the image from nginx:mainline-alpine3.18-slim to nginx:mainline-alpine-slim

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```bash
kubectl get deployments
```
NAME                     READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment1-t2q3   1/1     1            1           51s

```bash
kubectl edit deployment nginx-deployment1-t2q3
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"apps/v1","kind":"Deployment","metadata":{"annotations":{},"labels":{"app":"nginx-app1-t2q3","type":"front-end1-t2q3"},"name":"nginx-deployment1-t2q3","namespace":"default"},"spec":{"replicas":1,"selector":{"matchLabels":{"app":"nginx-app1-t2q3"}},"template":{"metadata":{"labels":{"app":"nginx-app1-t2q3"},"name":"nginx-replica-t2q3"},"spec":{"containers":[{"image":"nginx:mainline-alpine3.18-slim","name":"nginx-container"}]}}}}
  creationTimestamp: "2025-08-19T13:29:13Z"
  generation: 1
  labels:
    app: nginx-app1-t2q3
    type: front-end1-t2q3
  name: nginx-deployment1-t2q3
  namespace: default
  resourceVersion: "1426"
  uid: b8e02863-3798-45f8-86ba-f0ea3739bdd5
spec:
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: nginx-app1-t2q3
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: nginx-app1-t2q3
      name: nginx-replica-t2q3
    spec:
      containers:
      - image: nginx:mainline-alpine3.18-slim
        imagePullPolicy: IfNotPresent
        name: nginx-container
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:
  availableReplicas: 1
  conditions:
  - lastTransitionTime: "2025-08-19T13:29:16Z"
    lastUpdateTime: "2025-08-19T13:29:16Z"
    message: Deployment has minimum availability.
    reason: MinimumReplicasAvailable
    status: "True"
    type: Available
    type: Available
    type: Available
    type: Available
  - lastTransitionTime: "2025-08-19T13:29:13Z"
    lastUpdateTime: "2025-08-19T13:29:16Z"
    message: ReplicaSet "nginx-deployment1-t2q3-6d594d5766" has successfully progressed.
    reason: NewReplicaSetAvailable
    status: "True"

    ```


```bash
kubectl get services
kubectl get pods
kubectl describe nginx-deployment1-t2q3-74d4f4b8f4-ptbsv
```


he Nautilus devops team found that one of the applications that is deployed on the cluster is having some performance issues, they want to make some changes so that it can handle some more traffic. As per new updates some new changes need to be made in this existing setup. So update the deployment as per details mentioned below:


The deployment name is blue-app-t2q5, change its replicas count from 1 to 3.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```bash
kubectl scale deployment blue-app-t2q5 --replicas=3
```

```bash
kubectl get deployments
```


The Nautilus DevOps team aims to deploy microservices on the Kubernetes platform. They've established a Kubernetes cluster and are now focused on configuring namespaces, deployments, and related structures to meet their current needs. Here are the specific details shared by the team:


Create a namespace named dev-t3q3.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

Namespace 'dev-t3q3' exists

```bash
kubectl get namespaces
```

```bash
kubectl create namespace dev-t3q3
kubectl get namespaces
```

The Nautilus DevOps team aims to establish a ReplicationController to deploy multiple pods for hosting applications requiring a highly available infrastructure. Here are the specific details to create the ReplicationController:


Create a ReplicationController using httpd image with latest tag, and name it as httpd-replicationcontroller-t3q5. All pods should be running state after deployment.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

ReplicationController 'httpd-replicationcontroller-t3q5' exists

Image used is 'httpd'

Pods are 'Running'

```bash
kubectl get pods

kubectl create -f - <<EOF
apiVersion: v1
kind: ReplicationController
metadata:
  name: httpd-replicationcontroller-t3q5ku
spec:
  replicas: 3
  selector:
    app: httpd
  template:
    metadata:
      labels:
        app: httpd
    spec:
      containers:
      - name: httpd
        image: httpd:latest
        ports:
        - containerPort: 80
EOF

// Verify the ReplicationController and Pods
kubectl get replicationcontrollers
kubectl get pods
```


Despite diligent efforts, the DevOps team encountered difficulties deploying the orange-app-deployment-t4q6 on the Kubernetes cluster. Regrettably, this app is currently inaccessible. Your prompt attention to resolving this issue is crucial.


The orange-app-deployment-t4q6 is currently facing accessibility issues on the Kubernetes cluster. Your immediate objective is to investigate and rectify this issue to restore the app's functionality and accessibility.

Please prioritize diagnosing the root cause of the deployment issue and apply necessary fixes to ensure the successful deployment and accessibility of the orange-app-deployment-t4q6.

first there is 502 error, cause is service not found

```bash
kubectl get services
```

orange-app-service-t4q6   NodePort    10.96.132.15   <none>        80:31112/TCP   93s

```bash
kubectl describe service orange-app-service-t4q6
```

Name:                     orange-app-service-t4q6
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app=orage-app-t4q6
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.96.132.15
IPs:                      10.96.132.15
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  31112/TCP
Endpoints:                <none>
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>


It seems that the selector for the service is incorrect. The service is looking for pods with the label `app=orage-app-t4q6`, but the correct label should be `app=orange-app-t4q6`. This typo is likely the cause of the 502 error, as the service cannot find any endpoints to route traffic to.

To fix this issue, you need to update the service's selector to match the correct label for the pods. You can do this by editing the service definition and applying the changes.

```bash
kubectl edit service orange-app-service-t4q6
```

In the editor that opens, change the selector from `app=orage-app-t4q6` to `app=orange-app-t4q6`, then save and exit the editor.

After making this change, verify that the service now has endpoints by running:

```bash
kubectl get endpoints orange-app-service-t4q6
```
orange-app-service-t4q6   10.244.0.14:80   4m22s


he Nautilus DevOps team successfully deployed a Redis application on the Kubernetes cluster last week. However, this morning, modifications were being made to the existing setup by one of our team members. Unfortunately, errors occurred during these changes, causing the application to go offline.


The deployment named redis-deployment-t4q2 is currently experiencing issues, resulting in the pods being unavailable. Your task is to troubleshoot this issue and restore the deployment to ensure the pods are in a running state again.

Please proceed with diagnosing the problem and implementing the necessary fixes to bring the redis-deployment-t4q2 back to a functional state.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

firstly, check the status of the pods in the redis-deployment-t4q2 deployment:

```bash
kubectl get pods
```

redis-deployment-t4q2-6669965f8b-7ntfl        0/1     ContainerCreating   0          57s

we can check the events for the pod to get more information about why it's stuck in the ContainerCreating state:

```bash
kubectl describe pod redis-deployment-t4q2-6669965f8b-7ntfl
```

Name:             redis-deployment-t4q2-6669965f8b-7ntfl
Namespace:        default
Priority:         0
Service Account:  default
Node:             kodekloud-control-plane/172.17.0.2
Start Time:       Tue, 19 Aug 2025 13:53:41 +0000
Labels:           app=redis
                  pod-template-hash=6669965f8b
Annotations:      <none>
Status:           Pending
IP:               
IPs:              <none>
Controlled By:    ReplicaSet/redis-deployment-t4q2-6669965f8b
Containers:
  redis-container:
    Container ID:   
    Image:          redis:alpin
    Image ID:       
    Port:           6379/TCP
    Host Port:      0/TCP
    State:          Waiting
      Reason:       ContainerCreating
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:        300m
    Environment:  <none>
    Mounts:
      /redis-master from config (rw)
      /redis-master-data from data (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-bthrx (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             False 
  ContainersReady   False 
  PodScheduled      True 
Volumes:
  data:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  config:
    Type:      ConfigMap (a volume populated by a ConfigMap)
    Name:      redis-conig-t4q2
    Optional:  false
  kube-api-access-bthrx:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason       Age                 From               Message
  ----     ------       ----                ----               -------
  Normal   Scheduled    101s                default-scheduler  Successfully assigned default/redis-deployment-t4q2-6669965f8b-7ntfl to kodekloud-control-plane
  Warning  FailedMount  37s (x8 over 100s)  kubelet            MountVolume.SetUp failed for volume "config" : configmap "redis-conig-t4q2" not found



It seems that the ConfigMap "redis-conig-t4q2" is not found, which is causing the pod to be stuck in the ContainerCreating state. We need to check if the ConfigMap exists and if it is correctly named.

Let's list all ConfigMaps in the default namespace:

```bash
kubectl get configmaps
```

redis-config-t4q2   2      2m57s

we need to update the deployment to use the correct ConfigMap name.

```bash
kubectl edit deployment redis-deployment-t4q2
```

In the editor, change the ConfigMap name from "redis-conig-t4q2" to "redis-config-t4q2" and save the changes.

After updating the deployment, we can check the status of the pods again:

```bash
kubectl get pods
```

redis-deployment-t4q2-5c9c85687d-kpq6h        0/1     ErrImagePull        0          31s

```bash
kubectl describe pod redis-deployment-t4q2-5c9c85687d-kpq6h
```

redis image was alpin and not alpine so it does not work.

after editing again it works



One of the services named service-t5q6 needs some updates, as during deployment some required labels were missing from this service. Make changes to this service as per details mentioned below:


Update service-t5q6 service to add a label component: front-end-t5q6.

```bash
kubectl label service service-t5q6 component=front-end-t5q6
kubectl get services
kubectl describe service service-t5q6
```
it's ok we updated the service with the correct label.



An application was deployed on the Kubernetes cluster, the deployment name is deployment-t5q5. There is a service named service-t5q5 associated with this deployment. We need to make below changes in this service.


Update service-t5q5 service to an another match label component: front-end-t5q5.

```bash
kubectl label service service-t5q5 component=front-end-t5q5
```
service/service-t5q5 not labeled

so we need to add label with a different way

```bash
kubectl patch service service-t5q5 -p '{"metadata":{"labels":{"component":"front-end-t5q5"}}}'
```

```bash
kubectl get services
kubectl describe service service-t5q5
```
we can see the new label front end t5q5
