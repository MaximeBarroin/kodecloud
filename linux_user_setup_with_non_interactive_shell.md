To accommodate the backup agent tool's specifications, the system admin team at xFusionCorp Industries requires the creation of a user with a non-interactive shell. Here's your task:



Create a user named mariyam with a non-interactive shell on App Server 1.

Note: You can find the infrastructure details by clicking on the Details of all Users and Servers button on the top-right section of the page.


stapp01	172.16.238.10	stapp01.stratos.xfusioncorp.com	tony	Ir0nM@n	Nautilus App 1

```bash
ssh tony@stapp01.stratos.xfusioncorp.com
sudo useradd -s /sbin/nologin mariyam