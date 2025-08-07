On Application Server 2 create a container named nginx_2 using image nginx with alpine tag and make sure container is in running state.

stapp02	172.16.238.11	stapp02.stratos.xfusioncorp.com	steve	Am3ric@	Nautilus App 2

```bash
ssh steve@stapp02.stratos.xfusioncorp.com
```
password: Am3ric@

```bash
sudo su -
docker run -d --name nginx_2 nginx:alpine
```
To verify that the container is running, you can use the following command:

```bash
docker ps
```
This command will list all running containers, and you should see `nginx_2` in the output with its status as "Up".
If you want to check the logs of the container to ensure it started correctly, you can use
```bash
docker logs nginx_2
```
the command:

```bash
docker inspect nginx_2
```
This command will provide detailed information about the container, including its configuration, state, and any mounted volumes. You should see that the container is in a "running" state and that it has been created from the `nginx:alpine` image.
```json
[
    {
        "Id": "4e7731c382e5b1a1c05a45055b5a7d106aadbfa675c78be58e6813902f499c17",
        "Created": "2025-08-06T14:42:30.753944635Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 2203,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2025-08-06T14:42:32.442990508Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:d6adbc7fd47ec44ff968ea826c84f41d0d5a70a2dce4bd030757f9b7fe9040b8",
        "ResolvConfPath": "/var/lib/docker/containers/4e7731c382e5b1a1c05a45055b5a7d106aadbfa675c78be58e6813902f499c17/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/4e7731c382e5b1a1c05a45055b5a7d106aadbfa675c78be58e6813902f499c17/hostname",
        "HostsPath": "/var/lib/docker/containers/4e7731c382e5b1a1c05a45055b5a7d106aadbfa675c78be58e6813902f499c17/hosts",
        "LogPath": "/var/lib/docker/containers/4e7731c382e5b1a1c05a45055b5a7d106aadbfa675c78be58e6813902f499c17/4e7731c382e5b1a1c05a45055b5a7d106aadbfa675c78be58e6813902f499c17-json.log",
        "Name": "/nginx_2",
        "RestartCount": 0,
        "Driver": "vfs",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "bridge",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                31,
                89
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": [],
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware",
                "/sys/devices/virtual/powercap"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": null,
            "Name": "vfs"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "4e7731c382e5",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.29.0",
                "PKG_RELEASE=1",
                "DYNPKG_RELEASE=1",
                "NJS_VERSION=0.9.0",
                "NJS_RELEASE=1"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx:alpine",
            "Volumes": null,
            "WorkingDir": "/",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "6722925b02b0d3eafb14e816eedad8ab11e2a26d14e2fb7580c65034ff6e30c1",
            "SandboxKey": "/var/run/docker/netns/6722925b02b0",
            "Ports": {
                "80/tcp": null
            },
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "e28427ec2f87706ef1cffb66e95a8149301101d461c2dac2462d1e4ef2b71dc1",
            "Gateway": "172.12.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.12.0.2",
            "IPPrefixLen": 24,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:0c:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "02:42:ac:0c:00:02",
                    "NetworkID": "f6b6bfba11319b2719892b11f719ec5f71ca799a2b6fd474c32e6c26ea0c963d",
                    "EndpointID": "e28427ec2f87706ef1cffb66e95a8149301101d461c2dac2462d1e4ef2b71dc1",
                    "Gateway": "172.12.0.1",
                    "IPAddress": "172.12.0.2",
                    "IPPrefixLen": 24,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DriverOpts": null,
                    "DNSNames": null
                }
            }
        }
    }
]
``` 

The Nautilus team wants to create a debug container on Application Server 2. However, they had some specific requirements related to the CMD. Please complete the task as per details given below:


a. On Application Server 2 create a container named debug_2 using image ubuntu/apache2:latest.

b. Overwrite the default CMD with command sleep 1000.

c. Make sure the container is in running state.

```bash
ssh user@application_server_2
docker run -d --name debug_2 ubuntu/apache2:latest sleep 1000
```

To verify that the container is running, you can use the following command:

```bash
docker ps
docker inspect debug_2
```
This command will provide detailed information about the container, including its configuration, state, and any mounted volumes. You should see that the container is in a "running" state and that it has been created from the `ubuntu/apache2:latest` image with the CMD overwritten to `sleep 1000`.
```json
[
    {
        "Id": "4e7731c382e5b1a1c05a45055b5a7d106aadbfa675c78be58e6813902f499c17",
        "Created": "2025-08-06T14:42:30.753944635Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 2203,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2025-08-06T14:42:32.442990508Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:d6adbc7fd47ec44ff968ea826c84f41d0d5a70a2dce4bd030757f9b7fe9040b8",
        "ResolvConfPath": "/var/lib/docker/containers/4e7731c382e5b1a1c05a45055b5a7d106aadbfa675c78be58e6813902f499c17/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/4e7731c382e5b1a1c05a45055b5a7d106aadbfa675c78be58e6813902f499c17/hostname",
        "HostsPath": "/var/lib/docker/containers/4e7731c382e5b1a1c05a45055b5a7d106aadbfa675c78be58e6813902f499c17/hosts",
        "LogPath": "/var/lib/docker/containers/4e7731c382e5b1a1c05a45055b5a7d106aadbfa675c78be58e6813902f499c17/4e7731c382e5b1a1c05a45055b5a7d106aadbfa675c78be58e6813902f499c17-json.log",
        "Name": "/nginx_2",
        "RestartCount": 0,
        "Driver": "vfs",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "bridge",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                31,
                89
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": [],
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware",
                "/sys/devices/virtual/powercap"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": null,
            "Name": "vfs"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "4e7731c382e5",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.29.0",
                "PKG_RELEASE=1",
                "DYNPKG_RELEASE=1",
                "NJS_VERSION=0.9.0",
                "NJS_RELEASE=1"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx:alpine",
            "Volumes": null,
            "WorkingDir": "/",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "6722925b02b0d3eafb14e816eedad8ab11e2a26d14e2fb7580c65034ff6e30c1",
            "SandboxKey": "/var/run/docker/netns/6722925b02b0",
            "Ports": {
                "80/tcp": null
            },
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "e28427ec2f87706ef1cffb66e95a8149301101d461c2dac2462d1e4ef2b71dc1",
            "Gateway": "172.12.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.12.0.2",
            "IPPrefixLen": 24,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:0c:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "02:42:ac:0c:00:02",
                    "NetworkID": "f6b6bfba11319b2719892b11f719ec5f71ca799a2b6fd474c32e6c26ea0c963d",
                    "EndpointID": "e28427ec2f87706ef1cffb66e95a8149301101d461c2dac2462d1e4ef2b71dc1",
                    "Gateway": "172.12.0.1",
                    "IPAddress": "172.12.0.2",
                    "IPPrefixLen": 24,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DriverOpts": null,
                    "DNSNames": null
                }
            }
        }
    }
]
```

The Nautilus DevOps team has some confidential data present on App Server 2 in Stratos Datacenter. There is a container ubuntu_latest running on the same server. We received a request to copy some of the data from the docker host to the container. Below are more details about the task:



On App Server 2 in Stratos Datacenter copy an encrypted file /tmp/nautilus.txt.gpg from docker host to ubuntu_latest container (running on same server) in /opt/ location (create this location if doesn't exit). Please do not try to modify this file in any way.

stapp02
    docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/opt/nautilus.txt.gpg
```bash
ssh stapp02.stratos.xfusioncorp.com
```

```bash
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/opt/nautilus.txt.gpg
```

```bash
docker exec -it ubuntu_latest ls -l /opt/nautilus.txt.gpg
```

```bash
docker exec -it ubuntu_latest du -h /opt/nautilus.txt.gpg
```


On App Server 2 in Stratos Datacenter copy an encrypted file /tmp/test.txt.gpg from development_3 docker container to the docker host in /tmp location. Please do not try to modify this file in any way.

```bash
ssh stapp02.stratos.xfusioncorp.com
```

```bash
docker cp development_3:/tmp/test.txt.gpg /tmp/test.txt.gpg
```

```bash
ls -l /tmp/test.txt.gpg
```

```bash
du -h /tmp/test.txt.gpg
```
[root@stapp02 ~]# docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/opt/nautilus.txt.gpg
Successfully copied 2.05kB to ubuntu_latest:/opt/nautilus.txt.gpg
[root@stapp02 ~]# docker exec -it ubuntu_latest ls -l /opt/nautilus.txt.gpg
-rw-r--r-- 1 root root 105 Aug  6 14:47 /opt/nautilus.txt.gpg
[root@stapp02 ~]# docker exec -it ubuntu_latest du -h /opt/nautilus.txt.gpg
4.0K    /opt/nautilus.txt.gpg
[root@stapp02 ~]# docker cp development_3:/tmp/test.txt.gpg /tmp/test.txt.gpg

-bash: ocker: command not found
[root@stapp02 ~]# docker cp development_3:/tmp/test.txt.gpg /tmp/test.txt.gpg
Successfully copied 2.05kB to /tmp/test.txt.gpg
[root@stapp02 ~]# ls -l /tmp/test.txt.gpg
-rw-r--r-- 1 root root 98 Aug  6 14:50 /tmp/test.txt.gpg
[root@stapp02 ~]# du -h /tmp/test.txt.gpg
4.0K    /tmp/test.txt.gpg

On App Server 2 in Stratos Datacenter look for the docker images with size more than 100MB, delete all such docker images.

```bash
ssh stapp02.stratos.xfusioncorp.com
```

```bash
docker images --format "{{.Repository}}:{{.Tag}} {{.Size}}" | awk '$2 ~ /[0-9]+M/ && $2+0 > 100 {print $1}' | xargs -r docker rmi
```

There is a docker image on Application Server 2 in Stratos DC. This image needs to be retagged as per details given below:


Re-tag the nginx:mainline-alpine3.18-slim image as nginx:nautilus

```bash
ssh stapp02.stratos.xfusioncorp.com
```

```bash
docker tag nginx:mainline-alpine3.18-slim nginx:nautilus
```

```bash
docker images
```

remove the old tag of the image nginx:mainline-alpine3.18-slim

```bash
docker rmi nginx:mainline-alpine3.18-slim
```

```bash
docker images
```
[root@stapp02 ~]# docker tag nginx:mainline-alpine3.18-slim nginx:nautilus
[root@stapp02 ~]# docker ps
CONTAINER ID   IMAGE                   COMMAND                  CREATED          STATUS          PORTS     NAMES
7c499ec6d34c   httpd:alpine            "httpd-foreground"       5 minutes ago    Up 5 minutes    80/tcp    development_3
b84d3b423f16   ubuntu/apache2:latest   "apache2-foreground"     8 minutes ago    Up 8 minutes    80/tcp    ubuntu_latest
c525b3d7eb64   ubuntu/apache2:latest   "sleep 1000"             10 minutes ago   Up 10 minutes   80/tcp    debug_2
4e7731c382e5   nginx:alpine            "/docker-entrypoint.…"   13 minutes ago   Up 13 minutes   80/tcp    nginx_2
[root@stapp02 ~]# docker images
REPOSITORY       TAG                        IMAGE ID       CREATED         SIZE
httpd            alpine                     413c1ac706f8   13 days ago     64.5MB
nginx            alpine                     d6adbc7fd47e   6 weeks ago     52.4MB
ubuntu/apache2   latest                     511444d2ab5c   3 months ago    194MB
nginx            mainline-alpine3.18-slim   2fd4619865c4   17 months ago   11.9MB
nginx            nautilus                   2fd4619865c4   17 months ago   11.9MB
[root@stapp02 ~]# docker rmi nginx:mainline-alpine3.18-slim
Untagged: nginx:mainline-alpine3.18-slim
[root@stapp02 ~]# docker images
REPOSITORY       TAG        IMAGE ID       CREATED         SIZE
httpd            alpine     413c1ac706f8   13 days ago     64.5MB
nginx            alpine     d6adbc7fd47e   6 weeks ago     52.4MB
ubuntu/apache2   latest     511444d2ab5c   3 months ago    194MB
nginx            nautilus   2fd4619865c4   17 months ago   11.9MB
[root@stapp02 ~]# 

Create a new network named mysql-network using the bridge driver. Allocate subnet 182.18.0.0/24, configure Gateway 182.18.0.1

```bash
ssh stapp02.stratos.xfusioncorp.com
```

```bash
docker network create --driver bridge --subnet 182.18.0.0/24 --gateway 182.18.0.1 mysql-network
```

```bash
docker network ls
```
[root@stapp02 ~]# docker network create --driver bridge --subnet 182.18.0.0/24 --gateway 182.18.0.1 mysql-network
16e1ab6f9d7fd7f53e044a2fa860aa5a29e24770f73814ff2e62b148462e0b1d
[root@stapp02 ~]# docker network ls
NETWORK ID     NAME            DRIVER    SCOPE
f6b6bfba1131   bridge          bridge    local
dff006ad8062   host            host      local
16e1ab6f9d7f   mysql-network   bridge    local
fd62be1d619c   none            null      

The Nautilus DevOps team is planning to do some cleanup on App Server 2 in Stratos Datacenter, some old and unused docker networks need to be deleted. Find below more details:


Delete a docker network named php-network from App Server 2 in Stratos Datacenter.
```bash
ssh stapp02.stratos.xfusioncorp.com
```

```bash
docker network rm php-network
```

```bash
docker network ls
```



There is a static website running within a container named nautilus, this container is running on App Server 2. Suddenly, we started facing some issues with the static website on App Server 2. Look into the issue to fix the same, you can find more details below:


a. Container's volume /usr/local/apache2/htdocs is mapped with the host volume /var/www/html.

b. The website should run on host port 8080 on App Server 2 i.e command curl http://localhost:8080/ should work on App Server 2.

```bash
ssh stapp02.stratos.xfusioncorp.com
```

```bash
docker inspect nautilus
```

```bash
curl -I http://localhost:8080
```

```bash
docker restart nautilus
```

```bash

