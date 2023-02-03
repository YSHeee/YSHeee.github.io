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
| `docker tag`      |기존의 도커 이미지명에 새로운 태그명 생성                                  |
| `docker version`  |도커 버전 정보 출력                                                      |`--format`

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
- docker tag source_image:version new_tag:new_version
```

## Others
|    Command    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
| `docker cp`         |컨테이너와 로컬 파일시스템 간 파일/폴더 복사 | `--archive`, `--follow-link`
| `docker diff`       |컨테이너 파일 시스템의 파일/디렉터리 변경 사항 출력 | `A`: add, `D`: delete `C`: change
| `docker inspect`    |도커가 관리하는 개체에 대한 자세한 정보 출력 |`--format`, `--size`, `--type` 
| `docker stats`      |Display a live stream of container resource usage statistics <div>(컨테이너 리소스 통계) | `-a`, `--format`, `--no-stream`, `--no-trunc`
| `docker container prune`      |Exited 상태의 컨테이너 삭제                                                       |  
| `docker image prune -f --all` |Exited 상태의 컨테이너, 이와 관련된 이미지 삭제 |  
| `docker system prune -f --all`|Exited 상태의 컨테이너, 이와 관련된 이미지, 볼륨, 캐시까지 모두 삭제                 |  
|      |        |      
| `docker login`      |Login to a Docker registry | `--username`, `p`, `--password-stdin`
| `docker logout`     |Logout from a Docker registry |
| `docker push`       |Push an image or a repository to a registry | `-a`, `-q`, `--disable-content-trust`
| `docker search`     |Search the Docker Hub for images |`--filter`, `--format`, `--limit`, `--no-trunc`
|      |        |
| `docker create`     |Create a new container | [docs](https://docs.docker.com/engine/reference/commandline/create/)
| `docker events`     |도커 서버에서 일어난 이벤트를 실시간으로 출력 | `--filter`, `--format`, `--since`, `--until`
| `docker export`     |컨테이너의 파일시스템을 tar archive로 저장 | `--output`
| `docker import`     |저장한 컨테이너 tar 파일을 다시 도커 이미지로 불러오기 |`--change`, `--platform`, `-m`
| `docker history`    |이미지의 히스토리 출력 |`--format`, `--human`, `--no-trunc`, `-q`
| `docker info`       |도커 시스템 전체 정보 (컨테이너/이미지 수, 커널 버전, ...) |`--format`
| `docker kill`       |하나 이상의 실행중인 컨테이너를 **즉시 Kill**|`--signal` |
| `docker stop`       |하나 이상의 실행중인 컨테이너를 **Gracefully Stop** (프로세스 kill) | `--time`
| `docker start`      |하나 이상의 중지된 컨테이너 시작 |`-a`,`--checkpoint`,`-i`,`--detach-keys`
| `docker pause`      |하나 이상의 컨테이너 내 모든 프로세스 중지 (프로세스 pause) |
| `docker unpause`    |하나 이상의 컨테이너 내 모든 프로세스 중지 해제 |
| `docker save`       |태그 정보 등을 포함한 도커 이미지를 tar archive로 저장 | `--output`
| `docker load`       |저장한 이미지 tar 파일을(or STDIN) 도커 이미지로 로드 | `--input`
| `docker port`       |컨테이너 Port mapping 또는 컨테이너 Port Mapping List 출력 |
| `docker rename`     |Rename a container |
| `docker restart`    |하나 이상의 컨테이너 재시작 |`--time`
| `docker top`        |컨테이너의 실행중인 프로세스 출력 |
| `docker update`     |하나 이상의 컨테이너 구성 업데이트 | [docs](https://docs.docker.com/engine/reference/commandline/update/)
| `docker wait`       |Container Stop까지 기다린 다음, Exit code 출력 |
| `docker commit`     |컨테이너의 변경사항으로부터 새로운 이미지 생성 |`-a`, `-c`, `-m`, `-p`

Example
``` bash
# 호스트 -> 컨테이너
- docker cp [host_file_path] [container_name]:[container_내부_경로]
# 컨테이너 -> 호스트
- docker cp [container_name]:[container_내부_경로] [host_file_path]
# docker export
- docker export container_name > sample-container.tar
# docker import
- docker import file_name.tar repository:tag
# docker save
- docker save image_name > file_name.tar
# docker load
- docker load image_name < file_name.tar
- docker load image_name -i file_name.tar
# docker commit
- docker commit contaier_id new_image_name
```



## Manage
|    Command    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |                                                                                     
| `docker container`  |Manage containers |`attach`, ...
| `docker image`      |Manage images |
| `docker volume`     |Manage volumes |`create`, `inspect`, `ls`, `prune`, `rm`  
| `docker manifest`   |Manage Docker image manifests and manifest lists |`create`, `inspect`, `push`, `rm`, `annotate`
| `docker builder`    |Manage builds |`build`, `prune`
| `docker checkpoint` |Manage checkpoints |`create`, `ls`, `rm`
| `docker context`    |Manage contexts |`create`, `export`, `imoprt`, `inspect`, `ls`, `rm`, `update`, `use`
| `docker network`    |Manage networks |`create`, `connect`, `disconnect`, `inspect`, `ls`, `rm`, `prune`
| `docker plugin`     |Manage plugins |`create`, `disable`, `enable`, `inspect`, `ls`, `rm`, `push`, `set`, `upgrade`, `install`
| `docker system`     |Manage Docker |`events`, `df`, `info`, `prune`
| `docker secret`     |Manage Docker secrets |`create`, `inspect`, `ls`, `rm`
| `docker service`    |Manage services | `create`, `inspect`, `ls`, `rm`, `ps`, `logs`, `rollback`, `scale`, `update`
| `docker stack`      |Manage Docker stacks |`services`, `deploy`, `ls`, `ps`, `rm`
| `docker trust`      |Manage trust on Docker images |`key`, `key load`, `revoke`, `sign`, `signer`, `signer add`, `signer remove`, `update`
| `docker node`       |Manage Swarm nodes |`demote`, `inspect`, `ls`, `ps`, `rm`, `promote`, `update`
| `docker config`     |Manage Docker configs |`create`, `inspect`, `rm`, `ls`
| `docker buildx`     | |[docs](https://docs.docker.com/engine/reference/commandline/buildx/)

!!!quote
    [Docker-docs-BaseCommand](https://docs.docker.com/engine/reference/commandline/docker/)
