# Linux Server Docker App Configuration 
- VM, SSH, Docker, DockerHub

> :mega: In the configuration steps replace all occurrences of:
> - `<tag>` with your chosen tag image from DockerHub


## **1. Create VM in Azure or any other cloud provider(Digital Ocean, Linode, AWS...)**
- use Ubuntu Server 20.04 image
- use password for authentication
- once VM is created, connect to it using SSH: 
```
ssh -p 22 <user_name>@<vm_ip_address>
```
- as root run: 
```
apt update && apt full-upgrade -y
```

## **2. Secure SSH with Key Authentication**
- on your local machine(laptop/PC) that you will use to SSH to the VM create key pairs in `/home/docker/` directory:
```
ssh-keygen -t rsa -b 2048 -C 'linux server VM keys'
```
- add created public key to your VM machine `home` directory by copy/pasting it to the VM `.ssh/authorized_keys` file:
```
vim .ssh/authorized_keys
```
- disable password authentication on the server(`PasswordAuthentication no`) and restart the SSH service:
```
vim /etc/ssh/sshd_config

// set PasswordAuthentication to no in the configuration file
PasswordAuthentication no

systemctl restart ssh
```
- now you can SSH to the VM without password(you will not be asked for a password anymore: 
```
ssh -p 22 <user_name>@<vm_ip_address>
```

## **3. Install Docker** 
- SSH to VM:
```
ssh -p 22 <user_name>@<vm_ip_address>
```
- Docker installation instructions here: [UbuntuDockerInstallation](https://docs.docker.com/engine/install/ubuntu/)
- check if docker is running: `systemctl status docker`
- check docker version: `docker --version`
- docker playground: [LearnDocker](https://labs.play-with-docker.com/)

## **4. Pull the image from DockerHub and run a container**
- for this project I am using my own DockerHub image: [MyWebsite](https://hub.docker.com/repository/docker/crepic21/my-website/general)
- `docker image pull crepic21/my-website:<tag>`
- `docker container run -d -p 80:80 crepic21/my-website:<tag>`
- go to VM IP address port 80, you will see the website





































































































