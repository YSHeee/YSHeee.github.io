# Docker development **Best practices**

### 1. 이미지를 최대한 작은 사이즈로 생성하기

- Start with an appropriate *Base image*
```dockerfile title="Example: If you need a JDK"
# Unrecommend
FROM ubuntu
RUN apt-get update && \
    apt-get install -y openjdk-8-jdk && \
    apt-get install -y ant && \
    apt-get clean

# Recommend: use the official openjdk image
FROM openjdk
```
- Use multi-stage build

### 2. Do not rely on the automatically-created latest tag
- 이미지를 빌드할 때 항상 버전 정보, 의도한 제품/테스트 목적, 안정성, 기타 정보 등 유용한 태그 지정

### 3. Where and how to persist application data
- Store data using volumes
- Bind mounts 

### 4. Use CI/CD for testing and deployment

### ⍺. Dockerfile에서 변동성이 많은 코드를 아래로 둠으로써 cache 활용
- When building an image, Docker steps through the instructions in your Dockerfile, executing each in the order specified. As each instruction is examined, Docker looks for an existing image in its cache that it can reuse, rather than creating a new, duplicate image.


!!!quote
    [Docs Best-practice](https://docs.docker.com/develop/dev-best-practices/)  
    [Dockerfile Best-practice](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

