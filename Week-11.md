Docker is a platform that uses containerization to package, deploy, and run applications. It allows developers to bundle an application with all its dependencies (libraries, system tools, etc.) into a standardized unit called a container, ensuring consistent performance across different environments.

Install Docker in OUr machine

sudo apt-get update
sudo apt-get upgrade -y
sudo apt-get remove docker docker-engine docker.io containerd runc

sudo apt-get install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
    sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io

sudo systemctl start docker
sudo systemctl enable docker

sudo docker run hello-world

Now run Nginx
docker run nginx

To list containers
docker ps

to list all running container
docker ps -a

docker run -d -p 8000:80 nginx

Runs NGINX web server

Exposes it on port 8000

Access it at: http://localhost:8000

It automatically works like a mini web server

Then, stop the container by running:
docker stop silly_sammet

After stopping, running docker ps will show no active containers. To permanently remove a stopped container, use:

docker rm silly_sammet

Managing Docker Images
Viewing local Docker images is straightforward with the docker images command. This command displays each image along with its size, creation time, and more
docker images
REPOSITORY          TAG       IMAGE ID       CREATED        SIZE
nginx               latest    f68d6e55e065   4 days ago     109MB
redis               latest    4760dc956b2d   15 months ago  107MB
ubuntu              latest    f975c503748    16 months ago  112MB
alpine              latest    3fd9065eaf02   18 months ago  4.14MB

To delete an image no longer needed, ensure no container is using it and execute:

docker rmi nginx

You cannot delete an image (nginx) while there is a container using that image — even if the container is stopped.

OR remove all stopped containers

docker container prune

Now safely remove the image
docker rmi nginx

Additionally, if you want to download an image for later use without running a container immediately, use the 

docker pull command:

For Ubuntu container:

Now docker installed ubuntu container
docker run ubuntu

docker create the new container 
docker run -dit --name my-ubuntu ubuntu

(it run ubuntu in background)

docker exec -it my-ubuntu bash
Ubuntu shell open
run any commands
and Exit


🔹 docker start -ai my-ubuntu
✅ What it does:
start → Starts a stopped container

-a → Attach to its output

-i → Keep input open (interactive)

📺 Re-enters a previously exited container, like it's resumed from pause.


 docker stop my-ubuntu
✅ Gracefully stops a running container

🔹 docker rm my-ubuntu
✅ Removes (deletes) the container
⚠️ Must be stopped first

🔹 docker rmi ubuntu
✅ Removes the image named ubuntu
⚠️ Only if no containers are using it

docker exec my-ubuntu ls /
✅ Runs the command ls / inside my-ubuntu and shows output
(No interactive terminal)

exit
✅ Exits the container terminal and returns to your host shell

If you only want to pull the image without running use
docker pull imagename


To execute commands on a running container, use docker exec. For example, viewing the OS release information inside the Ubuntu container:


root@Docker:/root # docker exec c1a9d3a7ca7 cat /etc/*release*
NAME="Ubuntu"
VERSION="16.04.3 LTS (Xenial Xerus)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 16.04.3 LTS"
VERSION_ID="16.04"
HOME_URL="http://www.ubuntu.com/"
SUPPORT_URL="http://help.ubuntu.com/"
BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
VERSION_CODENAME=xenial
UBUNTU_CODENAME=xenial


To run the web application in detached (background) mode, add the -d option:

docker run -d kodekloud/simple-webapp

This will output a container ID similar to:

a043d40f85fefa414254e4775f9336ea59e5cf597af5c554e0a35a1631118

If you need to reattach to the container, use the docker attach command along with the container ID (a shortened unique prefix is acceptable):

docker attach a043d


What is port mapping:
Docker host:Docker host is just the computer or system where Docker is installed and running.

If Docker is installed on your Ubuntu VM, then your Ubuntu VM is the Docker host.

The host is where containers live and run.

🧱 Think of Docker Like a Building
🏠 Docker host = the building (your VM or laptop)

📦 Docker container = the rooms inside the building (Ubuntu, NGINX, etc.)

🧑‍💻 You = the person entering and exiting the rooms (via docker exec, etc.)

docker run -it ubuntu
✅ This creates a container (room) inside the Docker host (your Ubuntu).


docker run -d -p 8000:80 nginx

Now the NGINX container is running inside the Docker host.

Port 8000 is exposed from the container to the Docker host.
Local host:8000
Docker host:80

So, from your VM (Docker host), you can visit:
👉 http://localhost:8000


Volume mapping:
docker run mysql
docker stop mysql
(all data is deleted) to overcome this we come with command to store the file in the outside container
docker run -v /opt/datadir: /varlib/mysql mysql

To get all the information of the container
docker inspect "container name"

How to get the logs of container
docker logs name

To check the version of ubuntu
docker run ubuntu cat /etc/*release*

Docker file:

A Dockerfile is a text file that contains instructions to build a Docker image.

Example:

 For a basic web application, these steps might include:

Starting with an operating system (e.g., Ubuntu)
Updating package repositories via APT
Installing required dependencies using APT
Installing Python packages with pip
Copying your application's source code to a target directory (for example, /opt)
Launching the Flask web server

FROM ubuntu
RUN apt-get update && apt-get install -y python3 python3-pip
RUN pip install flask flask-mysql
COPY .opt/source-code

 steps to create simple php application run in apache server:

 create folder named: PHP-DOCKER-APP
 create two file under folder:

 Dockerfile
 index.php

 index.php
 
<?php
echo "Hello from Dockerized PHP on VM!";
?>


Dockerfile

FROM php:8.2-apache
COPY . /var/www/html/
EXPOSE 80

Opem ubuntu 
1. git clone "url"
2. docker build -t php-app .
3. docker run -d -p 8000:80 php-app
4. open internal google 
http://localhost:8000

Environment variable = a value (like password or port) stored outside the code, but used inside the app.

export APP_COLOR=blue; python app.py

docker run -e APP_COLOR=blue simple-webapp-color

When your application consists of multiple services, managing each container separately can become cumbersome. Docker Compose streamlines this process by allowing you to define all required services in a single YAML file (commonly named docker-compose.yml). You can then launch the complete stack with the docker-compose up command.

Example: Basic Docker Compose Configuration

Below is an example Docker Compose file that defines multiple services:


# docker-compose.yml
services:
  web:
    image: "mmunshad/simple-webapp"
  database:
    image: "mongodb"
  messaging:
    image: "redis:alpine"
  orchestration:
    image: "ansible"

Start your multi-container application with:

docker-compose.yaml
docker-compose up

Docker engine:
Core Components of Docker on Linux
Docker Daemon:
A background process that manages Docker objects such as images, containers, volumes, and networks.

Docker REST API Server:
An interface enabling programs to communicate with the daemon. This API facilitates the development of custom tools and integrations.

Docker CLI:
A command-line interface used to execute operations such as starting or stopping containers and managing images. The CLI communicates with the Docker daemon via the REST API.

For example, to run an Nginx container on a remote Docker host, use the command below:

docker -H=10.123.2.1:2375 run nginx

Docker engine:
Docker Engine is the core software that lets you build, run, and manage containers on your system.

Core Components of Docker on Linux
Docker deamon
Docker Rest API
Docker CLI

Managing Resources with cgroups
docker run --cpus=0.5 ubuntu
docker run --memory=100m ubuntu

Docker's File Storage Architecture

When Docker is installed, it establishes a directory structure typically at /var/lib/docker. This root directory contains several subdirectories that serve different purposes:

Docker optimizes builds by reusing layers that remain unchanged between images. Consider a scenario with two nearly identical applications:


Since the first three layers are identical in both Dockerfiles, Docker reuses the cached layers, significantly speeding up the build process and saving disk space. Even when updating application code, only the modified layers are rebuilt.


DOCKER STORAGE:

When Docker is installed, it establishes a directory structure typically at /var/lib/docker

Visualize the image layers from the base to the top:

Base Ubuntu layer.
APT package installation.
Python and Flask dependencies.
Application source code.
Entrypoint setup.

1.Once built, these layers are read-only on image.
2.When you run a container from the image, Docker adds a new, writable layer on top
3.captures any changes made during runtime—be it log files or temporary modifications
4.Docker uses a copy-on-write mechanism: it copies the original file to the writable layer and then applies any changes
5.When the container stops or is removed, this writable layer is also discarded.

To ensure data persists beyond the lifecycle of a container, Docker offers volumes

1.Creating and Using Volumes
docker volume create data_volume

2.Run a Container with a Volume:
docker run -v data_volume:/var/lib/mysql mysql

3.If you specify a volume that does not yet exist, such as data_volume2, Docker will automatically create it and mount it:
docker run -v data_volume2:/var/lib/mysql mysql


Alternatively, you can use bind mounts to link a specific host directory to the container, for instance:

docker run -v /data/mysql:/var/lib/mysql mysql

the newer and preferred method is using the --mount

docker run \
--mount type=bind,source=/data/mysql,target=/var/lib/mysql \
mysql


Docker storage drivers manage the layered filesystem, create writable layers, and implement the copy-on-write mechanism
is STORAGE DRIVERS:
for ubuntu: AUFS

DOCKER NETWORK:

1.By default, Docker creates three networks upon installation: bridge, none, and host.
2.When you launch a container without specifying a network, it connects to the bridge network by default
docker run ubuntu

3.You can also choose a different network using the --network parameter. For instance:
docker run ubuntu --network none
docker run ubuntu --network host



ECS:Elastice container service

Amazon ECS (Elastic Container Service) is a service by AWS that helps you run and manage Docker containers on the cloud — without managing servers manually.

📦 What is a Container?
A container is like a lightweight package of your app (code, libraries, dependencies) that runs the same everywhere.

ECS lets you run these containers in the cloud, automatically.

| Feature               | Benefit                       |
| --------------------- | ----------------------------- |
| Task Definitions      | Say what to run and how       |
| Services              | Keep apps running             |
| Auto Scaling          | Handle traffic automatically  |
| Load Balancer Support | Expose app to the internet    |
| IAM Integration       | Secure access to AWS services |
| Logs & Metrics        | Monitor containers easily     |






