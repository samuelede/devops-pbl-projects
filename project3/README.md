

DevOps PBL
Project 3 Report

Darey.io - DevOps Project Base Learning Project3 Documentation

JULY 2022


MERN STACK IMPLEMENTATION





Introduction & Background

MERN Web stack consists of following components:
MongoDB: A document-based, No-SQL database used to store application data in a form of documents.
ExpressJS: A server side Web Application framework for Node.js.
ReactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.
Node.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.
In project 3, we will implement a web solution on MERN stack in AWS Cloud.



Step 0 - Preparing prerequisites 

In order to complete this project you will need an AWS account and a virtual server with Ubuntu Server OS.
If you do not have an AWS account – go back to Project 1 Step 0 to sign in to AWS free tier account and create a new EC2 Instance of t2.nano family with Ubuntu Server 22.04 LTS (HVM) image and logi to the via the terminal.
![MERN Stack](images/MERNstack.png)

Step 1 - BackEnd Configuration


Step 1 of 1 - After setting up and/or starting a new instance, run the command: 
sudo apt update and sudo apt upgrade as shown above to get the latest ubuntu software. At the prompt type  y and hit enter to continue the process. Select all options available to restart if applicable and then ok to complete the restart process.


Step 1 of 2 - Run the folowing command to get and the Node.js location for installation.
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -


Step 1 of 3 - Run the command sudo apt-get install -y nodejs to install Node.js. 
This command installs nodejs and npm. NPM is a package manager for Node like apt for Ubuntu. 


Step 1 of 4 - Verify node installation and create a new directory for our Todo application with the following cmmands at the terminal:
 node -v then npm -v then mkdir Todo next ls to view the directory contents.
Run cd Todo to move into our application directory, then run npm init to initialize the project.

Step 1 of 5 - At the prompt type yes and hit enter and provide suitable answers at the prompt s shown above. Then run ls to confirm the package.json file has been created as shown below.





Step 1 of 6 - Next, install Express by running the command npm install express 
Then create a file indexjs with touch.js with the command touch index.js
Then run ls to confirm the index.js file was created.
Next, install the dotenv module with the command npm install dotenv
Then, run vim index.js to edit the file.
Copy and paste the following codes by right clicking in the terminal to paste into the file.

const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use((req, res, next) => {
res.send('Welcome to Express');
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});


Step 1 of 7 - Aftr pasting the code, note the port number specified as 5000 in the code. Then hit the esc key and type :w to save the file and :qa to exit vim.

