## Instructions

|    Command    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
| `FROM`        |이미지 불러오기 |
| `ENV`         |환경 변수 값 지정|
| `WORKDIR`     |컨테이너 파일 시스템에 해당 directory 생성 및 작업 디렉터리로 지정|
| `COPY`        |File/directory를 컨테이너로 복사|
| `CMD`         |컨테이너 실행 시, 입력되는 커맨드 |
| `EXPOSE`      |컨테이너 포트 번호 지정 |                                                                                       
| `ENTRYPOINT`  |컨테이너 실행 시, 정의된 커맨드 실행 (주로 변하지 않는 값 지정) | 
| `LABEL`       |이미지 메타데이터 |
| `VOLUME`      |지정한 이름으로 mount point 생성 및 volume 생성|
| `HEALTHCHECK` |컨테이너 내부에서 실행되는 인스트럭션. 컨테이너의 상태를 출력받기 위함 |
| | |
| `STOPSIGNAL`  |sets the system call signal that will be sent to the container to exit. |
| `USER`        |Sets the user name(or UID) and optionally the user group(or GID) to use as the default user and group for the remainder of the current stage |
| `ADD`         | Copies new files, directories or remote file URLs from src and adds them to the filesystem of the image at the path dest |
| `RUN`         |이미지 빌드 과정에서 필요한 명령어 실행 | Ex) apt install, pip install ...
| `ARG`         |Defines a variable that users can pass at build-time to the builder with the docker build command using the --build-arg varname=value flag. |
| `SHELL`       |allows the default shell used for the shell form of commands to be overridden. |
| `ONBUILD`     |Adds to the image a trigger instruction to be executed at a later time, when the image is used as the base for another build |

!!!quote
    [Dockerdocs-Dockerfile](https://docs.docker.com/engine/reference/builder/)  
    [Cheat-sheet](https://kapeli.com/cheat_sheets/Dockerfile.docset/Contents/Resources/Documents/index)
