In response to heightened security concerns, the xFusionCorp Industries security team has opted for custom Apache users for their web applications. Each user is tailored specifically for an application, enhancing security measures. Your task is to create a custom Apache user according to the outlined specifications:

stapp03	172.16.238.12	stapp03.stratos.xfusioncorp.com	banner	BigGr33n	Nautilus App 3


a. Create a user named kirsty on App server 3 within the Stratos Datacenter.

b. Assign a unique UID 1581 and designate the home directory as /var/www/kirsty.


```bash
ssh banner@stapp03.stratos.xfusioncorp.com
sudo su -
```

```bash
useradd -u 1581 -d /var/www/kirsty -s /bin/false kirsty
```


