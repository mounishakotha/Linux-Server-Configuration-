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
- Now, click on launch wizard-1 and click on **Inbound**.
- In Inbound, click on edit and add 3 rules i.e,add port SSh 2200, Http port 80, NTP port 123 and save. 

 #### Public IP Address : 3.81.217.0
 #### Accessable Port : 2200
 
 ## Steps to configure Linux server
 
 **Step1.** Create a new folder and paste the downloaded pem file there.
 
 **Step2.** Open it by using a command ```ssh -i filename(linux_server_31_01_2019).pem ubuntu @ IP address``` .
 
 **Step3.** Now, update it,
```
        sudo apt-get update
        sudo apt-get updrage      
```

**Step4.** Now change port 22 to port 2200 ```sudo vi /etc/ssh/sshd_config```
    In this file, change the port number to 2200 and save and exit (esc+:wq).
    
 **Step5.** Now restart the service ```sudo service ssh restart```
 
 **Step6.** Now open the file with ssh port 2200
```
ssh -i linux_server_31_31_2019.pem -p 2200 ubuntu@IP address
```
**Step 7.** Now add the following commands:
```
     sudo ufw default deny incoming
     sudo ufw default allow outgoing
     sudo ufw default allow 2200/TCP
     sudo ufw default allow www
     sudo ufw default allow 123/NTP
     sudo ufw default deny 22
     sudo ufw default enable
     To check status:
     sudo ufw status
```

### Creating grader

**Step 1.** Login to ubuntu and add user ``` sudo adduser grader and password: grader```

**Step 2.** Now give the grader premissions ```sudo visudo```
         Now edit there as ```grader ALL= (ALL:ALL) ALL``` and save and exit(ctl+X)
         
**Step 3.** To verify the grader as sudo permission ```su -grader and password: grader```

**Step 4.** Now, give SSH key-pair for grader
     Cofigure keypairs for gader
     Create .ssh folder by ```mkdir /home/grader/.ssh```
     
**Step 5.** Change it to grader ```su grader password:grader```
           ``` sudo -cp /home/ubuntu/.ssh/authorized_keys /home/grader/.ssh/authorized_keys```
           
**Step 6.** Now change ownership ``` chown grader.grader /home/grader/.ssh```

**Step 7.** Now add grader to sudogroup
```
             sudo su
             usermod -aG sudo grader
```
**Step 8.** Change permissions tp .ssh folder
```
      chmod 700 /home/grader/.ssh
      chmod 644 /home/grader/.ssh/authorized_keys
      vi /etc/ssh/sshd_config
      There at authentication edit as permit root login no and save and exit(ecs+:wq)
```
**Step 9.** Now restart the service ``` sudo service ssh restart```
