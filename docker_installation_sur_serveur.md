Install docker-ce and docker compose packages on App Server 2.




```bash
sudo apt-get update
sudo apt-get install -y docker-ce docker-compose
```

apt-get command is not found
If the `apt-get` command is not found, it indicates that the system is not using a Debian-based distribution (like Ubuntu). In such cases, you may need to use the package manager specific to your distribution. For example, if you are using a Red Hat-based distribution, you would use `yum` or `dnf`.

```bash
sudo yum update
sudo yum install -y docker-ce docker-compose
```

Unable to find a match: docker-ce docker-compose
If you encounter the error `Unable to find a match: docker-ce docker-compose`, it means that the Docker packages are not available in your current repository. You may need to set up the Docker repository first. Here’s how you can do it:
1. **Set up the Docker repository**:
   For Ubuntu or Debian-based systems, you can follow these steps:

   ```bash
   sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   ```

   For Red Hat-based systems, you can use:

   ```bash
   sudo yum install -y yum-utils
   sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
   ```
2. **Update the package index**:
    After adding the Docker repository, update the package index again:
    
    ```bash
    sudo apt-get update
    ```
    
    or for Red Hat-based systems:
    
    ```bash
    sudo yum makecache fast
    ```
3. **Install Docker**:
   Now you can try installing Docker again:
    For Ubuntu or Debian-based systems:
    
    ```bash
    sudo apt-get install -y docker-ce docker-compose
    ```
    For Red Hat-based systems:
    
    ```bash
    sudo yum install -y docker-ce docker-compose
    ```

 
Initiate the docker service.

```bash
sudo systemctl start docker
sudo systemctl enable docker


Failed to start docker.service: Unit docker.service not found.

```
If you encounter the error `Failed to start docker.service: Unit docker.service not found`, it indicates that Docker is not installed correctly or the service file is missing. You can try reinstalling Docker or checking if the installation was successful.
If you are using a different package manager, such as `yum` or `dnf`, the commands to start and enable Docker might differ slightly. For example, on a Red Hat-based system, you would use:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```
If you are still facing issues, you can check the status of the Docker service to get more information about the error:

```bash
sudo systemctl status docker
```

Unit docker.service could not be found.

If you see the error `Unit docker.service could not be found`, it means that the Docker service is not installed or not recognized by the system. Here are some steps to troubleshoot and resolve this issue:

1. **Check Docker Installation**: Ensure that Docker is installed correctly. You can verify this by running:

   ```bash
   docker --version
   ```

   If Docker is not installed, you will need to install it.

   bash: docker: command not found

2. **Install Docker**: If Docker is not installed, you can install it using the appropriate package manager for your distribution. For example, on Ubuntu or Debian-based systems, you can use:


