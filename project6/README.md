


# DevOps PBL
# Project 6 Report

# Darey.io - DevOps Project Base Learning Project6 Documentation

AUGUST 2022

## WEB SOLUTION WITH WORDPRESS








## Web Solution with WORDPRESS

You are progressing in practicing to implement web solutions using different technologies. As a DevOps engineer you will most probably encounter PHP-based solutions since, even in 2021, it is the dominant web programming language used by more websites than any other programming language.

In this project you will be tasked to prepare storage infrastructure on two Linux servers and implement a basic web solution using WordPress. WordPress is a free and open-source content management system written in PHP and paired with MySQL or MariaDB as its backend Relational Database Management System (RDBMS).

Project 6 consists of two parts:
1. Configure storage subsystem for Web and Database servers based on Linux OS. The focus of this part is to give you practical experience of working with disks, partitions and volumes in Linux.
2. Install WordPress and connect it to a remote MySQL database server. This part of the project will solidify your skills of deploying Web and DB tiers of Web solution.

### Three-tier Architecture
Generally, web, or mobile solutions are implemented based on what is called the **Three-tier Architecture.**
**Three-tier Architecture** is a client-server software architecture pattern that comprise of 3 separate layers.
1. Presentation Layer (PL): This is the user interface such as the client server or browser on your laptop.
2. Business Layer (BL): This is the backend program that implements business logic. Application or Webserver
3. Data Access or Management Layer (DAL): This is the layer for computer data storage and data access. Database Server or File System Server such as FTP server, or NFS Server

### Our 3-Tier Setup
1. A Laptop or PC to serve as a client
2. An EC2 Linux Server as a web server (This is where you will install WordPress)
3. An EC2 Linux server as a database (DB) server

**We will use RedHat OS for this project**
By now you should know how to spin up an EC2 instanse on AWS, but if you forgot – refer to [Project1 Step 0](https://github.com/samuelede/devops-pbl-projects/tree/main/project1#step-0--web-stack-implementation-lamp-stack-in-aws)
