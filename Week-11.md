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
