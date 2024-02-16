# Install Docker Engine on Ubuntu
: Updated at 23.10.16

1. Update apt package manager
```bash
sudo apt-get update
```
2. Install prerequisite package for docker
```bash
sudo apt-get install ca-certificates curl gnupg
```
3. Add Docker's GPG key
``` bash
sudo install -m 0755 -d /etc/apt/keyrings
```
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
4. Set up the repository of stable version
```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
5. **Install Docker engine**
``` bash
sudo apt-get update
```
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
6. Verify that the Docker Engine installation is successful by running the hello-world image
```bash
sudo docker run hello-world
```

# Set up the manage docker as a non-root user
현재는 모든 docker 작업 권한이 root 유저에게만 있으므로 `sudo`를 붙여주어야 한다.  
따라서, root 유저가 아닌 host의 기본 유저에게도 권한을 주기 위해 추가적인 설정이 필요하다.  <div>
1. Add your user to the docker group.
```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```
2. (VM Restart)
``` bash
sudo service docker restart
newgrp docker
```
3. Verify that you can run docker commands without `sudo`
```bash
docker run hello-world
```

---

!!! quote
    - Docker document   
    [Docker-install-ubuntu-Link](https://docs.docker.com/engine/install/ubuntu/)    
        - Method   
        I'm choose <**Install using the repository**>  
    - Docker document  
    [Docker-post-installation-steps](https://docs.docker.com/engine/install/linux-postinstall/)