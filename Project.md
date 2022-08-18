## Project - 6- Web Solution with Wordpress ##

WordPress is a free and open-source content management system written in PHP and paired with MySQL or MariaDB as its backend Relational Database Management System (RDBMS).

This Project consists of two parts:

1. Configure storage subsystem for Web and Database servers based on Linux OS. The focus of this part is to give you practical experience of working with disks, partitions and volumes in Linux.

2. Install WordPress and connect it to a remote MySQL database server. This part of the project will solidify your skills of deploying Web and DB tiers of Web solution.


## Three-tier Architecture ##
Generally, web, or mobile solutions are implemented based on what is called the Three-tier Architecture.

Three-tier Architecture is a client-server software architecture pattern that comprise of 3 separate layers.

![alt](./Images/definition.JPG)

1. Presentation Layer (PL): This is the user interface such as the client server or browser on your laptop.
2. Business Layer (BL): This is the backend program that implements business logic. Application or Webserver
3. Data Access or Management Layer (DAL): This is the layer for computer data storage and data access. Database Server or File System Server such as FTP server, or NFS Server.

The connectivity procedure are;
1. A Laptop or PC to serve as a client.
2. An EC2 Linux Server as a web server (This is where you will install WordPress).
3. An EC2 Linux server as a database (DB) server.

### Step 1 —  LAUNCH AN EC2 INSTANCE THAT WILL SERVE AS “WEB SERVER by preparing a Web Server. ###
-Launch an EC2 instance that will serve as "Web Server".
![alt](./Images/Redhat%20EC2.JPG)

- Create 3 volumes in the same availability zone as your Web Server EC2, each of 10 GiB.
![alt](./Images/3%20Volumes%20creation.JPG)

- 
