As part of the temporary assignment to the Nautilus project, a developer named javed requires access for a limited duration. To ensure smooth access management, a temporary user account with an expiry date is needed. Here's what you need to do:



Create a user named javed on App Server 3 in Stratos Datacenter. Set the expiry date to 2023-12-07, ensuring the user is created in lowercase as per standard protocol.


stapp03	172.16.238.12	stapp03.stratos.xfusioncorp.com	banner	BigGr33n	Nautilus App 3
```bash
ssh banner@stapp03.stratos.xfusioncorp.com
sudo useradd -e 2023-12-07 javed # -e option is used to set the expiry date
# check expiry
sudo chage -l javed # verify the expiry date