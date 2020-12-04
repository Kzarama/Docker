# [Docker](https://docs.docker.com/get-started/overview/)

![Docker](img/docker.png)

## Content

- **[Installation](#installation)**
  - **[Install docker in ubuntu](#install-docker-in-ubuntu)**
  - **[Uninstall old versions](#uninstall-old-versions)**
  - **[Uninstall docker](#uninstall-docker)**
- **[Commands of docker](#commands-of-docker)**
- **[Fix problem in docker](#fix-problem-in-docker)**

## Installation

### Install docker in ubuntu

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

### Uninstall old versions

```bash
sudo apt remove docker docker-engine docker.io containerd runc
```

### Uninstall docker

Uninstall docker engine, cli and containerd packages

```bash
sudo apt purge docker-ce docker-ce-cli containerd.io
```

To delete images, containers and volumes

```bash
sudo rm -rf /var/lib/docker
```

## Commands of docker

(with CONTAINER_ID or NAMES)

### Run

Run a container

```bash
docker run [OPTIONS] CONTAINER_IMAGE [COMMAND]
```

Options:  
-n, --name string = to name the container  
-it = iterative mode  
-d, --detach = to run the container in background with `tail -f /dev/null`  
-p, -publish list = to expose in the ports of the pc, the ports of the container, in list int:int `(PC_PORT:CONTAINER_PORT)`

### Exec

Execute a command or process in a up container

```bash
docker exec -it NAMES COMMAND
```

### Ps

See the containers that are running

```bash
docker ps
```

See the all containers

```bash
docker ps -a
```

### Rm

Delete containers

```bash
docker rm NAMES
```

### Container

Delete all containers exited

```bash
docker container prune
```

### Logs

To see the logs of the containers

```bash
docker logs [OPTIONS] NAMES
```

Options:  
-f = follow the logs

### Inspect

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

## Fix problem in docker

Fix error failed to register layer

```bash
service docker stop
```

```bash
service docker start
```
