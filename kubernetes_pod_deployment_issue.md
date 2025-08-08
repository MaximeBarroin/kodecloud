A junior DevOps team member encountered difficulties deploying a stack on the Kubernetes cluster. The pod fails to start, presenting errors. Let's troubleshoot and rectify the issue promptly.


1. There is a pod named webserver, and the container within it is named httpd-container, its utilizing the httpd:latest image. 


Identify and address the issue to ensure the pod is in the running state and the application is accessible.

To troubleshoot the issue with the `webserver` pod and ensure it is running correctly, follow these steps:
```bash
kubectl get pods webserver -o yaml
```
apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotations":{},"labels":{"app":"web-app"},"name":"webserver","namespace":"default"},"spec":{"containers":[{"image":"httpd:latests","name":"httpd-container","volumeMounts":[{"mountPath":"/var/log/httpd","name":"shared-logs"}]},{"command":["sh","-c","while true; do cat /var/log/httpd/access.log /var/log/httpd/error.log; sleep 30; done"],"image":"ubuntu:latest","name":"sidecar-container","volumeMounts":[{"mountPath":"/var/log/httpd","name":"shared-logs"}]}],"volumes":[{"emptyDir":{},"name":"shared-logs"}]}}
  creationTimestamp: "2025-08-08T13:01:36Z"
  labels:
    app: web-app
  name: webserver
  namespace: default
  resourceVersion: "1117"
  uid: 3bcd58d1-dc7d-4935-a613-9a877601fb2d
spec:
  containers:
  - image: httpd:latests
    imagePullPolicy: IfNotPresent
    name: httpd-container
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/log/httpd
      name: shared-logs
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-99zks
      readOnly: true
  - command:
    - sh
    - -c
    - while true; do cat /var/log/httpd/access.log /var/log/httpd/error.log; sleep
      30; done
    image: ubuntu:latest
    imagePullPolicy: Always
    name: sidecar-container
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/log/httpd
      name: shared-logs
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-99zks
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: kodekloud-control-plane
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - emptyDir: {}
    name: shared-logs
  - name: kube-api-access-99zks
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2025-08-08T13:01:36Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2025-08-08T13:01:36Z"
    message: 'containers with unready status: [httpd-container]'
    reason: ContainersNotReady
    status: "False"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2025-08-08T13:01:36Z"
    message: 'containers with unready status: [httpd-container]'
    reason: ContainersNotReady
    status: "False"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2025-08-08T13:01:36Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - image: httpd:latests
    imageID: ""
    lastState: {}
    name: httpd-container
    ready: false
    restartCount: 0
    started: false
    state:
      waiting:
        message: Back-off pulling image "httpd:latests"
        reason: ImagePullBackOff
  - containerID: containerd://d700a5d47d41517d3ffa18a85a2d61de3b72bd7f2bbb5fc19d594ff3162e2cca
    image: docker.io/library/ubuntu:latest
    imageID: docker.io/library/ubuntu@sha256:a08e551cb33850e4740772b38217fc1796a66da2506d312abe51acda354ff061
    lastState: {}
    name: sidecar-container
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2025-08-08T13:01:40Z"
  hostIP: 172.17.0.2
  phase: Pending
  podIP: 10.244.0.5
  podIPs:
  - ip: 10.244.0.5
  qosClass: BestEffort
  startTime: "2025-08-08T13:01:36Z"

The issue with the `webserver` pod is that the `httpd-container` is using an incorrect image name (`httpd:latests` instead of `httpd:latest`). This causes the image pull to fail, leading to the pod being in a `Pending` state.
To fix this, you need to update the pod definition to use the correct image name. You can do this by editing the pod directly or by applying a corrected YAML definition. Here’s how to update the pod:
```bash
kubectl edit pod webserver
```
This command will open the pod definition in your default text editor. Look for the `httpd-container` section and change the image from `httpd:latests` to `httpd:latest`. After making the change, save and exit the editor.
Alternatively, you can delete the existing pod and recreate it with the corrected image:
```bash
kubectl delete pod webserver
kubectl apply -f webserver-pod.yaml
``` 
when it's corrected, you just have to restart the pod to apply the changes:
```bash
kubectl delete pod webserver
```
Then, recreate the pod with the corrected image:
```bash
kubectl apply -f webserver-pod.yaml
```


2. Additionally, there's a sidecar container named sidecar-container using the ubuntu:latest image.
The sidecar container is configured to run a command that continuously reads the logs from the `httpd-container` and outputs them every 30 seconds. This setup is generally correct, but you should ensure that the log directory `/var/log/httpd` exists and is writable by both containers.
If the sidecar container is not functioning as expected, you can check its logs to see if there are any errors:
```bash
kubectl logs webserver -c sidecar-container
```
cat: /var/log/httpd/access.log: No such file or directory

If the sidecar container is unable to read the logs, it may be because the `httpd-container` has not yet created the log files. You can verify this by checking the logs of the `httpd-container`:
```bash
kubectl logs webserver -c httpd-container
```


AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 10.244.0.5. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 10.244.0.5. Set the 'ServerName' directive globally to suppress this message
[Fri Aug 08 13:06:19.450000 2025] [mpm_event:notice] [pid 1:tid 1] AH00489: Apache/2.4.65 (Unix) configured -- resuming normal operations
[Fri Aug 08 13:06:19.450177 2025] [core:notice] [pid 1:tid 1] AH00094: Command line: 'httpd -D FOREGROUND'

If the `httpd-container` is running but not generating logs, you may need to configure the Apache server to log to the specified directory. You can do this by adding a configuration file or modifying the existing one to set the `ErrorLog` and `CustomLog` directives to point to `/var/log/httpd/access.log` and `/var/log/httpd/error.log`, respectively.

To ensure the pod is in the running state and the application is accessible, follow these steps:
1. Correct the image name for the `httpd-container` to `httpd:latest
`.
2. Ensure the log directory `/var/log/httpd` exists and is writable by both containers
3. Configure the Apache server in the `httpd-container` to log to the specified files.
4. Restart the pod to apply the changes.
```bash
kubectl delete pod webserver
kubectl apply -f webserver-pod.yaml
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webserver
  labels:
    app: web-app
spec:
  containers:
    - name: httpd-container
        image: httpd:latest
        volumeMounts:
        - name: shared-logs
        mountPath: /var/log/httpd
    - name: sidecar-container
        image: ubuntu:latest
        command: ["sh", "-c", "while true; do cat /var/log/httpd/access.log /var/log/httpd/error.log; sleep 30; done"]
        volumeMounts:
        - name: shared-logs
        mountPath: /var/log/httpd
    volumes:
    - name: shared-logs
      emptyDir: {}
```bash
kubectl apply -f webserver-pod.yaml
```
or 
```bash
kubectl create -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: webserver
  labels:
    app: web-app
spec:
  containers:
    - name: httpd-container
      image: httpd:latest
      volumeMounts:
      - name: shared-logs
        mountPath: /var/log/httpd
    - name: sidecar-container
      image: ubuntu:latest
      command: ["sh", "-c", "while true; do cat /var/log/httpd/access.log /var/log/httpd/error.log; sleep 30; done"]
      volumeMounts:
      - name: shared-logs
        mountPath: /var/log/httpd
  volumes:
  - name: shared-logs
    emptyDir: {}
EOF
```
 
 launch the pod and verify its status:
```bash
kubectl get pods webserver
```
```bash
kubectl describe pod webserver
```
```bash