Use the exercise account to access Lab Desktop.

# What is Lab Desktop?
Click the refresh button of the browser to refresh the exercise page.
On the exercise operation interface, open the browser, and go to the Huawei Cloud login page. Click IAM User. 
Then, use the account assigned to you to log in to Huawei Cloud.

*Note: Use the account provided by the exercise tutorial.1. Preparing the Lab Environment*

# 1.1 Creating an ECS


1. After logging in to the console, click the service list in the upper left corner and choose Elastic Cloud Server.
Note: You can enter ECS in the search box to search for it.

2. Click Buy ECS in the upper right corner

 3. Click the Custom Config tab and set Billing Mode to Pay-per-use and Region to AP-Singapore.
      
4. Select x86 for architecture and c6.xlarge.2 for flavor.
Select 4 vCPUs | 8 GiB for this exercise. This exercise is about the deployment and experience of DeepSeek 1.5B 
and this version can be deployed and run in the CPU environment. The file size is about 1.1 GB.

5. Select CentOS 8.2 64bit(40 GiB) as the image.
   
6. The default size of the system disk is 40 GB
   
7.  Next, configure the network.
VPC: Retain the default value.

*Note: If no default VPC is available, click Create VPC to create one.*

8. Security Group: Retain the default value.
Note: If no default security group is available, click Create Security Group to create one.
9. Public Network Access
EIP: Auto assign
EIP Type: Dynamic BGP
Billed By: Traffic
Bandwidth (Mbit/s): 100

*Note: The speed for Ollama to pull the DeepSeek model is unstable. If the default bandwidth is used, the downloa
d may time out. Configure the bandwidth based on the recommended bandwidth.*

10. Instance Management
ECS Name: ecs-cent
Password: Huawei1234%

(Remember the password. Note that the ECS name and password must be set to the upper ones.Otherwise, the ex
ercise progress display will be affected.)

11. Click Submit, and then click Agree and Submit.
After the creation is complete, the created ECS is displayed on the homepage.

# 1.2 Logging In to the ECS

1.Log in to the ECS remotely.

2.Use CloudShell to log in.

3.Enter the login password (Huawei1234%) and click Connect.

2. Installing Ollama

Ollama is a powerful open-source tool to help users run, manage, and deploy large language models (LLMs) loca
lly. It simplifies the installation, configuration, and running of LLMs and enables users to quickly download, ru
n, and interact with various pre-trained models. Ollama supports multiple popular open-source models (such as 
Llama, Mistral, and DeepSeek). It is especially suitable for developers to quickly exercise and develop in local en
vironments.
There are two solutions for installing Ollama. Solution 1: Run the Linux command to download the latest versio
n of Ollama from GitHub and install it. Solution 2: Download Ollama backed up in OBS and install it. The secon
d solution provides a fast download speed and the Ollama version is released on February 28, 2025.

Solution 1: Running the Linux command

Run the following command:

 *curl -fsSL https://ollama.com/install.sh | sh*
 
Note: Ollama is downloaded from GitHub and may fail to be downloaded. If the download fails, run the comman
d again or use solution 2.

Check whether the startup is successful.
 *ollama -v*
 
The installation and startup of Ollama are complete.
Solution 2: Downloading the Ollama installation package
The Ollama version is released on February 28, 2025.
Download the Ollama installation package.

 *wget https://sandbox-experiment-files.obs.cnnorth-4.myhuaweicloud.com/deepseek/ollama-linux-amd64.tgz*

 Decompress the software package.
 
 *sudo tar -C /usr -xzf ollama-linux-amd64.tgz*
 
Add the execute permission.

 *sudo chmod +x /usr/bin/ollama*
 
Check whether the Ollama user exists.

 *id ollama*
 
If the ollama user does not exist, create an Ollama user.
 
 *sudo useradd -r -s /bin/false -m -d
/usr/share/ollama ollama*
 
Create ollama.service

 *cat << EOF > /etc/systemd/system/ollama.service*
 
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
ExecStart=/usr/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3
[Install]

*WantedBy=default.target EOF*
 
Reload the configuration file.

 *sudo systemctl daemon-reload*
 
Add the service to the directory during startup.

 *sudo systemctl enable ollama*
 
Start Ollama.

 *sudo systemctl start ollama*
 
Check whether the startup is successful.
 *ollama -V*

 The installation and startup of Ollama are complete.
 
# 3. Downloading and Running DeepSeek-R1 1.5B

There are two solutions for using Ollama to deploy DeepSeek. Solution 1: Run the Ollama command to pull Dee
pSeek-R1 1.5B. The model version is the same as that of the community version, but this solution takes a long ti
me. Solution 2: Download the model file backed up in OBS. The second solution provides a fast download speed 
and the DeepSeek version is released on February 14, 2025.

Solution 1: Using Ollama
The model version is the same as that of the community version, but this solution takes a long time.
If the pull fails, run the command again.

If the pull speed is slow, press ctrl+c to stop and run the command again. Ollama supports resumable download.

 *ollama pull deepseek-r1:1.5b*
 
Run DeepSeek-R1 1.5B.

 *ollama run deepseek-r1:1.5b*

Solution 2: Downloading from OBS
Download from OBS.
 *wget https://sandbox-experiment-files.obs.cnnorth-4.myhuaweicloud.com/deepseek/ollama_deepseek_r1_1.5b.tar.gz*
 
Decompress.
 *sudo tar -C /usr/share/ollama/.ollama/models-xzf ollama_deepseek_r1_1.5b.tar.gz*
 
Save the model file to the Ollama directory.
 *cd /usr/share/ollama/.ollama/modelsmv ./deepseek/sha256* ./blobs
mkdir -p ./manifests/registry.ollama.ai/library/deepseek-r1
mv ./deepseek/1.5b ./manifests/registry.ollama.ai/library/deepseek-r1
rm -rf deepseek/*
 
View the model list.
 *ollama list*
 
Run DeepSeek-R1 1.5B.
 *ollama run deepseek-r1:1.5b*
 
Now, you can talk with DeepSeek.
----



