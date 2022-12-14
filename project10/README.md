# DevOps PBL
# Project 10 Report

# Darey.io - DevOps Project Base Learning Project 10 Documentation

October 2022

## LOAD BALANCER SOLUTION WITH NGINX AND SSL/TLS

### Task
This project consists of two parts:

1. Configure Nginx as a Load Balancer
2. Register a new domain name and configure secured connection using SSL/TLS certificates

Your target architecture will look like this:

![project10 prerequisites](images/nginx_lb.png)

### Step 1 - CONFIGURE NGINX AS A LOAD BALANCER

We can either uninstall Apache from the existing Load Balancer server, or create a fresh installation of Linux for Nginx.

1. Create an EC2 VM based on Ubuntu Server 20.04 LTS and name it **Nginx LB** (do not forget to open TCP port 80 for HTTP connections, also open TCP port 443 – this port is used for secured HTTPS connections)
2. Update **/etc/hosts** file for local DNS with Web Servers’ names (e.g. **Web1** and **Web2**) and their local IP addresses
3. Install and configure Nginx as a load balancer to point traffic to the resolvable DNS names of the webservers

Update the instance and Install Nginx. Run the following commands to achieve this:

`sudo apt update`
`sudo apt install nginx`

Configure Nginx LB using Web Servers’ names defined in /etc/hosts

Open the default nginx configuration file with the command:

`sudo vi /etc/nginx/nginx.conf`

```
#insert following configuration into http section
upstream myproject {
server Web1 weight=5;
server Web2 weight=5;
}
server {
listen 80;
server_name www.domain.com;
location / {
proxy_pass http://myproject;
}
}
#comment out this line
# include /etc/nginx/sites-enabled/*;
```

Restart Nginx and make sure the service is up and running with the next commands:

`sudo systemctl restart nginx`

`sudo systemctl status nginx`

### Step 2 - Register a new domain name and configure secured connection using SSL/TLS certificates

