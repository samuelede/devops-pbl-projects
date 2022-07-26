

Project 2 Report

Darey.io - DevOps Project Base Learning Project2 Documentation

JULY 2022

LEMP STACK IMPLEMENTATION








STEP 0 - Preparing prerequisites

In order to complete this project you will need an AWS account and a virtual server with Ubuntu Server OS.
If you do not have an AWS account – go back to Project 1 Step 0 to sign in to AWS free tier account and create a new EC2 Instance of t2.nano family with Ubuntu Server 22.04 LTS (HVM) image and logi to the via the terminal.


Step 1 - Installing the NGINX Web Server 

To enable web pages  to be visible to visitors, we require an Nginx web server to display the web pages. The apt  package manager is used to install this feature. 
We begin by installing Nginx using the following commands:


Step 2 of 1 - Type the following at the terminal as shown above.
sudo apt update hit enter then type sudo apt install nginx
At the prompt, type y to confirm and continue Nginx installation.


Step 2 of 2 - After the installation is complete, run the following command to check the status of the installation. sudo systemctl status nginx


Step 2 of 3 - The green active (runing) state confirms a successful Nginx server installation also suggesting the launch of the web server in the cloud. Type q if you want to exit the server.


Step 2 of 4 - Next, we can access our webpage via port 80, type the following commands to achieve this:  curl http://localhost:80 or curl http://127.0.0.1:80
The first url uses the DNS name to access the web server while the second url uses the server IP address. 

To test our web server on a browser, we type the follwoing command.

Step 2 of 5 - In the browser type http://<Public-IP-Address>:80

Another method of accessing the server ip address is by typing the following command:

curl -s http://169.254.169.254/latest/meta-data/public-ipv4
The above image shows the current ip address of our working AWS server.



Step 2 - Installing MySQL

In step 2, the next step is to install our database (DBMS) server, now that our Nginx server installation is complete.  

Again we use the ‘apt’ command to gather the requirements and install the software.


Step 2 of 1 - Run the command sudo apt install mysql-server and hit enter. Type y to accept and continue the process as showen in the image above.


Step 2 of 2 - At the command line type sudo mysql to launch the mysql console as shown above.


Step 2 of 3 - Run the following command and hit enter to update the root default password. 
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
Next, type exit to exit from the mysql shell.


Step 2 of 4 - Next, run the command sudo mysql_secure_installation and follow the steps, firstly typing the default root password ‘PassWord.1’ and following the instructions and prompts.






Step 3 - Installing PHP

To install PHP to process our codes and generate dynamic content via the web server, we need to install a few packages from the command line so our Nginx server can process PHP requestst. 

Step 3 of 1 - Run the following command sudo apt install php-fpm php-mysql to begin the PHP installation process, type y and hit Enter to to continue as shown above.

All done.

