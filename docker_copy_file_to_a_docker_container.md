The Nautilus DevOps team possesses confidential data on App Server 2 in the Stratos Datacenter. A container named ubuntu_latest is running on the same server.



Copy an encrypted file /tmp/nautilus.txt.gpg from the docker host to the ubuntu_latest container located at /usr/src/. Ensure the file is not modified during this operation.


stapp02	172.16.238.11	stapp02.stratos.xfusioncorp.com	steve	Am3ric@	Nautilus App 2

```bash
ssh steve@stapp02.stratos.xfusioncorp.com
```
password: Am3ric@

```bash
sudo su -
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/usr/src/nautilus.txt.gpg
```
Successfully copied 2.05kB to ubuntu_latest:/usr/src/nautilus.txt.gpg

To verify that the file has been copied successfully, you can execute the following command inside the container:

```bash
docker exec -it ubuntu_latest ls -l /usr/src/nautilus.txt.gpg
```

This command will list the details of the file, confirming its presence and size.
To ensure that the file has been copied correctly and is intact, you can also check the file size or perform a checksum comparison if needed. Here’s how to check the file size:

```bash
docker exec -it ubuntu_latest du -h /usr/src/nautilus.txt.gpg
```


i wand to ensure the file has not been modified during the copy operation. You can compare the file size or checksum of the original file on the host with that in the container. Here’s how to do it:
```bash
# Check the file size on the host
du -h /tmp/nautilus.txt.gpg
# Check the file size in the container
docker exec -it ubuntu_latest du -h /usr/src/nautilus.txt.gpg
```
If both commands return the same file size, it indicates that the file has not been modified during the copy operation. If you want to perform a checksum comparison, you can use the `md5sum` or `sha256sum` command as follows:

```bash
md5sum /tmp/nautilus.txt.gpg
docker exec -it ubuntu_latest md5sum /usr/src/nautilus.txt.gpg
```
the output of both commands should match if the file has not been modified.