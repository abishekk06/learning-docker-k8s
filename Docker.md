# Docker:

[Docker](https://docs.docker.com/reference/) is a tool for running applications in an isolated environment.

Similar to virtual machine

App run in same environment

Standard for software deployment

## Containers vs Virtual Machine:

**Containers** are an abstraction at the app layer that packages code and dependencies together. Multiple containers can run on same machine and share the OS kernel with other containers, each running as islated process in user space.

**Virtual Machine** are an abstraction of physical hardware turning one server into many servers. The hypervisor allows many VMs to run on a single machine. Each VMincludes full copy of an OS, the application, necessary binaries and libraries - taking up tens of GBs. VMs can be slow to boot.

## Docker Images:

Image is a template for creating an environment of your choice.

Has everything need to run your apps. i.e, OS, Software, App code.

## Container:

Container is a running instance of an image.

To run a container,

'''
docker pull nginx  # pull an nginx image from docker hub

docker images  # list all images

docker run nginx:latest  # run a container from the image nginx

docker run -d nginx:latest  # run container in detach mode

docker container ls  # list all running containers

docker ps  # list all running containers
'''

### Exposing Ports:

Now a running nginx container with 80/tcp port exposed. This can be done while running a container.

    docker run -d -p 8080:80 nginx:latest  # Container can be accessed from local host

### Exposing multiple ports:

    docker run -d -p 3000:80 -p 8080:80 nginx:latest

### Managing Containers:

'''
docker stop <container-id> or <container-name>  # stop running container

docker start <container-id> or <container-name>  # start the stopped container

docker rm <container-id> or <container-name>  # remove the container

docker rm $(docker pd -aq)  # can remove all the stopped containers at once. -a shows stopped containers, --quite show Container IDs

docker run -d -p 3000:80 -p 8080:80 --name Marvel nginx:latest  # --name runs the container with name

export FORMAT = "ID\t{{.ID}}\nNAME\t{{.Names}}\nImage\t{{.Image}}\nPORTS\t{{.Ports}}\nCOMMAND\t{{.Command}}\nCREATED\t{{.CreatedAt}}\nSTATUS\t{{.Status}}\n"

docker ps --format=$FORMAT

docker rm -f <container-name>  # removes the container forcefully.

docker exec -it website  bash  # connect to the container via bash
'''

## Volumes:

Allows sharing of data. Files and Folders
Between host and container
Between containers

### Volumes(Host and Container):

    docker run --name webserver_nginx -v $(pwd):/usr/share/nginx/html -d -p 8080:80 nginx:latest

### Volumes between Containers:

A container(website) is already running.

    docker run --name website-copy -d -p 8081:80 --volume-from: website nginx:latest # copies the contents of the container - website

## DockerFile:

Build own Images, [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)

    docker build --tag <image-name>:<tag>  # To build docker image from the Dockerfile in the root directory of app.

    docker image ls  # List all images

### DockerFile for NodeApps:

Reference: [Node Js](https://nodejs.org/en/download/current) and [Express Js](https://expressjs.com/en/starter/installing.html)

Simple API for Hello World [here](https://expressjs.com/en/starter/hello-world.html)

