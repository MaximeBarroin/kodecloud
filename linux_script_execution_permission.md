In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named xfusioncorp.sh. While the script has been distributed to all necessary servers, it lacks executable permissions on App Server 3 within the Stratos Datacenter.



Your task is to grant executable permissions to the /tmp/xfusioncorp.sh script on App Server 3. Additionally, ensure that all users have the capability to execute it.

stapp03	172.16.238.12	stapp03.stratos.xfusioncorp.com	banner	BigGr33n	Nautilus App 3

```bash
ssh banner@stapp03.stratos.xfusioncorp.com
chmod +x /tmp/xfusioncorp.sh
# verify
ls -l /tmp/xfusioncorp.sh
```
---x--x--x 1 root root 40 Aug 27 07:28 /tmp/xfusioncorp.sh

try to execute it

```bash
/tmp/xfusioncorp.sh
```

/bin/bash: /tmp/xfusioncorp.sh: Permission denied

```bash
# all user must have execute permission
chmod a+x /tmp/xfusioncorp.sh
# verify
ls -l /tmp/xfusioncorp.sh
```
---x--x--x 1 root root 40 Aug 27 07:28 /tmp/xfusioncorp.sh

```bash
# Grant read and execute permissions to all users
chmod a+rx /tmp/xfusioncorp.sh

# Alternative: Use numeric notation
chmod 755 /tmp/xfusioncorp.sh

# Verify the permissions
ls -l /tmp/xfusioncorp.sh
```
-rwxr-xr-x 1 root root 40 Aug 27 07:28 /tmp/xfusioncorp.sh

```bash
# Now test execution
/tmp/xfusioncorp.sh
```

## Permission Analysis
- **Before**: `---x--x--x` (execute only, no read)
- **After**: `-rwxr-xr-x` (read + execute for all users)
- **Owner**: rwx (read, write, execute)
- **Group**: r-x (read, execute)
- **Others**: r-x (read, execute)

## Key Learning
For script execution, users need:
1. **Read permission** - to read the script content
2. **Execute permission** - to run the script
3. Both permissions are required; execute alone is insufficient
