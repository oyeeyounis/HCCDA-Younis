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

Step 11 Click Next: Confirm.After confirming the ECS configurations, select I have read and agre
e to the Service Level Agreement and Image Disclaimer, and click Submit. After about 10 seco
nds, you can view the created ECS on the Elastic Cloud Server page. If the Status is Running, the 
ECS can work normally


Step 12 Create a Linux ECS. Configure the parameters the same as creating the Windows ECS, exc
ept for ECS Name, Image, and Login Mode (choose Password，EIP: Auto assign).
Image: Public image, CentOS, CentOS 7.6 64-bit

# 1.2 Logging In to an ECS

Step 1 On the Elastic Cloud Server page, you can view the ECS AZ and its status. Click Remote L
ogin in the Operation column on the right.

Step 2 Locate the row containing ecs-windows, click Remote Login, and click Log In.
If Press Ctrl+Alt+Delete to sign in is displayed, click Send CtrlAltDel in the upper part of the remo
te login page.

Step 3 Click Input Commands in the upper right corner, paste the copied password, click Send, a
nd then press Enter.

Step 4 If a page similar to the one in following figure is displayed, the ECS login was successful.
Cloud Backup and Recovery: Not required ECS Group (Optional): Retain the default settings.


Step 5 In this exercise, there is no EIP bound to the Linux ECS. Therefore, you cannot use remote l
ogin tools (SSH tool) to log in to the ECS. You can choose Remote Login in the row containing ec
s-linux, and click Log In to log in to the ECS using VNC.

Linux:
ecs-linux login: root
Password: Enter a password, for example, Huawei@123.

Linux ECSs do not have a GUI. After you log in the Linux ECS remotely, enter root after ecs-li
nux login, and then press Enter to input the password. The password is entered in ciphertext
. Ensure that the password is correct before pressing Enter. If Welcome to Huawei Cloud Ser
vice is displayed, the ECS login was successful.

Step 6 If a page similar to the one in preceding figure is displayed, the Linux ECS login was succes
sful.
# 1.3 Modifying Windows ECS Specifications

Step 1 On the Elastic Cloud Server page, view the status of the target Windows ECS.

Step 2 If the ECS is not in the stopped state, select it and click Stop. If the Stop ECS page is displa
yed, select Forcibly stop the preceding ECSs and click Yes.

Step 3 After the ECS has stopped, click More in the Operation column of this ECS and choose M
odify Specifications.

Step 4 In the Modify Specifications dialog box,
select the desired ECS type, vCPUs, and memory size based on service requirements. In this exerci
se, the memory size is changed from 4 GB to 8 GB. Click Next.

Step 5 After confirming the new ECS specifications,select I have read and agree to the Image Di
sclaimer and click Submit. Go to the Elastic Cloud Server page and you will see that the ECS stat
us is Resized.

Step 6 Start the ECS. The ECS specifications have been modified.


# 2.1 Configuring a Windows ECS
Take the ecs-windows ECS you created as an example.

Step 1 Remotely log in to the ECS.

Step 2 Check whether DHCP is configured for the ECS NICs. If it is not, configure it

2. Click Network and Sharing Center
3.  Click a network connection, for example, Ethernet 2.
4. Click Properties, select Internet Protocol Version 4 (TCP/IPv4), and click Properties.
5.  If Obtain an IP address automatically and Obtain DNS server address automatically are sel
ected, DHCP has been configured. Otherwise, select the two check boxes and click OK.

Step 3 Click Start, right-click This PC, and choose Properties.In the navigation pane to the left of 
the System page, click Remote settings. Select Allow remote connections to this computer. Cli
ck OK. (The GUI varies somewhat depending on the OS version

Step 4 Go to Start > Control Panel and navigate to Windows Firewall.In the left pane, select All
ow an app or feature through Windows Firewall. Select apps that are allowed by Windows Fire
wall for Remote Desktop based on your network requirements and click OK.
In this exercise, both the private and public networks are allowed by the firewall

Step 5 Check whether Cloudbase-Init is installed on the ECS. If it is not, install it.
Go to Start > Control Panel > Programs and Features to check whether Cloudbase-Init has b
een installed on the ECS.

# 2.2 Creating a Windows Private Image

Step 1 Go back to the management console and in Service List choose Compute > Image Mana
gement Service

Step 2 On the Image Management Service page, click Create Image.

Step 3 On the Create Image page, set the following parameters and click Next.(Retain the defaul
ts for the rest of the parameters.)Region: AP-Singapore

1. Type: System disk image
2. Source: Select a Windows ECS, for example, ecs-windows.
3. Name: Enter a name, for example, image-windows2012
   
Step 4 Confirm the settings. Then, select I have read and agree to the Image Disclaimer and click Submit

Step 5 Switch back to the Private Images tab page to view the image status.

The time required for creating an image depends on the image size. Generally, it takes about 
10 to 20 minutes. When the image creation completes, its status changes to Normal. 

# 2.3 Modifying Image Information

Step 1.  Locate the row that contains the image to be modified and click Modify in the Operation column
Step 2.  You can modify the image name, memory, and other details

# 2.4 Replicating an Image Within a Region

Step 1 On the Image Management Service page, click Private Image to display the image list.

Step 2 Locate the row that contains the image to be replicated and in the Operation column choose More > Replicate.

Step 3 In the displayed Replicate Image dialog box, enter a new name for the image and click O
K. (Do not select KMS encryption.)


# 2.5 Applying for an ECS Using a Private Image

Step 1 On the Private Images tab page, locate the image and click Apply for Server in the Oper
ation column.

Step 2 On the ECS purchase page, ensure that the private image is selected.
Step 3 Go back to the ECS list to view the ECS created using the private image.

# 3.1 Configuring a Linux ECS
Take the ecs-linux ECS you created as an example.
Step 1 Remotely log in to the ECS.
Step 2 Check whether DHCP is configured for the ECS NICs. If it is not, configure it.
*For CentOS, you can configure DHCP by adding PERSISTENT_DHCLIENT="y" to the /etc/sysc
onfig/network-scripts/ifcfg-ethX configuration file using the vi editor.
 vi /etc/sysconfig/network-scripts/ifcfgeth0*

 Step 3 Check whether the one-click password reset plug-in has been installed on the ECS. If it is n
ot, install it.

Step 4 Check whether Cloud-Init is installed. If it is not, install it.

Step 5 Delete files from the network rule directory.
Note: To prevent NIC name drift on the new ECSs created from a private image, you need to 
delete network rule files of the ECS used to create the image.
Run the following command to check if there is a network rule file on the ESC:
 *ls -l /etc/udev/rules.d*

 # 3.2 Creating a Linux Private Image
Step 1 Go back to the management console and in Service List choose Compute > Image Mana
gement Service.

Step 2 On the Image Management Service page, click Create Image.
Step 3 Set the following parameters on the Create Image page and click Next.

1.Type: System disk image
2.Source: Select a Linux ECS, for example, ecs-linux.
3.Name: Enter a name, for example, image-centos7.

Step 4 Confirm the settings. Then, select I have read and agree to the Image Disclaimer and clic
k Submit.

Step 5 Switch back to the Private Images tab page to view the image status.

The time required for creating an image depends on the image size. Generally, it takes about 
10 to 20 minutes. When the image creation completes, its status changes to Normal.

# 3.3 Sharing an Image
You can share your images with other users. Before sharing images with a user, you need to 
obtain their Project ID. You can share a single image or multiple images as needed.
This document uses Windows ECS as an example. You need to use Linux ECS when performi
ng operations.

Step 1 Before sharing image with yourself, you need to find your Huawei Cloud account project I
D. Log in to the management console using your Huawei Cloud account (not SandBox user).

Step 2 Click the username in the upper right corner and select My Credentials from the drop-dow
n list.

Step 3 On the My Credentials page, view the project ID in the project list. You should use Project I
D of region “ AP-Singapore”.

Step 4 Return to the SandBox console.Using SandBox account, on the Private Images tab page, s
elect the private image to be shared and in the Operation column choose More > Share

Step 5 In the Share Image dialog box, enter your Project ID and click Add. Click OK.

Step 6 Log in to the management console using your Huawei Cloud account(not SandBox User),

# 3.4 Adding Tenants Who Can Use Shared Images

Step 1 Return to the SandBox console.On the Image Management Service page, click Private Im
age to display the image list.

Step 2 Click the name of the image to be shared. On the Shared with Tenants tab page, click Add Tenant.
go to the IMS console of “ AP-Singapore”, click the Shared Images tab, and click Accept.

Step 3 In the Add Tenant dialog box, you can enter the Project ID and click Add. (If you want to s
hare with yourself again, delete your account from list fisrt and then click Add



