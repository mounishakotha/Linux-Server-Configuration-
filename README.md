# Linux-Server-Configuration
This project is a part of **Udacity Nanodegree Full Stack.**

This project explains how to secure and set up a Linux distribution on a virtual machine, install and configure a web and database server to host a web application. 

- The virtual private server is [Amazon EC2](https://console.aws.amazon.com/).
- The web application is my [Item Catalog project](https://github.com/mounishakotha/Item-Catlog) created earlier in this Nanodegree program.
- The database server is [PostgreSQL](https://www.postgresql.org/).

## Process for connecting to Amazon EC2:
- Open [Amazon EC2](https://console.aws.amazon.com/) and login.
- After login,Click on Start Lab.
- Click on open console and change server place to N.Virginia.
- Click on *All Services* and click on *EC2*
- Then, Click on *Launch Instance*, and select  **Ubuntu Server 18.04 LTS**.
- Select general purpose and click on **Launch and review** and again select **Launch**.
- Then, choose **Create a new pair** and giver your key-pair name (my key-pair name is : linux_server_31_01_2019) and download key-pair.
- Click on Launch Instance.
- To check the instance is created successfully or not click on view Launch log.

 #### Public IP Address : 3.81.217.0
 #### Accessable Port : 2200
 
 ## Steps to configure Linux server
 
 #### Step1. Create a new folder and paste the downloaded pem file there.
 #### Step2. Open it by using a command ```ssh -i filename(linux_server_31_01_2019).pem ubuntu @ IP address``` 
 #### Step3. Now, update it,
```
        sudo apt-get update
        sudo apt-get updrage      
```
 #### Step4. Now change port 22 to port 2200 ```sudo vi /etc/ssh/sshd_config```
    In this file, change the port number to 2200 and save and exit (esc+:wq)
 #### Step5. Now restart the service ```sudo service ssh restart```
