# Rasa Deployment
Deploying Rasa Open Source Bot over Cloud using Docker.

## Prerequisites:
- Docker
- Docker Compose


## Instructions:

### For deploying over Server:
- Create the VM instance of Ubuntu over Compute Engine
- once the instance is created login to the VM using SSH
- Run the below commands and clone our Docker app:

 - > sudo apt-get update
 
#### 1) Install Docker

- > curl -fsSL https://get.docker.com -o get-docker.sh
- > sudo sh get-docker.sh
     
#### 2) Install [Docker-Compose](https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-16-04)

- > sudo curl -L "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

- > sudo chmod +x /usr/local/bin/docker-compose
- > docker-compose --version

#### 3) Clone the Docker App

- > git clone https://github.com/athenasaurav/moodbot25.git
- > cd moodbot25

#### 4) Installing NGINX

- > sudo apt-get update

- > sudo apt-get install software-properties-common

- > sudo add-apt-repository universe

- > sudo add-apt-repository ppa:certbot/certbot

- > sudo apt-get update

- > sudo apt-get install certbot

To get a certificate (you will need a domain name and email ready in this step):

- > sudo certbot certonly --standalone 

Enter Email and choose correct options to install certbot

#### 5) Moving freshly created certificates to Docker Application Directory

- > mkdir certs 

- > sudo cp /etc/letsencrypt/live/yourdomainname/fullchain.pem ./certs
- > sudo cp /etc/letsencrypt/live/yourdomainname/privkey.pem ./certs

** Remember to change the yourdomainname to appropriate domain name name without http or https or www

#### 6) Build the Docker app and run the services:

- > docker-compose build

It will download the necessary docker images and will build the containers for
us. Once the containers are ready , we can run the following command to
make the containers up in running state:

- > sudo docker-compose up -d

- Check whether the services are up and running using below command:

- > docker ps -a

- Once you see all the services up and running, open the ip address of the machine in the browser and test the bot


#### 7) To update the existing images after re-cloning

Reclone the github with changes

shutdown docker with 

- >docker-compose down

Re build the docker image with 

- >docker-compose build

then just do 

- >docker-compose restart
