The Nautilus DevOps team is crafting jobs in the Kubernetes cluster. While they're developing actual scripts/commands, they're currently setting up templates and testing jobs with dummy commands. Please create a job template as per details given below:


Create a job named countdown-datacenter.

The spec template should be named countdown-datacenter (under metadata), and the container should be named container-countdown-datacenter

Utilize image debian with latest tag (ensure to specify as debian:latest), and set the restart policy to Never.

Execute the command sleep 5

Note: The kubectl utility on jump_host is set up to operate with the Kubernetes cluster.

```bash
kubectl create job countdown-datacenter --image=debian:latest --restart=Never -- /bin/sh -c "sleep 5"
```

error: unknown flag: --restart

The `kubectl create job` command does not support the `--restart` flag directly. Instead, you can specify the restart policy within the job's YAML definition. Here’s how to create the job with the required specifications:

make the yaml is used with bash
``` bash
cat <<EOF | kubectl apply -f -
apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-datacenter
spec:
  template:
    spec:
      containers:
      - name: container-countdown-datacenter
        image: debian:latest
        command: ["/bin/sh", "-c", "sleep 5"]
      restartPolicy: Never
    backoffLimit: 4
EOF
```bash

Error from server (BadRequest): error when creating "STDIN": Job in version "v1" cannot be handled as a Job: strict decoding error: unknown field "spec.template.backoffLimit"

The error indicates that the `backoffLimit` field is not recognized in the context of the Job specification. The `backoffLimit` field is used to specify the number of retries before considering a job as failed, but it should be placed under the `spec` section of the Job, not under `spec.template`.
Here’s the corrected YAML definition for the job:

```bash
cat <<EOF | kubectl apply -f -
apiVersion: batch/v1
kind: Job
metadata:
    name: countdown-datacenter
spec:
  template:
    spec:
      containers:
      - name: container-countdown-datacenter
        image: debian:latest
        command: ["/bin/sh", "-c", "sleep 5"]
      restartPolicy: Never
EOF
```

verify the job creation by running:

```bash
kubectl get jobs
```

spec template is not named as 'countdown-datacenter'

To ensure that the spec template is named `countdown-datacenter`, you need to set the `metadata` field within the `template` section of the Job definition. Here’s the corrected YAML definition:

```bash
cat <<EOF | kubectl apply -f -
apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-datacenter
spec:
  template:
    metadata:
      name: countdown-datacenter
    spec:
      containers:
      - name: container-countdown-datacenter
        image: debian:latest
        command: ["/bin/sh", "-c", "sleep 5"]
      restartPolicy: Never
EOF
```
Create a job named countdown-xfusion.

The spec template should be named countdown-xfusion (under metadata), and the container should be named container-countdown-xfusion

Utilize image debian with latest tag (ensure to specify as debian:latest), and set the restart policy to Never.

Execute the command sleep 5
```bash
cat <<EOF | kubectl apply -f -
apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-xfusion
spec:
    template:
        metadata:
            name: countdown-xfusion
        spec:
            containers:
            - name: container-countdown-xfusion
              image: debian:latest
              command: ["/bin/sh", "-c", "sleep 5"]
            restartPolicy: Never
EOF
```