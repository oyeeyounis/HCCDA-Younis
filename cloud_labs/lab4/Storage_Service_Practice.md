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
