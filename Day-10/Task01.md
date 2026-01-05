### Day 10: Linux Bash Scripts

The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on App Server 3 in Stratos Datacenter, and they need to create a bash script named official_backup.sh which should accomplish the following tasks. (Also remember to place the script under /scripts directory on App Server 3).



a. Create a zip archive named xfusioncorp_official.zip of /var/www/html/official directory.


b. Save the archive in /backup/ on App Server 3. This is a temporary storage, as backups from this location will be clean on weekly basis. Therefore, we also need to save this backup archive on Nautilus Backup Server.


c. Copy the created archive to Nautilus Backup Server server in /backup/ location.


d. Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.


e. Do not use sudo inside the script.

Note:
The zip package must be installed on given App Server before executing the script. This package is essential for creating the zip archive of the website files. Install it manually outside the script.

![alt text](image.png)


✅ TASK: Website Backup Script (App Server 2)

Server: App Server 2
Script name: official_backup.sh
Script location: /scripts/official_backup.sh

1️⃣ Login to App Server 2
ssh steve@stapp02


(Use the correct default user for App Server 2 if different.)

2️⃣ Install zip package (OUTSIDE the script)
sudo yum install -y zip


⚠️ This must NOT be inside the script (task requirement).

3️⃣ Verify website directory exists
ls /var/www/html


You must see:

official


If not, do not continue until it exists.

4️⃣ Create required directories
sudo mkdir -p /scripts /backup
sudo chown -R steve:steve /scripts /backup


Replace steve with the actual App Server 2 user if needed.

5️⃣ Setup passwordless SSH to Backup Server

This ensures no password prompt during copy.

Generate SSH key
ssh-keygen -t rsa -b 2048


Press ENTER for all prompts (no passphrase).

Copy key to Nautilus Backup Server
ssh-copy-id clint@stbkp01.stratos.xfusioncorp.com

Test
ssh clint@stbkp01.stratos.xfusioncorp.com
exit


✅ If login works without password → correct

6️⃣ Create the script (IMPORTANT)
vi /scripts/official_backup.sh

📌 Paste exactly this content
#!/bin/bash

SOURCE_DIR="/var/www/html/official"
BACKUP_DIR="/backup"
ZIP_NAME="xfusioncorp_official.zip"

REMOTE_USER="clint"
REMOTE_HOST="stbkp01.stratos.xfusioncorp.com"
REMOTE_DIR="/backup"

zip -r "${BACKUP_DIR}/${ZIP_NAME}" "${SOURCE_DIR}"
scp "${BACKUP_DIR}/${ZIP_NAME}" "${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_DIR}/"


Save and exit:

ESC :wq

7️⃣ Make script executable
chmod +x /scripts/official_backup.sh

8️⃣ Run the script
/scripts/official_backup.sh

9️⃣ Verify backup on App Server 2
ls -l /backup/xfusioncorp_official.zip

🔟 Verify backup on Nautilus Backup Server
ssh clint@stbkp01.stratos.xfusioncorp.com
ls -l /backup/xfusioncorp_official.zip
exit