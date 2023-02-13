## Commands 
|    Command    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
| `docker compose up`       |Create and start containers <div> (Build, (re)create, start, attach) | `--attach`, `--build`, `--pull`, `--timeout`, <div> [docs](https://docs.docker.com/engine/reference/commandline/compose_up/)
| `docker compose down`     |컨테이너 중지 후 관련 컨테이너, 네트워크, 볼륨, 이미지 제거 <div> (Networks and volumes defined as **external** are never removed.) | `--remove-orphans`, `--rmi`, `--timeout`, `--volumes`
| `docker compose ls`       |List running compose projects | `-a`, `-q`, `--filter`, `--format`
| `docker compose build`    |Build or rebuild services | [docs](https://docs.docker.com/engine/reference/commandline/compose_build/)
| `docker compose convert`  |compose 파일을 플랫폼의 표준 형식으로 변환 | [docs](https://docs.docker.com/engine/reference/commandline/compose_convert/)
| `docker compose cp`       |서비스 컨테이너와 로컬 파일시스템 간 파일/폴더 복사 |`--archive`, `--index`, `-L`
| `docker compose create`   |Creates containers for a service <div> (start command to start the container at any point)| `--pull`,`build`, `--force-recreate`,`--no-build`,`--no-recreate`
| `docker compose events`   |프로젝트의 모든 컨테이너 이벤트 스트리밍 | `--json`
| `docker compose exec`     |Execute a command in a running container | `-d`, `-e`, [docs](https://docs.docker.com/engine/reference/commandline/compose_exec/)
| `docker compose images`   |생성된 컨테이너에서 사용하는 이미지 리스트 | `--format`, `-q`
| `docker compose kill`     |서비스 컨테이너 강제 중지 | `--remove-orphans`, `--signal`
| `docker compose logs`     |Displays log output from containers | [docs](https://docs.docker.com/engine/reference/commandline/compose_logs/)
| `docker compose pause`    |Pauses running containers of a service |
| `docker compose unpause`  |Unpauses paused containers of a service |
| `docker compose port`     |포트바인딩을 위한 public port 출력 | `--index`, `--protocol`
| `docker compose ps`       |List containers | `-a`, `-q`, `--format`, `--filter`, `--services`, `--status`
| `docker compose pull`     |Pull service images | `-q`, [docs](https://docs.docker.com/engine/reference/commandline/compose_pull/)
| `docker compose push`     |Push service images | `-q`, `--ignore-push-failures`, `--include-deps`
| `docker compose restart`  |Restart service containers <div> (compose.yml 변경사항 반영 X)| `--timeout`
| `docker compose rm`       |Removes stopped service containers | `-f`, `--stop`, `--volumes`
| `docker compose run`      |Run a one-off command on a service. | [docs](https://docs.docker.com/engine/reference/commandline/compose_run/)
| `docker compose stop`     |Stops running containers without removing them | `--timeout`
| `docker compose start`    |Starts existing containers for a service |
| `docker compose top`      |Display the running processes |
| `docker compose version`  |Show the Docker Compose version information | `--format`, `--short`

## Options
|    Command    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
| `docker compose -f`    |Specifying multiple Compose files |
| `docker compose -p`    |specify a project name            | 지정하지 않을 시, 환경변수 또는 디렉터리 이름 사용
| `--ansi`               |Control when to print ANSI control characters (never, always, auto) | default auto
| `--file`, `-f`         |Compose configuration files |
| `--env-file`           |Specify an alternate environment file |
| `--parallel`           |Control max parallelism, -1 for unlimited |
| `--profile`            |Specify a profile to enable |
| `--project-directory`  |Specify an alternate working directory | default the path of the, first specified, Compose file
| `--project-name`, `-p` |Project name |
| `--verbose`            |Show more output |
| `--version`, `-v`      |Show the Docker Compose version information |

Example
```
- docker compose -f docker-compose.yml -f docker-compose.admin.yml run backup_db
- docker compose -p my_project ps -a
```
!!!quote
    [Dockerdocs-compose-Command](https://docs.docker.com/engine/reference/commandline/compose/)