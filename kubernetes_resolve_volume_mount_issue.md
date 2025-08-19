We encountered an issue with our Nginx and PHP-FPM setup on the Kubernetes cluster this morning, which halted its functionality. Investigate and rectify the issue:



The pod name is nginx-phpfpm and configmap name is nginx-config. Identify and fix the problem.


Once resolved, copy /home/thor/index.php file from the jump host to the nginx-container within the nginx document root. After this, you should be able to access the website using Website button on the top bar.


Note: The kubectl utility on jump_host is configured to operate with the Kubernetes cluster.

```bash
thor@jump_host ~$ kubectl get pods
NAME           READY   STATUS    RESTARTS   AGE
nginx-phpfpm   2/2     Running   0          116s

thor@jump_host ~$ kubectl get configmap
kube-root-ca.crt   1      13m
nginx-config       1      2m17s

thor@jump_host ~$ kubectl describe pod nginx-phpfpm

```
```yaml
Name:             nginx-phpfpm
Namespace:        default
Priority:         0
Service Account:  default
Node:             kodekloud-control-plane/172.17.0.2
Start Time:       Tue, 19 Aug 2025 09:16:22 +0000
Labels:           app=php-app
Annotations:      <none>
Status:           Running
IP:               10.244.0.5
IPs:
  IP:  10.244.0.5
Containers:
  php-fpm-container:
    Container ID:   containerd://8bc128d0a11fc2350593faa60c70db7ace934fc33a12d04953b511278e9e3212
    Image:          php:7.2-fpm-alpine
    Image ID:       docker.io/library/php@sha256:2e2d92415f3fc552e9a62548d1235f852c864fcdc94bcf2905805d92baefc87f
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Tue, 19 Aug 2025 09:16:26 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /usr/share/nginx/html from shared-files (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-hxgt2 (ro)
  nginx-container:
    Container ID:   containerd://fdb2d6edd0750811d1af69e8f271cb54eafd181912031b32fb321e7967d81e47
    Image:          nginx:latest
    Image ID:       docker.io/library/nginx@sha256:33e0bbc7ca9ecf108140af6288c7c9d1ecc77548cbfd3952fd8466a75edefe57
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Tue, 19 Aug 2025 09:16:33 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /etc/nginx/nginx.conf from nginx-config-volume (rw,path="nginx.conf")
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-hxgt2 (ro)
      /var/www/html from shared-files (rw)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  shared-files:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  nginx-config-volume:
    Type:      ConfigMap (a volume populated by a ConfigMap)
    Name:      nginx-config
    Optional:  false
  kube-api-access-hxgt2:
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
  Normal  Scheduled  2m11s  default-scheduler  Successfully assigned default/nginx-phpfpm to kodekloud-control-plane
  Normal  Pulling    2m10s  kubelet            Pulling image "php:7.2-fpm-alpine"
  Normal  Pulled     2m8s   kubelet            Successfully pulled image "php:7.2-fpm-alpine" in 2.921432589s (2.921449785s including waiting)
  Normal  Created    2m7s   kubelet            Created container php-fpm-container
  Normal  Started    2m7s   kubelet            Started container php-fpm-container
  Normal  Pulling    2m7s   kubelet            Pulling image "nginx:latest"
  Normal  Pulled     2m     kubelet            Successfully pulled image "nginx:latest" in 7.002839084s (7.002856778s including waiting)
  Normal  Created    2m     kubelet            Created container nginx-container
  Normal  Started    2m     kubelet            Started container nginx-container
  ```

  


Next, we need to check the nginx configuration file in the configmap.

```bash
kubectl get configmap nginx-config -o yaml
```

```yaml
apiVersion: v1
data:
  nginx.conf: |
    events {
    }
    http {
      server {
        listen 8099 default_server;
        listen [::]:8099 default_server;

        # Set nginx to serve files from the shared volume!
        root /var/www/html;
        index  index.html index.htm index.php;
        server_name _;
        location / {
          try_files $uri $uri/ =404;
        }
        location ~ \.php$ {
          include fastcgi_params;
          fastcgi_param REQUEST_METHOD $request_method;
          fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
          fastcgi_pass 127.0.0.1:9000;
        }
      }
    }
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"nginx.conf":"events {\n}\nhttp {\n  server {\n    listen 8099 default_server;\n    listen [::]:8099 default_server;\n\n    # Set nginx to serve files from the shared volume!\n    root /var/www/html;\n    index  index.html index.htm index.php;\n    server_name _;\n    location / {\n      try_files $uri $uri/ =404;\n    }\n    location ~ \\.php$ {\n      include fastcgi_params;\n      fastcgi_param REQUEST_METHOD $request_method;\n      fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;\n      fastcgi_pass 127.0.0.1:9000;\n    }\n  }\n}\n"},"kind":"ConfigMap","metadata":{"annotations":{},"name":"nginx-config","namespace":"default"}}
  creationTimestamp: "2025-08-19T09:16:22Z"
  name: nginx-config
  namespace: default
  resourceVersion: "1617"
  uid: 65babb55-d86a-4cef-83c5-e5404468c721
```

next  , we need to change the port from 8099 to 80 in the nginx configuration file.

```bash
kubectl edit configmap nginx-config
```

```yaml
apiVersion: v1
data:
  nginx.conf: |
    events {
    }
    http {
      server {
        listen 80 default_server;
        listen [::]:80 default_server;

        # Set nginx to serve files from the shared volume!
        root /var/www/html;
        index  index.html index.htm index.php;
        server_name _;
        location / {
          try_files $uri $uri/ =404;
        }
        location ~ \.php$ {
          include fastcgi_params;
          fastcgi_param REQUEST_METHOD $request_method;
          fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
          fastcgi_pass 127.0.0.1:9000;
        }
      }
    }
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"nginx.conf":"events {\n}\nhttp {\n  server {\n    listen 80 default_server;\n    listen [::]:80 default_server;\n\n    # Set nginx to serve files from the shared volume!\n    root /var/www/html;\n    index  index.html index.htm index.php;\n    server_name _;\n    location / {\n      try_files $uri $uri/ =404;\n    }\n    location ~ \\.php$ {\n      include fastcgi_params;\n      fastcgi_param REQUEST_METHOD $request_method;\n      fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;\n      fastcgi_pass 127.0.0.1:9000;\n    }\n  }\n}\n"},"kind":"ConfigMap","metadata":{"annotations":{},"name":"nginx-config","namespace":"default"}}
  creationTimestamp: "2025-08-19T09:16:22Z"
  name: nginx-config
  namespace: default
  resourceVersion: "1617"
  uid: 65babb55-d86a-4cef-83c5-e5404468c721
```

After editing the configmap, we need to restart the nginx-phpfpm pod to apply the changes.

```bash
kubectl rollout restart deployment nginx-phpfpm
```
Error from server (NotFound): deployments.apps "nginx-phpfpm" not found


Once resolved, copy /home/thor/index.php file from the jump host to the nginx-container within the nginx document root. After this, you should be able to access the website using Website button on the top bar.

```bash
kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html/index.php
```
Defaulted container "php-fpm-container" out of: php-fpm-container, nginx-container

so we need to specify the container name when copying the file.

```bash
kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html/index.php -c php-fpm-container
kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html/index.php -c nginx-container
```

---

## Summary

### Problem Description
The Nginx and PHP-FPM setup on the Kubernetes cluster was non-functional due to configuration issues that prevented website accessibility.

### Root Cause Analysis
**Primary Issue**: Nginx was configured to listen on port **8099** instead of the standard HTTP port **80**, making the website inaccessible through the standard web interface.

### Architecture Overview
- **Pod**: `nginx-phpfpm` (multi-container pod)
- **Containers**: 
  - `php-fpm-container` (php:7.2-fpm-alpine)
  - `nginx-container` (nginx:latest)
- **ConfigMap**: `nginx-config` containing nginx configuration
- **Volumes**: 
  - `shared-files` (EmptyDir) mounted at `/var/www/html` and `/usr/share/nginx/html`
  - `nginx-config-volume` (ConfigMap) mounted at `/etc/nginx/nginx.conf`

### Troubleshooting Steps Performed

1. **Initial Assessment**
   ```bash
   kubectl get pods        # Verified pod status (2/2 Running)
   kubectl get configmap   # Confirmed ConfigMap exists
   kubectl describe pod nginx-phpfpm  # Analyzed pod configuration
   ```

2. **Configuration Analysis**
   ```bash
   kubectl get configmap nginx-config -o yaml  # Examined nginx configuration
   ```
   - **Issue Found**: Listen ports set to 8099 instead of 80

3. **Configuration Fix**
   ```bash
   kubectl edit configmap nginx-config
   ```
   - **Changed**: `listen 8099` → `listen 80`
   - **Changed**: `listen [::]:8099` → `listen [::]:80`

4. **Pod Restart Attempt**
   ```bash
   kubectl rollout restart deployment nginx-phpfpm
   ```
   - **Result**: Failed (nginx-phpfpm is a pod, not a deployment)
   - **Note**: Would need `kubectl delete pod nginx-phpfpm` to restart

5. **Application Deployment**
   ```bash
   kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html/index.php
   ```
   - **Issue**: Multi-container pod required container specification
   - **Solution**: Used `-c` flag to target specific containers

### Final Configuration
- ✅ **Port Fix**: Nginx now listens on standard port 80
- ✅ **File Deployment**: index.php copied to both containers
- ✅ **Volume Mount**: Sha  

### Key Learning Points
1. **Multi-container Pods**: Always specify container name with `-c` flag for file operations
2. **Resource Types**: Distinguish between pods and deployments for restart operations
3. **Port Configuration**: Standard web services should use port 80 for accessibility
4. **Volume Sharing**: EmptyDir volumes enable file sharing between containers in same pod

### Expected Outcome
With the port corrected to 80 and index.php deployed, the website should now be accessible via the "Website" button, with nginx serving PHP files through PHP-FPM successfully.

