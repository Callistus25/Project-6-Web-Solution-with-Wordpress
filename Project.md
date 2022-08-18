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
-Launch an EC2 instance that will serve as "Web Server" using Redhat OS.
![alt](./Images/Redhat%20EC2.JPG)

- Create 3 volumes in the same availability zone as your Web Server EC2, each of 10 GiB.
![alt](./Images/3%20Volumes%20creation.JPG)

- Attach all three volumes one by one to your Web Server EC2 instance you created. Please ensure that the availability zones are same.
![alt](./Images/Attaching%20volumes.JPG)

-Launch instance and SSH into the terminal. Use ``lsblk`` command to inspect what block devices are attached to the server. All devices in Linux reside in /dev/ directory. Inspect it with ls /dev/ and files name will be `xvdf, xvdh, xvdg`. 
![alt](./Images/Lsblk.JPG)

You can use command ``df -h`` to view the all mounts and free spaces on your server.
![alt](./Images/df%20-h.JPG)

- Use gdisk utility to create a single partition on each of the 3 disks `xvdf, xvdh, xvdg`.
```
sudo gdisk /dev/xvdf
```
![alt](./Images/sudo%20Gdisk.JPG)
 Note: You need to repeat this for each of the xvdf, xvdg, xvdh voulmes using hex code '8E00'.

 - Use lsblk utility to view the newly configured partition on each of the 3 disks.
 ![alt](./Images/Lsblk%20after%20partioning.JPG)

 - Install *lvm2* package using the below command; 
 ```
 sudo yum install lvm2
 ```

 - Run the below command to check for available partitions.
 ```
 sudo lvmdiskscan
 ``` 
![alt](./Images/sudo%20lvmdiskscan.JPG)

- Use ``pvcreate`` utility to mark each of 3 disks as physical volumes (PVs) to be used by LVM.
```
sudo pvcreate /dev/xvdf1
sudo pvcreate /dev/xvdg1
sudo pvcreate /dev/xvdh1
```
![alt](./Images/Sudo%20Pvcreate.JPG)

- Verify that your Physical volume has been created successfully by running below command;
```
sudo pvs
```
![alt](./Images/Sudo%20Pvs.JPG)

- Use ``vgcreate`` utility to add all 3 PVs to a volume group (VG). Name the VG webdata-vg. Verify that your VG has been created successfully by running ``sudo vgs``

```
sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1
sudo vgs
```
![alt](./Images/Sudo%20vcreate%20and%20Sudo%20vgs.JPG)

- Use lvcreate utility to create 2 logical volumes. apps-lv(website data storage) and logs-lv(log data storage)
```
sudo lvcreate -n apps-lv -L 14G webdata-vg
sudo lvcreate -n logs-lv -L 14G webdata-vg
```
![alt](./Images/Apps%20and%20logs%20storage%20creation.JPG)

- Verify that your Logical Volume has been created successfully.
```
sudo lvs
```
 ![alt](./Images/sudo%20lvs.JPG)
 



