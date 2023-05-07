# 4-30: 0-2

## 1. 컨테이너와 도커의 이해 - 컨테이너를 쓰는 이유 / 일반 프로그램과 컨테이너 프로그램의 차이점

* 소프트웨어 운영 플랫폼이 바뀌고 있다
* bare metal -> virtualization -> any infrastructure
* 컨테이너: 용량이 작고 배포가 쉽다
* 왜 리눅스인가
  * chroot, namespace, cgroups라는 리눅스의 기능을 쓰니까

* 고객사의 환경이 다르더라도 컨테이너로 어플리케이션을 배포할 수 있음
* 확장성

# 5-01: 3-6

* docker라는 호스트네임으로 ubuntu 설치함
* centos는 필요없을것 같아서 안함 -> 나중에 하던가

# 5-02: 7-8

* docker 설치하고 gurugio 유저를 docker라는 그룹에 추가함

# 5-03: 9-10

* 컨테이너 하나는 하나의 어플리케이션 프로세스이다
* 각각의 리소스(시피유/메모리, 유저 ID, 네트워크, 호스트네임) 등을 분리해서 가지고있다.
* 도커 호스트: 리눅스 커널을 가진 시스템
* 도커 호스트에 도커 데몬을 설치/실햄 -> 도커가 실행될 수 있음
* 도커 데몬 위에 컨테이너 실행

* 컨테이너 image: base image layer(UUID / 1.23MB) + app source image layer (UUID / 2KB) + run app
* container image consists of multi layers.
* Each layer has UUID.
* A container image is a file -> run that file -> container
* Container image is READ-ONLY.

```
docker search nginx
docker pull nginx:latest
docker run -d --name web -p 80:80 nginx:latest
```


# 5-04: 11-12

* Dockerfile: set of commands to build a container with Docker
* Many instructions in Dockerfile
* # comment
* FROM: base image ===> SHOULD be first
* COPY: copy file of host
* ADD: copy tar/url
* RUN: command to be ran upon base image
* USER: change user
* ENTRYPOINT: a command to be run when container starts => cannot be changed with docker command
* CMD: a command or argument for ENTRYPOINT => optionable for docker command

```
docker build -t hellojs:latest .
docker login
docker push hellojs:latest
```
* '.' -> base location is current directory


# 5-05: 13-14

* docker registry: 컨테이너 보관 창고? 컨테이너 이미지를 저장함
* Docker Hub: hub.docker.com 공개 이미지 저장소
* Private Registry: 사내 컨테이너 저장소

```
docker search [KEYWORD]
```

* Download "registry" container to create a private registry
* MUST set private repository address when pushing/downloading container image

```
localhost:5000/ubuntu:18.04
```


# 5-08: 15-16

image관리
```
docker search [option] <image name:tag>
docker pull [option] <image:flag>
docker images
docker inspect [option] <image:flag>
docker rmi [option] <image>

```

컨테이너 생성 관리
```
docker create --name webserver nginx
docker start webserver
docker ps
docker inspect webserver
docker stop webserver
docker rm webserver
```

```
docker run --name webserver -d nginx:1.14 = pull + create + start
```

컨테이너에서 실행중인 프로세스 확인
```
docker top webserver
```

```
docker logs webserver 로그확인
docker exec webserver /bin/bash 컨테이너안에서 쉘실행
docker exec -it webserver /bin/bash
```

# 5-09: 17-18
# 5-10: 19-20
# 5-11: 21-22
# 5-12: 23-25
