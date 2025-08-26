Following security audits, the xFusionCorp Industries security team has rolled out new protocols, including the restriction of direct root SSH login.



Your task is to disable direct SSH root login on all app servers within the Stratos Datacenter.

stapp01	172.16.238.10	stapp01.stratos.xfusioncorp.com	tony	Ir0nM@n	Nautilus App 1
stapp02	172.16.238.11	stapp02.stratos.xfusioncorp.com	steve	Am3ric@	Nautilus App 2
stapp03	172.16.238.12	stapp03.stratos.xfusioncorp.com	banner	BigGr33n	Nautilus App 3


```bash
ssh banner@stapp03.stratos.xfusioncorp.com
sudo nano /etc/ssh/sshd_config
#nano is not installed
sudo vi /etc/ssh/sshd_config
# Find the line that says "PermitRootLogin yes" and change it to "PermitRootLogin no"
# Save and exit the editor
sudo systemctl restart sshd
```

repeat on each app server

```bash
ssh tony@stapp01.stratos.xfusioncorp.com
sudo vi /etc/ssh/sshd_config
# Find the line that says "PermitRootLogin yes" and change it to "PermitRootLogin no"
# Save and exit the editor
sudo systemctl restart sshd

ssh steve@stapp02.stratos.xfusioncorp.com
sudo vi /etc/ssh/sshd_config
# Find the line that says "PermitRootLogin yes" and change it to "PermitRootLogin no"
# Save and exit the editor
sudo systemctl restart sshd

