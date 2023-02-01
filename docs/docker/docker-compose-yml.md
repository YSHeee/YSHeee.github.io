# Docker compose statement
``` yaml
version:
services: 
    <service_name>:
        image: 
        links:
        hostname:
        environment:
        restart:
        volumes:
        platform:
        build:
            context:
            dockerfile:
        entrypoint:
        command:
        logging:
            driver:
            options:
                #fluentd-address:
                #tag:
        healthcheck:
            test:
            interval:
            timeout:
            retries:
            start_period:
        depends_on:
        env_file:
        ports:
        tty:
        networks:
        secrets:
            source:
            target:
        deploy:
            mode:
            replicas:
            update_config:
                parallelism:
                order:
                delay:
                failure_action:
        dns:
        labels:
        devices:
        external_links:
        extra_hosts:
    
    <service_name2>:
        ...

networks:
    <network_name>
        external:
            name: <network_name>
volumes:

```

|    statement    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
| `version`     |해당 도커파일에 사용된 도커 컴포즈 파일 형식의 버전 |

|    statement    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
| ⬇ **`services`** |애플리케이션을 구성하는 모든 서비스  |
| `image`           |실행할 이미지 지정(컨테이너 이름이자 DNS이름) |
| `links`           |다른 컨테이너와의 연결|
| `hostname`        |Hostname 설정 |
| `environment`     |컨테이너에서 사용될 환경 변수 값 정의 |
| `restart`         |컨테이너 restart 방식 설정 |`no`:수동으로 재시작<div>`always`:컨테이너를 수동으로 끄기 전까지 항상 재시작<div>`on-failure`:오류가 있을 시 재시작
| `volumes`         |지정한 경로의 Volume 마운트 |
| `platform`        |OS Architecture| `linux/arm64`, `linux/amd64`, ...
| `build`<div>`context`<div>`dockerfile` |해당 디렉터리에 있는 Dockerfile 빌드<div>build context path<div>빌드할 도커파일 이름 |Dockerfile: `build: .`<div>Not 'Dockerfile': `context`,`dockerfile` 사용
| `entrypoint`      |ENTRYPOINT |
| `command`         |COMMAND |
| `logging`<div>`driver`<div>`options`    |logging 설정<div>logging driver 설정 |
| `healthcheck` <div>`test`<div>`interval`<div>`timeout`<div>`retries`<div>`start_period` |컨테이너 상태를 점검하기 위한 설정<div>health check command<div> 헬스 체크 실시 간격 <div> 실패로 간주하기까지의 제한 시간 <div> 상태 이상까지 필요한 연속 실패 횟수 <div>컨테이너 실행 후 첫 healthcheck 실시까지의 시간 간격 |
| `depends_on`      |해당 서비스가 다른 서비스에 의존함을 의미 <div> (해당 서비스 실행 전 나열된 기술을 먼저 실행)|
| `env_file`        |컨테이너 환경변수 정의를 위한 env_file 경로 |
| `ports`           |host:container (External port:Internal port)|
| `tty`             |keep the container running |
| `networks`        |서비스가 구성될 도커 네트워크 |
| `secrets`<div>`source`<div>`target` |실행 시 컨테이너 내부 파일에 기록될 secret value 정의 | DB password, 인증서, API Key ...
| `extends`         |make this service extend another |
| `dns`             |dns 설정 | 
| `labels`          |  |
| `devices`         |  |
| `external_links`  |  |
| `extra_hosts`     |  |
| `deploy`<div>`mode`<div>`replicas`<div>`update_config`  | |


|    statement    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
| ⬇ **`networks`**    |creates a custom network called `network_name` |
| `external`   |해당 네트워크는 이미 존재하므로 새로 생성 X |

|    statement    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
| `volumes`     |volume 생성 및 사용|


!!! quote
    [Docs compose-specification](https://docs.docker.com/compose/compose-file/)
    [Compose file version](https://docs.docker.com/compose/compose-file/compose-file-v3/)  
    [Useful Site](https://docs.divio.com/en/latest/reference/docker-docker-compose/)  
    [Useful cheatshet](https://gist.github.com/jonlabelle/bd667a97666ecda7bbc4f1cc9446d43a)  
    [Useful-Healthcheck](https://www.atatus.com/blog/health-check-command-in-docker/)