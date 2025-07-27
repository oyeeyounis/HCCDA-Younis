# Compute Service Lab

In this exercise, we will create both Windows and Linux ECSs.

Go to the [Lab Desktop] and open the Google Chrome browser to access the HUAWEI CLOUD log
in page. Select IAM User Login. In the login dialog box, enter the assigned HUAWEI CLOUD lab ac
count and password to log in to HUAWEI CLOUD.

# 1.1 Creating Two Types of ECSs

Step 1 Log in to the HUAWEI CLOUD console, and choose the AP-Singapore region.

Step 2 In Service List on the left, choose Virtual Private Cloud
Step 3 Click Create VPC

Step 4 Configure the VPC parameters as follows and click Create Now.

Basic Information

Region: AP-Singapore

Name:vpc-WP

IPv4 CIDR Block: 192.168.0.0/16

Default Subnet

AZ:AZ1

Name: subnet-WP

IPv4 CIDR Block: 192.168.0.0/24

Retain the default settings for other parameters

Step 5 Switch to Virtual Private Cloud page and view the created VPC.

Step 6 Click Service List on the left and choose Compute > Elastic Cloud Server

Step 7 Click Buy ECS.

Step 8 Configure basic settings as follows:
Billing Mode: Pay-per-use

Region: AP-Singapore

AZ: Random

CPU Architecture: x86

Specifications: General computing, s6.large.2, 2 vCPUs | 4 GB (configure based on your requ
irements)

Image: Public Image, Windows, Windows Server 2012 R2 Standard 64bit English(40 GB)

Host Security: Select Enable (basic edition for this exercise).
System Disk: High I/O, 40 GB

Step 9 Click Next: Configure Network. The Configure Network page is displayed. Configure the 
parameters as follows:

Network: Choose the created VPC.

Extension NIC: Retain the default settings.

Security Group: Retain the default settings.

EIP: Not required

Step 10 Click Next: Configure Advanced Settings. The Configure Advanced Settings page is di
splayed. Configure the parameters as follows:

ECS Name: ecs-windows (Change as required.)

Login Mode: Password
Password: Enter a password, for example, Huawei@1234

Cloud Backup and Recovery: Not required ECS Group (Optional): Retain the default settings.
Advanced Options: Retain the default settings.

