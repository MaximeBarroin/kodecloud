Within the Stratos DC, the Nautilus storage server hosts a directory named /data, serving as a repository for various developers non-confidential data. Developer mark has requested a copy of their data stored in /data/mark. The System Admin team has provided the following steps to fulfill this request:



a. Create a compressed archive named mark.tar.gz of the /data/mark directory.

b. Transfer the archive to the /home directory on the Storage Server.

ststor01	172.16.238.15	ststor01.stratos.xfusioncorp.com	natasha	Bl@kW	Nautilus Storage Server

```bash
ssh natasha@ststor01.stratos.xfusioncorp.com
tar -czvf /home/mark.tar.gz /data/mark  # -czvf action is to create a compressed archive

# verify the archive contents
tar -tzvf /home/mark.tar.gz
```





