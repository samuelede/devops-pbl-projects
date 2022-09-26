

# DevOps PBL
# Project 7 Report

# Darey.io - DevOps Project Base Learning Project 7 Documentation

AUGUST 2022

## DEVOPS TOOLING WEBSITE SOLUTION




### Setup and technologies used in Project 7
As a member of a DevOps team, you will implement a tooling website solution which makes access to DevOps tools within the corporate infrastructure easily accessible.

In this project you will implement a solution that consists of following components:

1. Infrastructure: AWS
2. Webserver Linux: Red Hat Enterprise Linux 8
3. Database Server: Ubuntu 20.04 + MySQL
4. Storage Server: Red Hat Enterprise Linux 8 + NFS Server
5. Programming Language: PHP
6. Code Repository: GitHub

On the diagram below you can see a common pattern where several stateless Web Servers share a common database and also access the same files using Network File Sytem (NFS) as a shared file storage. Even though the NFS server might be located on a completely separate hardware – for Web Servers it look like a local file system from where they can serve the same files.

![3Tier Tooling Website Infrastructure](images/0-Tooling-Website-Infrastructure.png)

### Step 1 – Prepare NFS Server
Spin up a new EC2 instance with RHEL Linux 8 Operating System.

Based on your LVM experience from [Project 6](https://github.com/samuelede/devops-pbl-projects/tree/main/project6#step-1---prepare-a-web-server), follow the steps and setup a server named NFS Server to Configure LVM on the Server.


Instead of formating the disks as **ext4** you will have to format them as **xfs**

Ensure there are 3 Logical Volumes. *lv-opt* *lv-apps*, and *lv-logs*

Create mount points on /mnt directory for the logical volumes as follow:

**Mount lv-apps** on **/mnt/apps** – To be used by webservers

**Mount lv-logs** on **/mnt/logs** – To be used by webserver logs

**Mount lv-opt** on **/mnt/opt** – To be used by Jenkins server in Project 8


Install *NFS server*, configure it to start on reboot and make sure it is up and running. Run the following commands
`sudo yum -y update`

`sudo yum install nfs-utils -y`

`sudo systemctl start nfs-server.service`

`sudo systemctl enable nfs-server.service`

`sudo systemctl status nfs-server.service`

![3Tier Configure NFS Server](images/step7_1_configureNFS_server.png)


### STEP 2 — CONFIGURE THE DATABASE SERVER
Following the previous steps in [Project 6 - Step 4 and Step 5](https://github.com/samuelede/devops-pbl-projects/tree/main/project6#step-4---install-mysql-on-db-server-ec2) configure a MySQL DBMS Server named *DB Server* to work with the remote Web Server

1. Install MySQL server
2. Create a database and name it **tooling**
3. Create a database user and name it **webaccess**
4. Grant permission to *webaccess* user on *tooling* database to do anything only from the webservers *subnet cidr*


### STEP 3 — PREPARE THE WEB SERVERS

We need to make sure that our Web Servers can serve the same content from shared storage solutions, in our case – NFS Server and MySQL database.
You already know that one DB can be accessed for reads and writes by multiple clients. For storing shared files that our Web Servers will use – we will utilize NFS and mount previously created Logical Volume lv-apps to the folder where Apache stores files to be served to the users (/var/www).

This approach will make our Web Servers stateless, which means we will be able to add new ones or remove them whenever we need, and the integrity of the data (in the database and on NFS) will be preserved.

During the next steps we will do following:

- Configure NFS client (this step must be done on all three servers)
- Deploy a Tooling application to our Web Servers into a shared NFS folder
- Configure the Web Servers to work with a single MySQL database

1. Launch a new EC2 instance with RHEL 8 Operating System

2. Install NFS client

`sudo yum install nfs-utils nfs4-acl-tools -y`

3. Mount /var/www/ and target the NFS server’s export for apps

`sudo mkdir /var/www`

`sudo mount -t nfs -o rw,nosuid <NFS-Server-Private-IP-Address>:/mnt/apps /var/www`

4. Verify that NFS was mounted successfully by running df -h. Make sure that the changes will persist on Web Server after reboot:

`sudo vi /etc/fstab`

add following line

`<NFS-Server-Private-IP-Address>:/mnt/apps /var/www nfs defaults 0 0`

5. Install Remi’s repository, Apache and PHP

`sudo yum install httpd -y`

`sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm`

`sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm`

`sudo dnf module reset php`

`sudo dnf module enable php:remi-7.4`

`sudo dnf install php php-opcache php-gd php-curl php-mysqlnd`

`sudo systemctl start php-fpm`

`sudo systemctl enable php-fpm`

`setsebool -P httpd_execmem 1`

Repeat steps 1-5 for another 2 Web Servers.
