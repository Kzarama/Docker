# [Docker](https://docs.docker.com/get-started/overview/)

![Docker](img/docker.png)

## Content

- **[Installation](#installation)**
  - **[Install docker in ubuntu](#install-docker-in-ubuntu)**
  - **[Uninstall old versions](#uninstall-old-versions)**
  - **[Uninstall docker](#uninstall-docker)**
- **[Containers](#containers)**
  - **[Commands](#commands-of-containers)**
- **[Image](#image)**
  - **[Commands](#commands-of-images)**
  - **[Dockerfile commands](#dockerfile-commands)**
- **[File data](#file-data)**
  - **[Bind mounts](#bind-mounts)**
  - **[tmpfs mount](#tmpfs-mount)**
  - **[Volume](#volume)**
  - **[Copy file in the container](#copy-file-in-the-container)**
- **[Network](#network)**
  - **[Install docker-compose](#install-docker-compose)**
  - **[Commands](#commands-of-docker-compose)**
  - **[Bind mounts](#bind-mounts)**
- **[Docker un docker](#docker-in-docker)**
- **[Fix problem in docker](#fix-problem-in-docker)**

# Installation

## Install docker in ubuntu

To update the packages

```bash
sudo apt update
```

To install packages to allow apt to use a repository over htts

```bash
sudo apt install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

Add the official docker GPG key

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Set up the stable repository

```bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

Update the packages

```bash
sudo apt update
```

Install the latest docker version of docker engine and containerd

```bash
sudo apt install docker-ce docker-ce-cli containerd.io
```

To verify docker installed

```bash
sudo docker run hello-world
```

To authorize docker, and use docker without sudo

```bash
sudo usermod -aG docker USER
```

## Uninstall old versions

```bash
sudo apt remove docker docker-engine docker.io containerd runc
```

## Uninstall docker

Uninstall docker engine, cli and containerd packages

```bash
sudo apt purge docker-ce docker-ce-cli containerd.io
```

To delete images, containers and volumes

```bash
sudo rm -rf /var/lib/docker
```

# Containers

## Commands of containers

(with CONTAINER_ID or NAMES)

Run a container

```bash
docker run [OPTIONS] CONTAINER_IMAGE [COMMAND]
```

Options:

- -n, --name string = to name the container
- -rm = delete a container then of the stop of this
- -it = iterative mode
- -d, --detach = to run the container in background with `tail -f /dev/null`
- -p, -publish list = to expose in the ports of the pc, the ports of the container, in list int:int `(PC_PORT:CONTAINER_PORT)`
- --memory memory_size = limit of the memory for the container

Stats of docker

```bash
docker stats
```

Process of the container

```bash
docker exec NAMES ps -ef
```

Execute a command or process in a up container

```bash
docker exec -it NAMES COMMAND
```

See the containers that are running

```bash
docker ps OPTIONS
```

Options:

- -a = list the all containers
- -l = latest container

Stops the container (send a SIGTERM)

```bash
docker stop NAMES
```

Kill the container (send a SIGKILL)

```bash
docker kill NAMES
```

Delete containers

```bash
docker rm NAMES
```

Delete all containers exited

```bash
docker container prune
```

Delete all containers

```bash
docker rm -f $(docker ps -aq)
```

Delete containers, networks, images and cache

```bash
docker system prune
```

To see the logs of the containers

```bash
docker logs [OPTIONS] NAMES
```

Options:  
-f = follow the logs

All data of the container

```bash
docker inspect NAMES
```

Filter the process id of the container

```bash
docker inspect --format '{{.State.Pid}}' NAMES
```

Kill the process of the container in linux

```bash
kill -9 PROCESS_ID
```

# Image

## Commands of images

List images

```bash
docker image ls
```

Bring new image

```bash
docker pull IMAGE:VERSION
```

Create new images (example ubuntu)

- Create Dockerfile file
  ```Dockerfile
  from ubuntu:latest
  run touch /usr/src/hello-world.txt
  ```
- Create the container in the bash
  ```bash
  docker build -t ubuntu:hello_world .
  ```

Rename images

```bash
docker tag NAME:TAG DOCKER_USERNAME/NEW_NAME:NEW_TAG
```

History of the dockerfile

```bash
docker history NAME:TAG
```

Before the push, make a login

```bash
docker login
```

```bash
Docker commit [OPTIONS] CONTAINER [REPOSITORY:TAG]
```

Make the push

```bash
docker push DOCKER_USERNAME/NAME:TAG
```

## Dockerfile commands

- from = container base
- copy = copy files
- workdir = path of the work directory
- run = run command
- expose = expose a port in the pc
- entrypoint = use with cmd, with cmd like parameter of this and this run a command
- cmd = default command, that run when the container is exposed (use [])

# File data

## Bind mounts

Is used for persist the data os the container, for this in the run command add -v FOLDER_PATH:DATA_PATH

### Example with mongodb

Run the container with mongodb

```bash
docker run -d --name db -v /home/kz/git/Docker/mongodb:/data/db mongo
```

Exec the bash in the container

```bash
docker exec -it db bash
```

## tmpfs mount

Temporal mount, only data save with the container

## Volume

List the volume

```bash
docker volume ls
```

Create a volume

```bash
docker volume create VOLUME_NAME
```

Delete a volume

```bash
docker volume rm VOLUME_NAME
```

Delete all networks not exited

```bash
docker volume prune
```

Run a container using a volume (src= source volume, dst= folder destination in the container)

```bash
docker run -d --name db --mount src=VOLUME_NAME, dst=/data/db mongo
```

## Copy files

To copy files to the container

```bash
docker cp FILE NAMES:PATH
```

To copy files to the pc

```bash
docker cp NAMES:PATH FILE
```

# Network

Communication between containers

List all networks

```bash
docker network ls
```

Create a network

```bash
docker network create --attachable NETWORK
```

Delete a network

```bash
docker network rm NETWORK
```

Delete all networks not exited

```bash
docker network prune
```

Connect container at the network

```bash
docker network connect NETWORK NAMES
```

# Docker compose

## Install docker-compose

Download the docker-compose release

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

Apply permissions at the download

```bash
sudo chmod +x /usr/local/bin/docker-compose
```

## Commands of docker compose

Way to easy the run of the components, allows write the declaration of the services that the containers need

- version = #versions of docker compose
- services = services that compose the application, the services can have more than one container
- SERVICE_NAME:
- build = path of the files
- image = name of the image
- environment = environment variables
- depends_on = the service have dependency of the other service
- port = port of the application

Run the docker-compose

```bash
docker-compose up [OPTIONS]
```

Options

- -d = detach
- --scale app=n = make n instances of the services (for ports make a rank "3000-3001:3000")

List the containers

```bash
docker-compose ps
```

See the logs of the services

```bash
docker compose logs [SERVICE_NAME]
```

Run a command in the service

```bash
docker-compose exec SERVICE_NAME COMMAND
```

Shutdown the docker-compose

```bash
docker-compose down
```

For the register the changes is necessary build again the app and run the command of up the docker-compose

## Bind mounts

In the service of the docker-compose file add volumes: and for copy the files use PC_PATH:PATH, for ignore only put the route

# Docker un docker

Run docker in a docker container

```bash
docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock docker
```

## Fix problem in docker

Fix error failed to register layer

```bash
service docker stop
```

```bash
service docker start
```
