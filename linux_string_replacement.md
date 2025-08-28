Within the Stratos DC, the backup server holds template XML files crucial for the Nautilus application. Before utilization, these files require valid data insertion. As part of routine maintenance, system admins at xFusionCorp Industries employ string and file manipulation commands.



Your task is to substitute all occurrences of the string About with Cloud within the XML file located at /root/nautilus.xml on the backup server.

stbkp01	172.16.238.16	stbkp01.stratos.xfusioncorp.com	clint	H@wk3y3	Nautilus Backup Server

```bash
ssh clint@stbkp01.stratos.xfusioncorp.com
# Navigate to the directory containing the XML file
cd /root

# Use sed to replace all occurrences of "About" with "Cloud"
sed -i 's/About/Cloud/g' nautilus.xml #sed command to replace text -i for in-place editing

# Verify changes
vi nautilus.xml
