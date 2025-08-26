In response to the latest tool implementation at xFusionCorp Industries, the system admins require the creation of a service user account. Here are the specifics:



Create a user named james in App Server 1 without a home directory.

Note: You can find the infrastructure details by clicking on the Details of all Users and Servers button on the top-right section of the page.

stapp01	172.16.238.10	stapp01.stratos.xfusioncorp.com	tony	Ir0nM@n	Nautilus App 1

```bash
ssh tony@stapp01.stratos.xfusioncorp.com
sudo useradd -M james  # -M option is used to create a user without a home directory
# no home directory is useful when the user is only going to run a specific service
## verify
sudo id james
