The Nautilus DevOps team is conducting application deployment tests on selected application servers. They require a nginx container deployment on Application Server 3. Complete the task with the following instructions:


On Application Server 3 create a container named nginx_3 using the nginx image with the alpine tag. Ensure container is in a running state.

stapp03	172.16.238.12	stapp03.stratos.xfusioncorp.com	banner	BigGr33n	Nautilus App 3.

```bash
ssh banner@172.16.238.12
```
 set the password to BigGr33n
```bash
sudo su -
```
Then install Docker if not already installed:
```bash
yum install docker -y
```
Start the Docker service:
```bash
systemctl start docker
```

```bash
docker run --name nginx_3 -d nginx:alpine
```

Verify that the container is running:
```bash
docker ps
```
```bash
docker inspect nginx_3
```

```bash
docker logs nginx_3
```