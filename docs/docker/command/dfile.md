## Instructions

|    Command    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
| `FROM`        |이미지 불러오기 |
| `ENV`         |환경 변수 값 지정|
| `WORKDIR`     |컨테이너 파일 시스템에 해당 directory 생성, 작업 디렉터리로 지정|
| `COPY`        |File/directory를 이미지의 파일 시스템에 복사| `단순 copy`
| `ADD`         | new file, dir, remote file URL을 복사하여 <br> 경로 대상 이미지의 파일 시스템에 추가 | `압축 해제`, `URL 지원` |
| `EXPOSE`      |컨테이너 포트 번호 지정 |
| `CMD`         |컨테이너 실행 시, 입력되는 커맨드 | **only one** in Dockerfile
| `ENTRYPOINT`  |컨테이너 실행 시, 정의된 커맨드 실행 (주로 변하지 않는 값 지정) |
| `LABEL`       |이미지에 메타데이터 추가 <br> 이름, 버전, 저작자 정보 등 |
| `VOLUME`      |지정한 이름으로 mount point 생성 및 volume 생성|
| `USER`        |사용자 이름(or UID) 또는 사용자 그룹(or GID) 설정 |
| `RUN`         |이미지 빌드 과정에서 필요한 명령어 실행 | apt install, ...
| `ARG`         |docker build 명령 시 입력받을 수 있는 인자 선언 <div> (암호는 X, docker history로 확인 가능하기 때문) | `--build-arg`
| `SHELL`       |빌드 시 사용할 셸 변경 <div> zsh, csh, tcsh, powershell 사용 가능|
| `HEALTHCHECK` |컨테이너 내부에서 실행되는 인스트럭션| **only one** in Dockerfile |
| `STOPSIGNAL`  |docker stop 명령 시 컨테이너 안에서 실행 중인 <br> 프로그램에 전달되는 시그널 변경|
| `ONBUILD`     |해당 이미지에서 파생된 하위 이미지에서 실행되는 trigger|
| `MAINTAINER`  |생성된 이미지의 Author field 설정 |

Example
``` dockerfile
## FROM (default tag: latest)
FROM <image>
FROM <image>:<tag>
FROM <image>@<digest>

## ENV
ENV <key> <value>
ENV <key>=<value> 

## WORKDIR
WORKDIR <path>

## COPY
COPY <src> <dest>

## ADD  
ADD <복사할 파일 경로> <이미지에서 파일이 위치할 경로>

## CMD
CMD ["<executable>","<param1>","<param2>"] ➤ (exec form, this is the preferred form)
CMD ["<param1>","<param2>"] ➤ (as default parameters to ENTRYPOINT)
CMD <command> <param1> <param2> ➤ (shell form)

## EXPOSE
EXPOSE <port>

## ENTRYPOINT
ENTRYPOINT ["<executable>", "<param1>", "<param2>"] ➤ (exec form, preferred)
ENTRYPOINT <command> <param1> <param2> ➤ (shell form)

## LABEL
LABEL <key>=<value>

## VOLUME
VOLUME <path>

## HEALTHCHECK
HEALTHCHECK [<options>] CMD <command> ➤ (check container health by running a command inside the container)
HEALTHCHECK NONE ➤ (disable any healthcheck inherited from the base image)
# options
--interval=<duration> (default 30s)
--timeout=<duration> (default 30s)
--retries=<number> (default 3)
# Exit code
0: success, 컨테이너가 정상적이고 사용 가능한 상태
1: unhealthy, 컨테이너가 올바르게 작동하지 않는 상태
2: reserved, (do not use this exit code)

## STOPSIGNAL
STOPSIGNAL <signal>

## USER
USER <username>

## RUN
RUN <command>
RUN ["<executable>", "<param1>", "<param2>"] ➤ (exec form)

## ARG
ARG <name>
# predefined ARG variables
HTTP_PROXY and http_proxy
HTTPS_PROXY and https_proxy
FTP_PROXY and ftp_proxy
NO_PROXY and no_proxy

## SHELL
SHELL ["<executable>", "<param1>", "<param2>"]

## ONBUILD
ONBUILD <Dockerfile INSTRUCTION>

## MAINTAINER
MAINTAINER <name>
```

!!!quote
    [Dockerdocs-Dockerfile](https://docs.docker.com/engine/reference/builder/)  
    [docs Best-practice](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) 
    [Cheat-sheet](https://kapeli.com/cheat_sheets/Dockerfile.docset/Contents/Resources/Documents/index)
