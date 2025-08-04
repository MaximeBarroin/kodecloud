The Nautilus DevOps team is setting up recurring tasks on different schedules. Currently, they're developing scripts to be executed periodically. To kickstart the process, they're creating cron jobs in the Kubernetes cluster with placeholder commands. Follow the instructions below:


Create a cronjob named datacenter.


Set Its schedule to something like */5 * * * *. You can set any schedule for now.


Name the container cron-datacenter.


Utilize the httpd image with latest tag (specify as httpd:latest).


Execute the dummy command echo Welcome to xfusioncorp!.


Ensure the restart policy is OnFailure.

Note: The kubectl utility on jump_host is configured to work with the kubernetes cluster.

don't forget to set container name to cron-datacenter and restart policy to OnFailure.

```bash
kubectl create cronjob datacenter --schedule="*/5 * * * *" --image=httpd:latest --restart=OnFailure -- /bin/sh -c "echo Welcome to xfusioncorp!"
```
 edit cronjob to set the container name to cron-datacenter:

 ```bash
kubectl patch cronjob datacenter -p '{"spec":{"jobTemplate":{"spec":{"template":{"spec":{"containers":[{"name":"cron-datacenter"}]}}}}}}'
```
The CronJob "datacenter" is invalid: spec.jobTemplate.spec.template.spec.containers[0].image: Required value

To resolve the error, you need to specify the image in the container definition. Here’s how to update the cron job with the correct container name and image:

```bash
kubectl patch cronjob datacenter -p '{"spec":{"jobTemplate":{"spec":{"template":{"spec":{"containers":[{"name":"cron-datacenter","image":"httpd:latest"}]}}}}}}'
```

```bash
kubectl get cronjob datacenter -o yaml
```

