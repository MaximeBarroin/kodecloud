After conducting a security audit within the Stratos DC, the Nautilus security team discovered misconfigured permissions on critical files. To address this, corrective actions are being taken by the production support team. Specifically, the file named /etc/resolv.conf on Nautilus App 3 server requires adjustments to its Access Control Lists (ACLs) as follows:

stapp03	172.16.238.12	stapp03.stratos.xfusioncorp.com	banner	BigGr33n	Nautilus App 3

1. The file's user owner and group owner should be set to root.

2. Others should possess read only permissions on the file.

3. User james must not have any permissions on the file.

4. User eric should be granted read only permission on the file.

```bash
ssh banner@stapp03.stratos.xfusioncorp.com
# Check current permissions and ownership
ls -l /etc/resolv.conf

-rw-r--r-- 1 root root 69 Aug 27 13:59 /etc/resolv.conf

# Set user and group ownership to root
chown root:root /etc/resolv.conf

# Set permissions
chmod 444 /etc/resolv.conf # read only for all

# Verify changes
ls -l /etc/resolv.conf

# Verify ACLs
getfacl /etc/resolv.conf

user::r--
group::r--
other::r--

# Set specific ACLs for users
setfacl -m u:james:--- /etc/resolv.conf
setfacl -m u:eric:r-- /etc/resolv.conf

# Verify ACLs
getfacl /etc/resolv.conf

```