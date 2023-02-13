# Plex
\: video, music and photos from personal media libraries and streams them to smart TVs, streaming boxes and mobile devices

```yaml title="docker-compose.yml"
version: "2.1"
services:
  plex:
    image: lscr.io/linuxserver/plex:latest
    container_name: plex
    network_mode: host
    environment:
      - VERSION=docker
    volumes:
      - ${HOME}/plex:/media/
    restart: always
```
### `http://localhost:32400/web` 접속
!!! quote
    - [dockerHub](https://hub.docker.com/r/linuxserver/plex)
    - [awesome-compose](https://github.com/docker/awesome-compose/tree/master/plex)

---
# Pi-hole
``` yaml title="docker-compose.yml"
version: "3"

# More info at https://github.com/pi-hole/docker-pi-hole/ and https://docs.pi-hole.net/
services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    # For DHCP it is recommended to remove these ports and instead add: network_mode: "host"
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "67:67/udp" # Only required if you are using Pi-hole as your DHCP server
      - "80:80/tcp"
    environment:
      TZ: 'America/Chicago'
      # WEBPASSWORD: 'set a secure password here or it will be random'
    # Volumes store your data between container upgrades
    volumes:
      - './etc-pihole:/etc/pihole'
      - './etc-dnsmasq.d:/etc/dnsmasq.d'
    #   https://github.com/pi-hole/docker-pi-hole#note-on-capabilities
    cap_add:
      - NET_ADMIN # Required if you are using Pi-hole as your DHCP server, else not needed
    restart: unless-stopped
```

!!! quote
    - [Github](https://github.com/pi-hole/docker-pi-hole/#running-pi-hole-docker)
    - [DockerHub](https://hub.docker.com/r/pihole/pihole)
---
# Gitlab
``` yaml title="docker-compose.yml"
version: '3.6'
services:
  web:
    image: 'gitlab/gitlab-ce:latest'
    restart: always
    hostname: 'gitlab.example.com'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'https://gitlab.example.com'
        # Add any other gitlab.rb configuration here, each on its own line
    ports:
      - '80:80'
      - '443:443'
      - '22:22'
    volumes:
      - ${HOME}/temp/config:/etc/gitlab
      - ${HOME}/temp/logs:/var/log/gitlab
      - ${HOME}/temp/data:/var/opt/gitlab
    shm_size: '256m'
```
!!! quote
    - [Docs](https://docs.gitlab.com/ee/install/docker.html#install-gitlab-using-docker-compose)
    - [Blog-1](https://velog.io/@hanif/Docker%EB%A1%9C-GitLab-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%A0%91%EC%86%8D%ED%95%98%EA%B8%B0)