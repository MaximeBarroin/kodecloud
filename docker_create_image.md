One of the Nautilus developer was working to test new changes on a container. He wants to keep a backup of his changes to the container. A new request has been raised for the DevOps team to create a new image from this container. Below are more details about it:

stapp01	172.16.238.10	stapp01.stratos.xfusioncorp.com	tony	Ir0nM@n	Nautilus App 1


a. Create an image media:devops on Application Server 1 from a container ubuntu_latest that is running on same server.

```bash
ssh tony@stapp01.stratos.xfusioncorp.com
sudo docker commit ubuntu_latest media:devops
docker images
```