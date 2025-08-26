One of the Nautilus DevOps team members was working to configure services on a kkloud container that is running on App Server 2 in Stratos Datacenter. Due to some personal work he is on PTO for the rest of the week, but we need to finish his pending work ASAP. Please complete the remaining work as per details given below:


a. Install apache2 in kkloud container using apt that is running on App Server 2 in Stratos Datacenter.


b. Configure Apache to listen on port 5004 instead of default http port. Do not bind it to listen on specific IP or hostname only, i.e it should listen on localhost, 127.0.0.1, container ip, etc.


c. Make sure Apache service is up and running inside the container. Keep the container in running state at the end.


stapp02	172.16.238.11	stapp02.stratos.xfusioncorp.com	steve	Am3ric@	Nautilus App 2


```bash
ssh steve@stapp02.stratos.xfusioncorp.com
## Connect to the kkloud container
sudo docker exec -it kkloud bash
apt update
## Install Apache
apt install apache2 -y
## Configure Apache to listen on port 5004
sed -i 's/Listen 80/Listen 5004/' /etc/apache2/ports.conf
## Restart Apache service
service apache2 restart

# Restarting Apache httpd web server apache2                                                                                                                                         AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.12.0.2. Set the 'ServerName' directive globally to suppress this message

 # c. Make sure Apache service is up and running inside the container. Keep the container in running state at the end.

service apache2 status