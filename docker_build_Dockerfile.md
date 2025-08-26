As per recent requirements shared by the Nautilus application development team, they need custom images created for one of their projects. Several of the initial testing requirements are already been shared with DevOps team. Therefore, create a docker file /opt/docker/Dockerfile (please keep D capital of Dockerfile) on App server 1 in Stratos DC and configure to build an image with the following requirements:

stapp01	172.16.238.10	stapp01.stratos.xfusioncorp.com	tony	Ir0nM@n	Nautilus App 1


a. Use ubuntu:24.04 as the base image.


b. Install apache2 and configure it to work on 6000 port. (do not update any other Apache configuration settings like document root etc).

```bash
ssh tony@stapp01.stratos.xfusioncorp.com
# Create the directory with sudo
sudo mkdir -p /opt/docker

# Create the Dockerfile using tee with sudo
sudo tee /opt/docker/Dockerfile > /dev/null << 'EOF'
FROM ubuntu:24.04

RUN apt update && \
    apt install apache2 -y && \
    sed -i 's/Listen 80/Listen 6000/' /etc/apache2/ports.conf && \
    sed -i 's/:80>/:6000>/' /etc/apache2/sites-available/000-default.conf

EXPOSE 6000

CMD ["apache2ctl", "-D", "FOREGROUND"]
EOF
```
check if the Dockerfile was created successfully.

```bash
sudo docker build -t media:webserver /opt/docker
```

Key Technical Decisions
Permission Handling: Used sudo tee to overcome /opt directory write permissions
Apache Foreground Mode: Used apache2ctl -D FOREGROUND instead of service commands for container compatibility
Port Configuration: Modified both configuration files to ensure complete port change
Image Tagging: Named the image media:webserver for clear identification
