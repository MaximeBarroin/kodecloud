The Nautilus DevOps team needs to set up several docker environments for different applications. One of the team members has been assigned a ticket where he has been asked to create some docker networks to be used later. Complete the task based on the following ticket description:


a. Create a docker network named as ecommerce on App Server 3 in Stratos DC.


b. Configure it to use bridge drivers.


c. Set it to use subnet 172.28.0.0/24 and iprange 172.28.0.0/24.

stapp03	172.16.238.12	stapp03.stratos.xfusioncorp.com	banner	BigGr33n	Nautilus App 3

```bash
ssh banner@stapp03.stratos.xfusioncorp.com

# Create the docker network
docker network create --driver bridge --subnet 172.28.0.0/24 --ip-range 172.28.0.0/24 ecommerce
#cidr show this network can be join by a number of machines of 254
# 172.28.0.1 - 172.28.0.254

# check
docker network ls