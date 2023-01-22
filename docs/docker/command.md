## Basic Commands
|    Command    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
| `docker pull`     |docker image repository 또는 registry에서 Docker image를 가져오는 명령어 |
| `docker build`    |`Dockerfile`로부터 도커 이미지 빌드                                      |
| `docker images`   |local에 존재하는 docker image 리스트 출력                                |    
| `docker run`      |도커 컨테이너 실행                                                       | `-it`: interatctive-terminal 접속 <div> `--name`: 컨테이너 이름 설정 <div> `/bin/bash`: bash 터미널 사용 <div> `-d`: 백그라운드 실행
| `docker exec`     |도커  컨테이너 내부 접속                                                 | `-it`, `/bin/bash`
| `docker ps`       |현재 실행중인 도커 컨테이너 리스트 출력                                    | `-a` : 모든 컨테이너 출력
| `docker logs`     |도커 컨테이너의 log 확인                                                 | `-f`: 실시간 watch 
| `docker stop`     |실행 중인 도커 컨테이너 중단                                              |
| `docker rm`       |도커 컨테이너 삭제                                                       |
| `docker rmi`      |도커 이미지 삭제                                                         |  

Example
```
- docker pull image_name
- docker ps 
- docker ps -a  
- docker run -it --name container_name image_name /bin/bash  
- docker exec -it container_name /bin/bash
- docker logs container_name -f    
- docker stop container_name
- docker rm container_name
- docker rmi image_name
```

## Others
|    Command    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
| `docker cp`         |Copy files/folders between a container and the local filesystem |
| `docker manifest`   |Manage Docker image manifests and manifest lists |
| `docker diff`       |Inspect changes to files or directories on a container’s filesystem |
| `docker inspect`    |:material-arrow-down-circle: Return low-level information on Docker objects |
| `docker stats`      |:material-arrow-up-circle: Display a live stream of container(s) resource usage statistics |
|                     |                                                                                           |  
| `docker volume`     |Manage volumes |                                                                                       
| `docker container`  |Manage containers |
| `docker builder`    |Manage builds |
| `docker checkpoint` |Manage checkpoints |
| `docker config`     |Manage Docker configs |
| `docker context`    |Manage contexts |
| `docker image`      |Manage images |
| `docker network`    |Manage networks |
| `docker plugin`     |Manage plugins |
| `docker system`     |Manage Docker |
| `docker secret`     |Manage Docker secrets |
| `docker service`    |Manage services |
| `docker stack`      |Manage Docker stacks |
| `docker trust`      |Manage trust on Docker images |
| `docker swarm`      |Manage Swarm |
| `docker node`       |Manage Swarm nodes |
|                     |                                                                                           |      
| `docker login`      |Login to a Docker registry |
| `docker logout`     |Logout from a Docker registry |
| `docker push`       |Push an image or a repository to a registry |
| `docker search`     |Search the Docker Hub for images |
|                     |                                                                                           |
| `docker create`     |Create a new container |
| `docker events`     |Get real time events from the server |
| `docker export`     |Export a container’s filesystem as a tar archive |
| `docker history`    |Show the history of an image |
| `docker import`     |Import the contents from a tarball to create a filesystem image |
| `docker info`       |Display system-wide information |
| `docker kill`       |Kill one or more running containers |
| `docker load`       |Load an image from a tar archive or STDIN |
| `docker port`       |List port mappings or a specific mapping for the container |
| `docker rename`     |Rename a container |
| `docker restart`    |Restart one or more containers |
| `docker save`       |Save one or more images to a tar archive (streamed to STDOUT by default) |
| `docker stop`       |:material-arrow-down-circle: Stop one or more running containers (프로세스 kill) |
| `docker start`      |:material-arrow-down-circle: Start one or more stopped containers |
| `docker pause`      |:material-arrow-up-circle: Pause all processes within one or more containers (프로세스 pause) |
| `docker unpause`    |:material-arrow-up-circle: Unpause all processes within one or more containers |
| `docker tag`        |Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE |
| `docker top`        |Display the running processes of a container |
| `docker update`     |Update configuration of one or more containers |
| `docker version`    |Show the Docker version information |
| `docker wait`       |Block until one or more containers stop, then print their exit codes |
| `docker commit`     |Create a new image from a container’s changes |


!!!note
    [Docker-docs-BaseCommand](https://docs.docker.com/engine/reference/commandline/docker/)
