## 1. Downloading balenaEtcher
https://www.balena.io/etcher

## 2. Downloading and deploying Armbian on OrangePi 3 LTS
https://www.armbian.com/

## 3. Find the ip-address of the single board connected to the router via ethernet
```
sudo apt-get install nmap
```
```
ifconfig
```
```
sudo nmap -sn 192.168.1.0/24
```
*change 192.168.1.0 to your ip*

## 4. Connecting to the single board via SSH
```
ssh root@192.168.100.88
```
*change 192.168.100.88 to your single-board ip*

Armbian default password:
1234

## 5. Installing and optimizing docker and docker-compose
```
sudo apt-get update
```
Install the necessary packages required for downloading and installing software packages over HTTPS, verifying the authenticity of the packages using the public key infrastructure, and performing secure file transfer
```
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
```
Official Docker repository key for GPG:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
Add Docker's official GPG keyring to the system's list of trusted keys and adds a new entry to the system's software sources list:
```
echo "deb [arch=arm64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Update the repositories and install the Docker Engine:
```
sudo apt-get update
sudo apt-get install -y docker.io
```
Check the installed version of Docker:
```
docker -v 
```
Executing the hello-world image:
```
sudo docker run hello-world
```
Install docker-compose:
```
sudo apt-get install -y docker-compose
```
Check the installed version:
```
docker-compose version
```
Create the daemon.json file:
```
sudo nano /etc/docker/daemon.json
```
Now fill it with the necessary parameters
```
{
   "log-driver": "local",
   "log-opts": {
       "max-size": "10m",
       "max-file":"3"
   },
   "userland-proxy": false
}
```
*Parameter Description:*
*"log-driver": "local" - parameters for local log files*
*"max-size": "10m" - maximum size of one log file is 10 Mb*
*"max-file": "3″ - the maximum number of log files is 3*

Restart the Docker service:
```
sudo systemctl restart docker
```

6. Downloading and configuring the bot
Install the bot on our single board
```
git clone https://github.com/karfly/chatgpt_telegram_bot
```
Input the folder containing our bots
```
cd chatgpt_telegram_bot
```
Go to the configuration file
```
nano config/config.yml
```
Rename the configuration files:
```
mv config/config.example.yml config/config.yml
mv config/config.example.env config/config.env
```
Make the bot compatible with ARM8v-a processors:
Open the docker-compose.yml file:
```
nano docker-compose.yml
```
Change the version of MongoDB:
```
image: mongo:4.4.12
```
Add the following commands to limit the cache size and memory usage to 1 GigaBYTE:
```
command: mongod --bind_ip_all --wiredTigerCacheSizeGB 1
mem_limit: 1g
```
7. Raising containers with the bot

Start containers:
```
docker-compose --env-file config/config.env up --build
```

ChatGPT Telegram Bot by Karim Iskakov ( @karfly )
https://github.com/karfly/chatgpt_telegram_bot
