# LAB : Deploying an Enterprise Web
An enterprise intends to deploy their website on HUAWEI CLOUD and they have the 
following requirements:
1.Database nodes and service nodes are deployed on separate ECSs.
2.ECSs are added or removed as incoming traffic changes over time.
# Prerequisites:
Log in to HUAWEI CLOUD.Go to the [Lab Desktop] and open the Google 
Chrome browser to access the HUAWEI CLOUD login page. Select IAM User Login. In the 
login dialog box, enter the assigned HUAWEI CLOUD lab account and password to log in to 
HUAWEI CLOUD.
![Huawei_login_Screen_Shot](imagess/login.png)

# 1.Tasks
1.1 Creating a VPC
Step 1 Switch to the management console, and select the AP-Singapore region. In the left 
navigation pane, choose Service List > Networking > Virtual Private Cloud.
Step 2 Click Create VPC.

Step 3 Configure the parameters as follows, and click Create Now.

● Region: AP-Singapore

● Name: vpc-mp (Change it as needed.)

● Retain the default settings for other parameters.

Step 4 View the created VPC in the VPC list.

# 1.2 Creating and Configuring a Security Group

Step 1 On the Network Console, choose Access Control > Security Groups and create a 
security group.

Step 2 Click the security group name.
Step 3 Click Inbound Rules and then Add Rule to add an inbound rule with the following 
parameter settings:

● Protocol & Port: All

● IP address in Source: 0.0.0.0/0

# 1.3 Buying an ECS
Step 1 In the service list, choose Compute > Elastic Cloud Server.

Step 2 Click Buy ECS and set the following parameters.
Basic settings:

● Billing Mode: Pay-per-use

● Region: AP-Singapore

● AZ: Random

● CPU Architecture: x86

● Specifications: General computing, s6.small.1 1 vCPUs | 1 GB

● Image: Public image, CentOS 7.6 64bit (40 GB)

● System Disk: High I/O, 40 GB

Network configuration:

● Network: Select the VPC you have created.

● Security Group: Select the security group you have created.

● EIP: Auto assign, Dynamic BGP, Billed by Bandwidth, 2 Mbit/s

Advanced settings:
● ECS Name: ecs-mp (Change it as needed.)

● Login Mode:Password, for example, Huawei@123!

● Cloud Backup and Recovery: Not required

Step 3 Confirm the configuration, select I have read and agree to the Service Level 
Agreement and Image Disclaimer, and click Buy Now.

Step 4 View the purchased ECS in the ECS list.

# 1.4 Buying an RDS DB Instance
Step 1 Go back to the service list, and choose Database > Relational Database Service.

Step 2 Click Buy DB Instance.
Step 3 Set the parameters as follows and click Next.

● Billing Mode: Pay-per-use

● Region: AP-Singapore

● Instance parameters: rds-name (customizable), MySQL, 8.0, Primary/Standby, Cloud SSD

● Performance specifications: 2 vCPUs | 4 GB. Determine the specifications based on real-world 
service requirements.

● VPC, Security Group, and Password: Select the VPC and security group you have created. 
Set the password, for example, Huawei!@#$.


● Retain the default settings for other parameters.

Step 4 Confirm the configuration, and click Submit. Go to the RDS DB instance list, and wait 
for the creation to complete, which takes 6 to 10 minutes.

Step 5 Click the DB instance name to view its floating IP address.

# 2.Setting Up the Linux, Apache, MySQL, PHP (LAMP) Environment

2.1 Installing LAMP

Step 1 Go back to the ECS console and click Remote Login in the Operation column of the 
purchased ECS.

Step 2 In the VNC window, enter the username (root for Linux ECSs by default) and password 
for login.

Step 3 Run the following command to install LAMP and enable the services you will need:
 Copy Codeyum install -y httpd php php-fpm php-mysql mysql
If Complete! is displayed, LAMP has been successfully installed.

Step 4 Configure httpd:

 Copy Codevim /etc/httpd/conf/httpd.conf

 Step 5 In the configuration file, press Shift+G to go to the last line of the configuration file, 
press I to enter the editing mode, move the cursor to the end of the configuration file, and press 
Enter. Then copy and paste the following content:
 Copy CodeServerName localhost:80

 Step 7 Run the following command to download the WordPress installation package:
 
 Copy Codewget -c https://koolabsfiles.obs.ap-southeast3.myhuaweicloud.com:443/20220731/wordpress-4.9.10.tar.gz
If wordpress-4.9.10.tar.gz is displayed, the WordPress installation package has been 
downloaded.

Step 8 Run the following command to decompress the WordPress installation package to the 
/var/www/html directory:

 Copy Codetar -zxvf wordpress-4.9.10.tar.gz -C /var/www/html
The command output similar to the following is displayed. 

Step 9 Run the following command to grant the read and write permissions to the directory 
where the file is located:
 Copy Codechmod -R 777 /var/www/html
 
Step 10 Run the following command to enable httpd:
 Copy Codesystemctl start httpd.service
 
Step 11 Run the following command to enable php-fpm:
 Copy Codesystemctl start php-fpm.service
 
Step 12 Run the following command to check the httpd status, which should be active (running)
and highlighted:
 Copy Codesystemctl status httpd

 Step 13 Run the following command to check the php-fpm status, which should be active 
(running) and highlighted:

 Copy Codesystemctl status php-fpm
 
Step 14 Run the following command to make httpd automatically start at boot. If information 
similar to what shown in the figure is displayed, httpd has been configured to automatically start 
at boot.

 Copy Codesystemctl enable httpd
 Step 15 Run the following command to configure php-fpm automatically start upon system boot. 
If information similar to what shown in the figure is displayed, php-fpm has been configured to 
automatically start upon system boot.
 Copy Codesystemctl enable php-fpm
 
Step 16 In the browser, access the EIP bound to the ECS. If the following figure is displayed, 
LAMP has been installed.

# 2.2 Creating a Database for WordPress

Step 1 Go back to the RDS console and click Log In in the Operation column of the created 
RDS MySQL database instance.

Step 2 Enter the username (root by default) and password (you set when purchasing the RDS 
instance). Select Remember Password, enable Collect Metadata Periodically and Show 
Executed SQL Statements. If the connection test is successful, click Log In.

Step 3 On the top menu bar, choose SQL Operations > SQL Query, as shown in the following 
figure. Delete the default content in the command line under SQL Window.

Step 4 Enter the following SQL statement and click Execute SQL. If the following information 
is displayed, the database for WordPress has been created.
 Copy Codecreate database wordpress

 # 2.3 Installing WordPress
Step 1 In the address box of the browser, enter http://ECS EIP/wordpress to access the 
WordPress installation wizard.

Opening the WordPress installation wizard
Step 2 Click Let's go!. in the displayed page, enter the database access information, and click
Submit.

● Database Name: wordpress

● Username: root

● Password: Enter the password you set.

● Database Host: Enter the database floating IP address and port number obtained in section 
Buying an RDS DB Instance.

● Table Prefix: Retain the default settings.

● Click Run the installation.

● Set Site Title, Username, Password, and Your Email, and click Install WordPress

Step 3 Enter the user name and password on the displayed login page. Then, click Log In

Now the initial configurations of the WordPress website server and its back-end database 
instance are complete. Next, we will configure ELB and AS for the WordPress website server.

# 3.Achieving High Availability for Web Servers
To ensure high availability, enterprises usually deploy their applications on more than one 
server, use ELB to distribute incoming traffic across these servers, and use AS to scale in or out 
servers on demand. In this exercise, we will use the website you built in the preceding exercise 
as an example to describe how you can configure ELB to distribute incoming traffic across the 
web servers, and we will use AS to improve the availability of the website.

# 3.1 Creating a Shared Load Balancer

Step 1 On the management console, hover on the upper left to display Service List and choose 
Networking > Elastic Load Balance.

Step 2 Click Buy Elastic Load Balancer.

Step 3 Configure the parameters as follows and click Next.

● Type: Shared load balancer

● Region: AP-Singapore

● Name: elb-mp (Change it as needed.)

● Network type: Public network

● VPC: the VPC and subnet you created

● EIP: New EIP, Dynamic BGP, Bandwith, 2 Mbit/s

Step 4 Confirm the configuration and submit your request.

Step 5 Go back to the load balancer list and ensure that the load balancer is in the Running state.

Step 6 Click the name of the load balancer. Under Listeners, click Add Listener. Configure the 
name, protocol, and port for the listener.

Step 7 Click Next, configure the backend server group, and click Finish.
● Name: listener-mp (Change it as needed.)

● Remain the default settings for other parameters.

Step 8 Click Next, close Health Check and click Next.

● Health Check: disabled

Now that the ELB configuration is complete, we need to configure some backend servers for AS. 
They will be added to or removed from the backend server group based on how much traffic 
there is. Before you configure AS, create a private image on the IMS console. This image will be 
used by the system to create these ECSs.

# 3.2 Creating an Image

Step 1 Go back to the ECS console, locate the ECS you created, and choose More > Stop in the 
Operation column

Step 2 Go back to the service list. Under Compute, click Image Management Service.

Step 3 Click Create Image and configure the parameters as follows:

● Type: System disk image

● Source: the ECS you created

● Name: ims-mp (Change it as needed.)

Step 4 Click Next, confirm the configuration, and click Submit.Step 5 Wait until the image status becomes Normal. Then, switch back to the ECS console, and 
start the ECS.

# 3.3 Configuring AS
Step 1 Go back to the service list. Under Compute, click Auto Scaling.

Step 2 Click Create AS Configuration.

Step 3 Select the system disk image and security group you just created and set EIP to Do not use.

Step 4 View the created AS configuration.

Step 5 Click Create AS Group.

Step 6 Configure the parameters.

Step 7 Select the AS configuration and load balancer you just created. AS will dynamically 
adjust the number of ECSs in the backend server group using the image configured or used in the 
AS configuration.

Step 8 Locate the AS group you created and click View AS Policy in the Operation column.

Step 9 Under AS Policies, click Add AS Policy.

● Trigger Condition: CPU Usage, Max., >=, 60. Scaling Action: Add, 1, instances

● Trigger Condition: CPU Usage, Avg., <=, 20. Scaling Action: Reduce, 1, instances

Step 10 Wait for about 2 minutes and check whether the AS policy has taken effect. As we can 
see in the following figure, two ECSs have been added to the AS group. The AS policy has taken 
effect.

Step 11 Switch back to the ELB console and click the load balancer name, elb-mp. Locate the 
backend server group associated with the load balancer and view the two ECSs added by the AS 
service.

Step 12 Verify that web servers where the website is deployed can be accessed using the EIP 
bound to the load balancer. We have finished configuring AS and verified that AS can 
dynamically adjust the number of ECSs in the backend server group associated with the load 
balancer based on the configured AS policy.

# 4.Visiting the Website

Step 1 In the address box of the browser on your PC, enter http://Load balancer's 
EIP/wordpress/, and press Enter.

Step 2 Check whether the website can be accessed. If the website can be accessed, web servers 
where the website is deployed can provide Internet-accessible services using the load balancer's 
EIP.

# 5.Monitoring Resources
Step 1 On the service list page, choose Management & Governance > Cloud Eye.

Step 2 On the Overview page, view overall resource information and alarm statistics.

Step 3 In the left navigation pane, choose Alarm Management > Alarm Records. View service 
alarms and handle any faults in a timely manner.

Step 4 In the left navigation pane, choose Server Monitoring > Elastic Cloud Server and then 
view ECS monitoring information.

Step 5 Click the name of an ECS to view its monitoring details






