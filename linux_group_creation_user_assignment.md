The system admin team at xFusionCorp Industries has streamlined access management by implementing group-based access control. Here's what you need to do:



a. Create a group named nautilus_sftp_users across all App servers within the Stratos Datacenter.


b. Add the user kano into the nautilus_sftp_users group on all App servers. If the user doesn't exist, create it as well.


stapp01	172.16.238.10	stapp01.stratos.xfusioncorp.com	tony	Ir0nM@n	Nautilus App 1
stapp02	172.16.238.11	stapp02.stratos.xfusioncorp.com	steve	Am3ric@	Nautilus App 2
stapp03	172.16.238.12	stapp03.stratos.xfusioncorp.com	banner	BigGr33n	Nautilus App 3

```bash
ssh tony@stapp01.stratos.xfusioncorp.com
sudo su -
groupadd nautilus_sftp_users
usermod -aG nautilus_sftp_users kano
useradd -u 1582 -d /var/www/kano -s /bin/false kano
//useradd kano to nautilus_sftp_users
usermod -aG nautilus_sftp_users kano
exit 
exit
```

```bash
ssh steve@stapp02.stratos.xfusioncorp.com
sudo su -
groupadd nautilus_sftp_users
usermod -aG nautilus_sftp_users kano
useradd -u 1582 -d /var/www/kano -s /bin/false kano
//useradd kano to nautilus_sftp_users
usermod -aG nautilus_sftp_users kano
exit
exit
```
```bash
ssh banner@stapp03.stratos.xfusioncorp.com
sudo su -
groupadd nautilus_sftp_users
usermod -aG nautilus_sftp_users kano
useradd -u 1582 -d /var/www/kano -s /bin/false kano
//useradd kano to nautilus_sftp_users
usermod -aG nautilus_sftp_users kano
exit
exit
```