One of the Nautilus project developers need access to run docker commands on App Server 1. This user is already created on the server. Accomplish this task as per details given below:

User john is not able to run docker commands on App Server 1 in Stratos DC, make the required changes so that this user can run docker commands without sudo.


stapp01	172.16.238.10	stapp01.stratos.xfusioncorp.com	tony	Ir0nM@n	Nautilus App 1

```bash
ssh tony@stapp01.stratos.xfusioncorp.com
sudo usermod -aG docker john

// Verify that john can run docker commands without sudo
sudo -u john docker ps
```
we don't know password for john so we have to try with sudo privileges.