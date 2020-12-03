# [Docker](https://docs.docker.com/get-started/overview/)

![Docker](img/docker.png)

## To install docker in ubuntu

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

Add the oficial docker GPG key

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

## Unistall docker

Uninstall docker engine, cli and containerd packages

```bash
sudo apt purge docker-ce docker-ce-cli containerd.io
```

To delete images, containers and volumes

```bash
sudo rm -rf /var/lib/docker
```
