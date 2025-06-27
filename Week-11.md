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


