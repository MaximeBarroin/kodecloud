An issue has arisen with a static website running in a container named nautilus on App Server 1. To resolve the issue, investigate the following details:



Check if the container's volume /usr/local/apache2/htdocs is correctly mapped with the host's volume /var/www/html.

Verify that the website is accessible on host port 8080 on App Server 1. Confirm that the command curl http://localhost:8080/ works on App Server 1.

stapp01	172.16.238.10	stapp01.stratos.xfusioncorp.com	tony	Ir0nM@n	Nautilus App 1

````bash
docker inspect nautilus
```

[
    {
        "Id": "5bd50c47e15734312a2c22f10885bc8002f56e23438f631cc6352e3da5f2d75c",
        "Created": "2025-08-05T08:39:37.14984258Z",
        "Path": "httpd-foreground",
        "Args": [],
        "State": {
            "Status": "exited",
            "Running": false,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 0,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2025-08-05T08:39:40.047472782Z",
            "FinishedAt": "2025-08-05T08:39:41.231323878Z"
        },
        "Image": "sha256:5bdbc621ec089f8137cf0fdd49caa16748854c8c72739e794d1c2c9ab88dfed7",
        "ResolvConfPath": "/var/lib/docker/containers/5bd50c47e15734312a2c22f10885bc8002f56e23438f631cc6352e3da5f2d75c/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/5bd50c47e15734312a2c22f10885bc8002f56e23438f631cc6352e3da5f2d75c/hostname",
        "HostsPath": "/var/lib/docker/containers/5bd50c47e15734312a2c22f10885bc8002f56e23438f631cc6352e3da5f2d75c/hosts",
        "LogPath": "/var/lib/docker/containers/5bd50c47e15734312a2c22f10885bc8002f56e23438f631cc6352e3da5f2d75c/5bd50c47e15734312a2c22f10885bc8002f56e23438f631cc6352e3da5f2d75c-json.log",
        "Name": "/nautilus",
        "RestartCount": 0,
        "Driver": "vfs",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": [
                "/var/www/html:/usr/local/apache2/htdocs/"
            ],
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "bridge",
            "PortBindings": {
                "80/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "8080"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                0,
                0
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
        "Mounts": [
            {
                "Type": "bind",
                "Source": "/var/www/html",
                "Destination": "/usr/local/apache2/htdocs",
                "Mode": "",
                "RW": true,
                "Propagation": "rprivate"
            }
        ],
        "Config": {
            "Hostname": "5bd50c47e157",
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
                "PATH=/usr/local/apache2/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "HTTPD_PREFIX=/usr/local/apache2",
                "HTTPD_VERSION=2.4.65",
                "HTTPD_SHA256=58b8be97d9940ec17f7656c0c6b9f41b618aac468b894b534148e3296c53b8b3",
                "HTTPD_PATCHES="
            ],
            "Cmd": [
                "httpd-foreground"
            ],
            "Image": "httpd",
            "Volumes": null,
            "WorkingDir": "/usr/local/apache2",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {},
            "StopSignal": "SIGWINCH"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "ccd50540e03558e6f6eac02c4aa4d54ab490d8bf90e6d6af835e0006d1ae7ff3",
            "SandboxKey": "/var/run/docker/netns/ccd50540e035",
            "Ports": {},
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "",
            "Gateway": "",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "",
            "IPPrefixLen": 0,
            "IPv6Gateway": "",
            "MacAddress": "",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "",
                    "NetworkID": "fa4990eb8457cbfbe46efdadb605da47757fa3696778c3bce3c05f0f8aef99e7",
                    "EndpointID": "",
                    "Gateway": "",
                    "IPAddress": "",
                    "IPPrefixLen": 0,
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

To troubleshoot the static website running in the container named nautilus, follow these steps:
1. **Check Volume Mapping**: Ensure that the volume `/usr/local/apache2/htdocs` in the container is correctly mapped to the host's volume `/var/www/html`. The `docker inspect` output shows that this mapping is correctly set up.
2. **Verify Website Accessibility**: Check if the website is accessible on host port 8080 on App Server 1. You can do this by running the following command on App Server 1:

```bash
curl -I http://localhost:8080
```
Failed to connect to localhost port 8080: Connection refused

This indicates that the website is not accessible on port 8080. To resolve this, you can try the following steps:   
3. **Restart the Container**: Sometimes, simply restarting the container can resolve issues. Use the following command to restart the nautilus container:

```bash
docker restart nautilus
```

