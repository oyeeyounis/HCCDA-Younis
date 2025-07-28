# Storage Services Practice

# 1.1.1 About This Exercise
EVS provides persistent block storage for ECSs and BMSs. With data redundancy and cache accel
eration techniques, EVS disks deliver high availability and durability as well as stable, low latency. 
You can initialize EVS disks, create file systems on them, and store data persistently on them. This 
exercise describes basic EVS operations, such as purchasing and attaching EVS disks.

# 1.1.2 Objectives
Upon completion of this exercise, you will be able to:
1、Purchase EVS disks.
2、Attach EVS disks.
3、Initialize EVS disks on Windows and Linux servers.
4、Use EVS snapshots.
1.1.3 Tasks
1.1.3.1 Roadmap
EVS disks are usually used to increase user's storage space to meet their business needs. You can 
buy EVS disks for use, or detach and delete them if they are no longer required. This exercise intr
oduces how to use an EVS disk in Windows and Linux.

1、EVS disks can be used as system disks or data disks for cloud servers. When a cloud server is p
urchased, a system disk is automatically purchased and attached. You cannot purchase a system 
disk separately.
2、Data disks can be purchased during or after the server purchase. If you add data disks during t
he server purchase, the system will automatically attach the data disks to the server. If you purcha
se data disks after the server has been purchased, you need to manually attach the data disks.
3、In this exercise, we will buy two Windows ECSs ecs-vivi and ecs-test in the AP-Singapore regio
n, buy an EVS disk separately and attach it to ECS ecs-vivi, and create a test file on the disk. Then, 
detach this disk and attach it to ECS ecs-test, and log in to ECS ecs-test to check whether the test 
file exists.

# Prerequisites: Log in to HUAWEI CLOUD.

Go to the [Lab Desktop] and open the browser to access the HUAWEI CLOUD login page. Select I
AM User Login. In the login dialog box, enter the assigned HUAWEI CLOUD lab account and pass
word to log in to HUAWEI CLOUD, as shown in the HUAWEI CLOUD Lab Account.

Step 2 In Service List on the left, choose Virtual Private Cloud.

Step 3 Click Create VPC

Step 4 Configure the VPC parameters as follows and click Create Now.
Basic Information

1、Region: AP-Singapore
2、Name:vpc-WP
3、IPv4 CIDR Block: 192.168.0.0/16
Default Subnet
1、AZ:AZ1
2、Name: subnet-WP
3、IPv4 CIDR Block: 192.168.0.0/24
4、Retain the default settings for other parameters.
Note: Replace the VPC name vpc-WP and the default subnet name subnet-WP with the account n
ame assigned by the system, for example, vpc-Sandbox-voyager002 and subnet-Sandbox-voyage
r002.

Step 5 Switch to Virtual Private Cloud page and view the created VPC.

Step 6 Click Service List on the left and choose Compute > Elastic Cloud Server.

Step 7 Click Buy ECS.

Step 8 Configure basic settings as follows:
1、Billing Mode: Pay-per-use
2、Region: AP-Singapore
3、AZ: AZ1
4、CPU Architecture: x86
5、Specifications: General computing, s6.large.2, 2 vCPUs | 4 GB (configure based on your require
ments)

1.Image: Public Image, Windows, Windows Server 2012 R2 Standard 64bit

2.Host Security: Select Enable (basic edition for this exercise).
3.System Disk: High I/O, 40 GB

Step 9 Click Next: Configure Network. The Configure Network page is displayed. Configure the pa
rameters as follows:

1.Network: Choose the created VPC.2、Extension NIC: Retain the default settings.
3.Security Group: Retain the default settings.
4.EIP: Not required

Step 10 Click Next: Configure Advanced Settings. The Configure Advanced Settings page is displa
yed. Configure the parameters as follows:

1.ECS Name: ecs-vivi
2.Login Mode: Password
3.Password：Define by yourself (Keep the password secure. If you forget the password, you can 
log in to the ECS console and change it.)
4.Confirm Password：Keep same with the above
5.Cloud Backup and Recovery: Not required
6.ECS Group (Optional): Retain the default settings.
7.Advanced Options: Retain the default settings

Step 11 Click Next: Confirm. After confirming the ECS configurations, select I have read and agree 
to the Service Level Agreement and Image Disclaimer, and click Submit. After about 10 seconds, y
ou can view the created ECS on the Elastic Cloud Server page
If the Status is Running, the ECS can work normally.

Step 11 Click Next: Confirm. After confirming the ECS configurations, select I have read and agree 
to the Service Level Agreement and Image Disclaimer, and click Submit. After about 10 seconds, y
ou can view the created ECS on the Elastic Cloud Server page
If the Status is Running, the ECS can work normally.

Step 13 Click Buy Disk.

Step 14 Set disk parameters as follows:

1.Billing Mode: Pay-per-use
2.Region: AP-Singapore
3.AZ: AZ1
4.Disk Type: High I/O (If this type is unavailable, select one available on the console.)
5.Disk Size: 20 GB
6.More: Do not configure this parameter.
7.Disk Name: volume-vivi (custom)

Step 15 Click Next.

Step 16 On the Details page, confirm the disk configuration. If you need to modify the configurati
on, click Previous. If not, click Submit.

Step 17 Go back to the disk list page and view the disk status. When the disk status changes to A
vailable, the disk has been purchased.

# 1.1.3.2.2 Attaching a Non-shared EVS Disk
Separately purchased EVS disks are data disks. In the EVS disk list, the function of such disks is Da
ta disk, and their status is Available. Data disks need to be attached to servers for use.
System disks are purchased along with servers and are automatically attached. In the EVS disk list, 
the function of such disks is System disk, and their status is In-use. After a system disk is detache
d from a server, the disk function changes to Bootable disk, and the disk status changes to Availa
ble. (A non-shared EVS disk is similar to a physical SSD or SATA disk. After attached, a non-shared 
disk can be partitioned into the C, D, and E drives for use.)
Step 1 In the EVS disk list, locate the EVS disk to be attached and click Attach in the Operation column.

Step 2 Select the target Windows ECS and select a mount point from the drop-down list. The ECS 
and EVS disk must be in the same AZ.

Step 3 Go back to the EVS disk list page. The disk status is Attaching, indicating that the disk is be
ing attached to the server. When the disk status changes to In-use, the disk has been attached. Y
ou must initialize the disk before using it.

# 1.1.3.2.3 Initializing an EVS Disk
After a data disk is attached to an ECS, you must log in to the ECS and initialize the disk before us
ing it.
Step 1 Locate the row that contains the target ECS and click Remote Login in the Operation colu
mn.
Step 2 Log in using Remote Login on the management console. On the desktop of the ECS, choo
se Start > Server Manager. On the dashboard, choose Tools > Computer Management.

Step 3 In the navigation tree on the left, choose Storage > Disk Management.

Step 4 On the Disk Management page, if the status of new disk is Offline, right-click Offline and c
hoose Online to online the disk. If the status is Not Initialized, right-click the status and choose Ini
tialize Disk.
In the Initialize Disk window, select the target disk, click MBR (Master Boot Record) or GPT (GUID 
Partition Table), and click OK.
Step 5 Right-click the unallocated area and choose New Simple Volume.

Step 6 In the displayed New Simple Volume Wizard window, click Next.

Step 7 Specify the volume size and click Next. The default value is the maximum size.

Step 8 Assign a drive letter and click Next.

Step 9 Select Format this volume with the following settings, set parameters based on the require
ments, and select Perform a quick format. Then, click Next.

Step 10 Click Finish. Wait for the initialization to complete. When the volume status changes to H
ealthy, the initialization is complete.

Step 11 Open This PC. If a new volume appears, the disk has been attached.

# 1.1.3.2.4 Detaching an EVS Disk and Performing Verification

Before you detach an EVS disk on the console, log in to the ECS and unmount the disk.
To verify that data on a detached EVS disk can still be used, we will detach the disk and then attac
h it to another ECS for verification.

Step 1 Locate the row that contains the target ECS and click Remote Login in the Operation colu
mn.
Step 2 Create a test file test.txt on the attached EVS disk

Step 3 Open the Disk Management window and bring the EVS disk offline. 

Step 4 Open This PC and check that volume D disappears. 

Step 5 Buy another Windows ECS (Windows Server 2012 R2 Standard 64-bit English) by referring 
to the preceding sections. 

Step 6 Detach the EVS disk from ECS ecs-vivi and attach it to ECS ecs-test, the newly purchased ECS. 

Step 7 Log in to the ECS console, find ECS ecs-test, and click Remote Login. 

Step 8 Open the Disk Management window and check that the EVS disk is online. 

Step 9 Check whether test file test.txt exists. 

The file exists, verifying that this exercise succeeds. 

# 1.1.3.3 Attaching an EVS Disk to a Linux ECS 

Step 1 Create a Linux ECS (CentOS 7.6 64 bit). Configure the parameters the same as creating the 
Windows ECS, except for ECS Name, Image, and Login Mode. 

Step 2 Purchase a non-shared EVS disk and name it volume-linuxadd by referring to the precedin
 g section, and attach the disk to the purchased ECS. (When purchasing the disk, select the AZ wh
 ere the Linux ECS resides for the disk.) 
 
Step 3 Remotely log in to the Linux ECS and run the following command to view the new data dis
 k: 
                               *fdisk -l*
                             
The command output shows that the ECS has two disks, system disk /dev/vda and data disk /dev
 /vdb. 
 
Step 4 Run the following command to enter fdisk to partition the new data disk: 
In this example, run the following command: 
                                *fdisk /dev/vdb* 
                             
Enter n and press Enter to create a partition. 

Step 5 In this example, a primary partition is created. Therefore, enter p and press Enter to create 
a primary partition. Enter the partition number of the primary partition and press Enter.Partition n
 umber 1 is used in this example. 
First sector indicates the start sector. The value ranges from 2048 to 20971519, and the default va
 lue is 2048. 
 
Step 6 Press Enter. The default first sector 2048 is used. 
Last sector indicates the end sector. The value ranges from 2048 to 20971519, and the default val
 ue is 20971519. 
 
Step 7 Press Enter. The default last sector 20971519 is used. 
A primary partition has been created for a 10-GB data disk. 

Step 8 Enter p and press Enter to view details about the new partition. 
Details about the /dev/vdb1 partition are displayed. 

Step 9 Enter w and press Enter to write the changes into the partition table. 
In case that you want to discard the changes made before, you can exit fdisk by entering q. 

Step 10 Run the following command to synchronize the changes in the partition table to the OS: 
partprobe.

Step 11 Run the following command to set the file system format for the new partition: 
mkfs -t File system format /dev/vdb1 
In this example, run the following command to set the ext4 file system for the new partition: 
mkfs -t ext4 /dev/vdb1 
The formatting takes a period of time. Wait until the task status changes to done. 

Step 12 Run the following command to create a mount point: 
In this example, run the following command to create a mount point /mnt/sdc: 
mkdir /mnt/sdc 

Step 13 Run the following command to mount the new partition on the created mount point: 
In this example, run the following command to mount the new partition on /mnt/sdc: 
mount /dev/vdb1 /mnt/sdc 

Step 14 Run the following command to view the mount result: 
df -TH 
New partition /dev/vdb1 has been mounted on /mnt/sdc. 

# 1.1.3.4 (Optional) Setting Automatic Mounting at System Start 

Step 1 In the Linux ECS, run the command to query the UUID of the disk partition. 
In this example, run the following command to obtain the UUID of /dev/vdb1: 
blkid /dev/vdb1 

Step 2 Run the following command to open the fstab file: 
*vi /etc/fstab* 
Press i to enter editing mode and add the following content (replace the UUID with what you hav
 e obtained): 
 
*/mnt/sdc  ext4  defaults  0 2 
UUID= 8493dccb-1a8c-4225-8e9c-84eb1243cf23* 
Press Esc, enter :wq, and press Enter to exit editing mode. 

Step 3 Run the command to unmount the partition. In this example, run the following command: 
umount /dev/vdb1 

Step 4 Run the following command to reload all the content in the /etc/fstab file: 
mount -a 

Step 5 Run the following command to query the file system mounting information: 
mount | grep /mnt/sdc 

# 1.1.3.5 (Optional) Using Snapshots 

Step 1 On the ECS ecs-linux, run the following commands to create a test file: 
mkdir /mnt/sdc/snapshot 
cd /mnt/sdc/snapshot 
echo "snapshot test"> test.file 
cat test.file 

Step 2 Locate the EVS disk purchased before and choose More > Create Snapshot in the Operation column. 
 
Step 3 Name the snapshot volume-linuxdata and click Create Now. 

Step 4 Go back to the disk list. Choose Snapshots in the navigation pane on the left, locate the volume-linuxdata snapshot, and click Create Disk in the Operation column. 

Step 5 Buy a disk according to the following figure. 

Step 6 View the disk created from the snapshot. 

Step 7 Attach the disk to ECS ecs-linux. 

Step 8 Log in to ECS ecs-linux and view the new data disk. 
fdisk -l 

Step 9 Run the following command to create a mount point: 
mkdir /mnt/mdc 

Step 10 Run the following command to mount the new partition /dev/vdc1 on /mnt/mdc: 
mount /dev/vdc1 /mnt/sdc 

Step 11 Switch to /mnt/sdc and check whether the snapshot file has been synchronized. 
cd /mnt/sdc/snapshot 
ls cat test.file 
If the preceding command output is returned, the snapshot file has been synchronized.

# 1.2.1 About This Exercise 

OBS provides a stable, secure cloud storage with high scalability and ease of use. It allows users t
 o store virtually any amount of unstructured data in any format, and allows them to access data fr
 om anywhere using REST APIs. Objectives 
Upon completion of this exercise, you will be able to: 
1. Perform OBS operations, such as creating buckets and folders, uploading, downloading, and d
 eleting files or folders, and deleting buckets. 
 
# 1.2.2 Tasks 
# 1.2.2.1 Roadmap 

1.When users log in to OBS Console using their HUAWEI CLOUD account or as an IAM user, OBS authenticates their account or IAM user credentials. 

2. When users access OBS using the tools (OBS Browser+ or obsutil), SDKs, or APIs, OBS requires 
access keys (AK and SK) for authentication. Therefore, users need to obtain the access keys (AK a
 nd SK) before they access OBS using any methods other than OBS Console. 
 
#1.2.2.2 Creating a Bucket 
Step 1 Log in to the HUAWEI CLOUD console, and choose the AP-Singapore region. 
Step 2 In Service List on the left, choose OBS. click Create Bucket. 
Step 3 In the Create Bucket dialog box, configure the following parameters: 

1.Region: AP-Singapore 
2.Default Storage Class: Select Standard. 
3.Bucket Policy: Private 
4.Multi-AZ Mode: It is disabled by default. 
5.Bucket Name: test-vivi is used as an example. You can hover your cursor over the tooltip to vi
 ew the bucket naming rules. 
 
Step 4 Click Create Now. A dialog box is displayed, indicating whether the bucket is created. 

# 1.2.2.3 Uploading a File or Folder 

Step 1 Click the name of the created bucket and Objects to go to the object list page. 
Step 2 Click Upload Object. 
Step 3 In the Upload Object dialog box, click add file. 
Step 4 Select the files（Such as: background.jpg）be uploaded and click Upload. 
Step 5 View the uploaded file or folder in the list. 

# 1.2.2.4 Downloading a File or Folder 

Step 1 In the object list, select the file or folder to be downloaded and click Download. 

Step 2 In the dialog box, select a path for saving the downloaded file on your local PC . 
# 1.2.2.5 Deleting a File or Folder 

Step 1 In the object list, select the file or folder to be deleted, and choose More > Delete in the O
 peration column. 
 
Step 2 In the Delete dialog box, click Yes. 

# 1.3.1 About This Exercise 

SFS provides reliable, high-performance shared file storage hosted on HUAWEI CLOUD. With SFS, 
you can enjoy shared file access spanning multiple ECSs, BMSs, and containers created on CCE an
 d CCI. This exercise describes basic SFS operations. 
 
# 1.3.2 Objectives 
Upon completion of this exercise, you will be able to: 
1.Create an SFS Turbo file system. 
2.Mount an SFS Turbo file system on Linux and Windows servers. 
3.Enable cloud servers in different VPCs to share the same SFS file system. 

# 1.3.3 Tasks 

# 1.3.3.1 Creating an SFS Turbo File System 

# 1.3.3.1.1 Prerequisites 

1.A VPC vpc-mp has been created. 
2.A Linux ECS ecs-linux running CentOS 7.6 has been purchased. An EIP has been bound to the 
ECS, and the ECS locates in VPC vpc-mp. 
3.A Windows ECS ecs-windows running Windows Server 2012 has been purchased. An EIP has b
 een bound to the ECS, and the ECS locates in VPC vpc-mp. 
 
# 1.3.3.1.2 Binding the EIP to the ECS 

Step 1 Log in to the HUAWEI CLOUD console and choose Elastic IP in the service list. 

Step 2 On the displayed page, click Buy EIP. 

Step 3 Set the parameters as prompted. 

1.Billing Mode: Pay-per-use 
2.Region: AP-Singapore 
3.EIP Type: Dynamic BGP 
4.Billed By: Traffic 
5.Bandwidth (Mbit/s): 5 
6. Quantity: 2 
Retain the default settings for other parameters. 
Step 4 Click Next and Submit. 

Step 5 In the EIP list, locate the row that contains the target EIP, and click Bind. 

Step 6 Select the instance to which you want to bind the EIP and click OK.

Step 7 An EIP has been bound to the ECS, and perform the same operation to the other ECS 

# 1.3.3.1.3 Creating an SFS File System 

Step 1 Log in to the HUAWEI CLOUD console and choose Scalable File Service in the service list. 

Step 2 Click Create File System. 

Step 3 On the displayed page, set the name, file system type, and VPC for the file system you are 
creating. 

1.Billing Mode:Pay-per-use 
2.Region: AP-Singapore 
3.File System Type:General 
4.Storage Class:Standard 
5.Capacity (GB):500 
6.Protocol Type: NFS 
7.VPC: Select the created one 
8.Name: sfs-mp 
9.Retain the default settings for other parameters. 

Step 4. Click Next. 

Step 5. On the Details page, confirm the configuration and click Submit. 

Step 6. A message is displayed indicating that the request has been submitted. 

Step 7 Go back to the SFS console and view the result. 
# 1.3.3.2 Mounting an SFS File System to a Linux ECS 
# 1.3.3.2.1 Procedure 
Step 1 Go to the ECS console. Locate the row that contains the purchased ECS and click Remote L
 ogin. 
Step 2 Log in the ECS as user root. 

Step 3 Run the following command to check whether the NFS software package has been installe
 d in the operating system (generally available in the operating system): 
rpm -qa |grep nfs 
If information similar to the preceding figure is returned, the NFS software package has been inst
 alled. The command output varies with the operating system. 
 
Step 4 If no command output is returned, the NFS software package is not installed. Run the resp
 ective command to install the NFS software package. In this exercise, CentOS 7.6 bit is used as an 
example. 
1、In CentOS, Red Hat, EulerOS, Fedora, or Oracle Enterprise Linux, run the following command: 
sudo yum -y install nfs-utils 

Step 5 Run the following command to install the bind-utils software package: 
yum install bind-utils 
Log in to the SFS console, click the file system to be mounted, and view the mount. 
Note that information in the red box is the domain name of the file system. 

Step 6 If information similar to the following is displayed, IP addresses have been mapped to the 
file system domain name. 

Step 7 Run the mkdir /local path command to create a local directory for mounting the file syste
 m. mkdir /localfolder 
 
Step 8 Run the following command to mount the file system on the local path: 
mount -t nfs -o vers=3,timeo=600,nolock Mount address of the SFS file system /local path 
In this example, run the following command: 
*mount -t nfs -o vers=3, timeo=600, nolock
nslookup sfs-nas01.ap-southeast-2a.myhuaweicloud.com:/share-c343b993 /localfolder*

Step 9 Run the following command to view the mounted file system: 
mount -l 

Step 10 Run the following command to edit the fstab file: 
vi /etc/fstab 
Press i to enter editing mode. At the end of the file, add the file system information. In this exam
 ple, add the following content: 
sfs-nas01.ap-southeast
2a.myhuaweicloud.com:/share-c343b993 /localfolder nfs vers=3, timeo=600, nolock 0 0 
Press Esc, enter :wq, and press Enter to save and exit. 
Replace Mount address and /localfolder with those used in your environment. 

Step 11 Run the following command to view the changes of fstab: 
cat /etc/fstab 

Step 12 Restart the ECS. reboot 

Step 13 Log in to the system and run the following command to view the mounted file system: 
mount -l 

Step 14 Create file new. 
cd /localfolder vim new 

Step 15 Press i to enter editing mode. Enter Hello HuaweiCloud SFS, press Esc, and enter :wq to e
 xit editing mode and save the change. 
 
Step 16 Run the following command to view the file content: 
cat /localfolder/new 
Now that the file system has been mounted to the ECS and can be used. 

# 1.3.3.3 Mounting an SFS File System to a Windows ECS 

# 1.3.3.3.1 Logging In to a Windows ECS 

Step 1 Log in to the ECS console. Locate the row that contains the purchased Windows ECS and c
 lick Remote Login. 
 
# 1.3.3.3.2 Installing the NFS Client 

Step 1 Open Server Manager by clicking the icon in the lower left corner. 
Step 2 Click Add Roles and Features and click Next for three consecutive times to go to the Serve
 r Roles page. 
Step 3 Under File and Storage Services, click Server for NFS. In the displayed window, click Add Fe
 atures. 
Step 4 Click Next. On the Features page, click Client for NFS. 
Step 5 Click Next to go to the Confirmation page. 
Step 6 Click Install. 
Step 7 After the installation is complete, restart the client and log to the ECS again as prompted. 

# 1.3.3.3.3 Mounting the File System

Step 1 Open Control Panel and choose to view by category. 
Step 2 On the Control Panel, choose System and Security > Administrative Tools > Services for N
 etwork File System (NFS). 
Step 3 Right-click Client for NFS and choose Properties. In the displayed dialog box, change the tr
 ansport protocol to TCP and select Use hard mounts as the default mount type. 


Step 4 Run the following command in the Command Prompt of the Windows Server 2012 (X is th
 e drive letter of the free disk): 
 
For the SFS Turbo file system, run the following command: 
mount -o nolock -o casesensitive=yes IP:/! X: 

You can get the IP address from the SFS Turbo 
(The mount address varies with the file system. Replace this mount address with your file system'
 s mount address. Do not copy the address in this example.) 
 
# 1.3.3.3.4 Verification 

Step 1 On the Windows ECS, open This PC to check that the mounted file system is available. 


Step 2 Access !(\\192.168.0.226)(X:) and check that file new exists. This file is created in the file sys
 tem from ECS ecs-linux, indicating that the SFS Turbo file system can be shared among servers. 
Contents
