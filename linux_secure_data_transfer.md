A Nautilus developer has stored confidential data on the jump host within Stratos DC. To ensure security and compliance, this data must be transferred to one of the app servers. Given developers lack direct access to these servers, the system admin team has been enlisted for assistance.

stapp01	172.16.238.10	stapp01.stratos.xfusioncorp.com	tony	Ir0nM@n	Nautilus App 1
stapp02	172.16.238.11	stapp02.stratos.xfusioncorp.com	steve	Am3ric@	Nautilus App 2
stapp03	172.16.238.12	stapp03.stratos.xfusioncorp.com	banner	BigGr33n	Nautilus App 3
stlb01	172.16.238.14	stlb01.stratos.xfusioncorp.com	loki	Mischi3f	Nautilus HTTP LBR
stdb01	172.16.239.10	stdb01.stratos.xfusioncorp.com	peter	Sp!dy	Nautilus DB Server
ststor01	172.16.238.15	ststor01.stratos.xfusioncorp.com	natasha	Bl@kW	Nautilus Storage Server
stbkp01	172.16.238.16	stbkp01.stratos.xfusioncorp.com	clint	H@wk3y3	Nautilus Backup Server
stmail01	172.16.238.17	stmail01.stratos.xfusioncorp.com	groot	Gr00T123	Nautilus Mail Server
jump_host	Dynamic	jump_host.stratos.xfusioncorp.com	thor	mjolnir123	Jump Server to Access Stork DC
jenkins	172.16.238.19	jenkins.stratos.xfusioncorp.com	jenkins	j@rv!s	Jenkins Server for CI/CD

Copy /tmp/nautilus.txt.gpg file from jump server to App Server 2 placing it in the directory /home/webdata.

```bash
scp /tmp/nautilus.txt.gpg steve@stapp02.stratos.xfusioncorp.com:/home/webdata # scp permits to securely copy files between hosts
```