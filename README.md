# advanced-FTP-serverAdvanced FTP Server Setup
Project Overview
This project aims to set up and configure a secure FTP server using vsftpd and an FTP client like FileZilla. The objective is to ensure controlled access to different user groups, secure file transfers, and effective user management.
Objectives
●	Install and configure an FTP server with vsftpd.
●	Implement security measures like disabling anonymous access and enabling chroot jail.
●	Configure different user groups with specific access rights.
●	Install and configure FileZilla for testing file transfers.
Step-by-Step Setup
Step 1: Install and onfigure the FTP Server (vsftpd)
Install vsftpd on Ubuntu/Debian:
sudo apt update
sudo apt install vsftpd -y

Configure vsftpd:
Edit the configuration file:
sudo nano /etc/vsftpd.conf

Modify or add the following settings:
anonymous_enable=NO
local_enable=YES
write_enable=YES
chroot_local_user=YES
allow_writeable_chroot=YES
ssl_enable=YES
rsa_cert_file=/etc/ssl/certs/vsftpd.pem
rsa_private_key_file=/etc/ssl/private/vsftpd.pem
pasv_enable=YES
pasv_min_port=40000
pasv_max_port=50000

Restart the vsftpd service:
sudo systemctl restart vsftpd

Step 2: Create and Manage Users
Create the required users and directories:
sudo useradd -m -d /var/ftp/dev -s /usr/sbin/nologin devTeam
sudo useradd -m -d /var/ftp/qa -s /usr/sbin/nologin qaTeam
sudo useradd -m -d /var/ftp/client -s /usr/sbin/nologin clientUser

Set passwords:
sudo passwd devTeam
sudo passwd qaTeam
sudo passwd clientUser

Set directory permissions:
sudo chown -R devTeam:devTeam /var/ftp/dev
sudo chown -R qaTeam:qaTeam /var/ftp/qa
sudo chown -R clientUser:clientUser /var/ftp/client
sudo chmod 750 /var/ftp/dev
sudo chmod 750 /var/ftp/qa
sudo chmod 750 /var/ftp/client

Step 3: Install and Configure FileZilla
Install FileZilla:
sudo apt install filezilla -y

Configure FileZilla:
●	Open FileZilla
●	Go to File > Site Manager
●	Create a new site with:
○	Host: (your server IP)
○	Protocol: FTP
○	Encryption: Require explicit FTP over TLS
○	Login type: Normal
○	Username: (e.g., devTeam, qaTeam, clientUser)
○	Password: (set during user creation)
Step 4: Test File Transfers
●	Use devTeam to upload and download files in /var/ftp/dev
●	Use qaTeam to download files from /var/ftp/qa
●	Use clientUser to download files from /var/ftp/client
Screenshots
(Include relevant screenshots of configuration files, FileZilla setup, and file transfers.)
Resources
●	Setting up vsftpd
●	GitHub Documentation


  ![WhatsApp Image 2025-02-05 at 19 29 50 (1)](https://github.com/user-attachments/assets/83d20fca-fe59-43df-ac23-8464584c9e9e)
  ![WhatsApp Image 2025-02-05 at 19 29 50 (7)](https://github.com/user-attachments/assets/faba57c9-d3e0-47f8-96fb-9b11b2eefc4f)
![WhatsApp Image 2025-02-05 at 19 29 50 (8)](https://github.com/user-attachments/assets/405eb1aa-2870-401c-9ce2-b65a8be247d3)
![WhatsApp Image 2025-02-05 at 19 29 50 (9)](https://github.com/user-attachments/assets/637e171e-87d4-4ce8-9bd3-4c77edbead03)

