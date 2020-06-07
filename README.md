# Docker
To install docker in ubuntu
~~~bash
sudo apt update
~~~
~~~bash
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
~~~
~~~bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
~~~
~~~bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
~~~
~~~bash
sudo apt-get update
~~~
~~~bash
sudo apt-get install docker-ce docker-ce-cli containerd.io
~~~
To verify docker installed
~~~bash
sudo docker --verision
~~~
To authorize docker, and use docker without sudo
~~~bash
sudo usermod -aG docker USER
~~~
