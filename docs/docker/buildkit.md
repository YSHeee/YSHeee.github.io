# Buildkit
\: a toolkit for converting source code to build artifacts in an efficient, expressive and repeatable manner.  
\: **It can run build steps in parallel** when possible

- Distributable workers  
- Nested build job invocations  
- Build cache import/export  
- Execution without root privileges  
- ...

---
:fontawesome-solid-star: Docker Desktop
: **BuildKit is enabled by default for all users on Docker Desktop.**  
 you don’t have to manually enable BuildKit.   

If you want to change the buildkit setting
```bash
1. Docker Desktop → Preference → Docker Engine 
2. 다음을 false로 변경

  "features": {
    "buildkit": true
}
```

:fontawesome-solid-star: Linux   
① To set the BuildKit environment variable when running the docker build command  
```bash
DOCKER_BUILDKIT=1 docker build -t name .
```
② To set enable docker BuildKit by default,  
```bash
1. /etc/docker/daemon.json에 추가
{
  "features": {
    "buildkit" : true
  }
}
2. Restart the Docker daemon
```
---

!!!quote
    - docker-docs:BuildKit :material-arrow-right-bold:
    [BuildKit-docs](https://docs.docker.com/build/buildkit/)  
    - Github:BuildKit :material-arrow-right-bold:
    [BuildKit-Github](https://github.com/moby/buildkit)  
    - Useful Blog :material-arrow-right-bold:
    [Blog1](https://blukat.me/2021/07/docker-buildkit-speedup/)

