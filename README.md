# Docker SOCKS5 Proxy

This repository will allow you to launch your own socks5 proxy server with minimal cost.

##Quickstart

Below is the instruction for raising SOCKS5 proxy. The only requirement is the presence of a [white] ) IP. If you do not have a personal server, then at the bottom of the page you will find instructions for setting up a free server on AWS. You can also use any other cloud server provider.

1. Install Docker engine.
   
   Select the instruction for your OS. Whole system testing was done for Ubuntu only, but it should work for other operating systems with some modifications to the commands below.
 
   1. [Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce)
   2. [Mac](https://docs.docker.com/docker-for-mac/install/)
   3. [Windows](https://docs.docker.com/docker-for-windows/install/)
   
2. Clone this repository

   ```bash
   git clone https://github.com/elejke/docker-socks5.git
   cd docker-socks5
   ```
   
3. Build the Docker Image

   ```bash
   sudo docker build -t socks5 .
   ```
   
   If you want to use a login and password for your server, then change the corresponding line in [Dockerfile](Dockerfile#L4) to the desired login/password pair.
   
4. Run the Docker image:

   ```bash
   sudo docker run -d -p 80:1080 socks5
   ```
   
   In this case, the proxy server will run on port 80. You can change it to an arbitrary one by changing the appropriate number when starting the Docker container. Please note that the selected port must be open to outside access.
   
   If you want to use a username/password for your proxy, then you must also add a configuration file to the Docker container, which is done by adding an option at startup:
   
   ```bash
   sudo docker run -d -p 80:1080 -v ${PWD}/sockd.conf:/etc/sockd.conf socks5
   ```
   
   In this case, the login / password specified in step 3 will be used.
   
5. Your proxy server is ready!

   Use your IP address, the port specified in step 4, and login/password (if set) in any application!
   
   For Telegram, the corresponding settings are in:
   
   1. **iOS**: Settings - Data and Storage - Use Proxy
   2. **Desktop**: Settings - Privacy and Security - Use Proxy
   
## Free server on Amazon [AWS](https://aws.amazon.com)

1. Registration of an AWS account with the possibility of raising free servers within 12 months:
   
   1. Create an account at https://aws.amazon.com/free/ by selecting the account type **Personal**. When using free servers, money from the linked card will not be spent, except for $1, which will be withdrawn upon registration.
   2. Login to the created account using: https://console.aws.amazon.com
   3. It may take up to 24 hours for the registration to complete and the eligibility to be confirmed. You can check whether it has ended or not in the console: go to the **Services** tab and press **EC2**

2. To launch a free server on **AWS EC2**, go to the **Services > EC2** tab and click **Launch Instance**, on the left side, click the checkbox next to **Free tier only ** and select from the list image **Ubuntu Server 16.04 LTS (HVM), SSD Volume Type - ami-43a15f3e**
    
   1.Select **t2.micro**
   2. At the top of the screen, click **Configure Security Group**, click **Add Rule** and select **HTTP** from the dropdown list (your proxy server will already be configured to use 80)
   3. Click **Review and Launch > Launch**
      
      1. In the window that appears, click Create a new key pair, name it socks5 and click Download Key Pair and Launch Instance.
      2. Congratulations! You have started the server.

3. Go to the **Instances** tab on the left side of the **EC2** console and select a running server, press the **Connect** button and follow the instructions (change the key permissions and connect from the console via **ssh**)
