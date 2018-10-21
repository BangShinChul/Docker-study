# Docker-study
Docker를 사용하면서 공부한것을 적어놓는 곳입니다.

참고 
- https://docs.docker.com/get-started/#test-docker-version
- https://docker-curriculum.com/
- https://blog.nacyot.com/articles/2014-01-27-easy-deploy-with-docker/

***
### docker 설치

```
$ sudo apt-get install docker
```

<br>

### docker run : run 명령어를 통해 image를 container로 올려 실행시킵니다.

```
$ docker run hello-world
```

### docker conatiner ls : 현재 컨테이너 상태를 알아볼 수 있는 명령어 입니다.

```
$ docker container ls
```

내려간 컨테이너까지 모두 확인해보는 명령어는 아래와 같습니다.

```
$ docker container ls --all
```

### docker search {image-name} : 원하는 도커 이미지를 docker hub에서 검색할 수 있습니다.

```
$ docker search ubuntu

NAME                                                   DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
ubuntu                                                 Ubuntu is a Debian-based Linux operating s...   8576      [OK]
dorowu/ubuntu-desktop-lxde-vnc                         Ubuntu with openssh-server and NoVNC            230                  [OK]
rastasheep/ubuntu-sshd                                 Dockerized SSH service, built on top of of...   176                  [OK]
consol/ubuntu-xfce-vnc                                 Ubuntu container with "headless" VNC sessi...   129                  [OK]
ansible/ubuntu14.04-ansible                            Ubuntu 14.04 LTS with ansible                   95                   [OK]
ubuntu-upstart                                         Upstart is an event-based replacement for ...   92        [OK]
neurodebian                                            NeuroDebian provides neuroscience research...   54        [OK]
1and1internet/ubuntu-16-nginx-php-phpmyadmin-mysql-5   ubuntu-16-nginx-php-phpmyadmin-mysql-5          48                   [OK]
ubuntu-debootstrap                                     debootstrap --variant=minbase --components...   39        [OK]
nuagebec/ubuntu                                        Simple always updated Ubuntu docker images...   23                   [OK]
tutum/ubuntu                                           Simple Ubuntu docker images with SSH access     18            
i386/ubuntu                                            Ubuntu is a Debian-based Linux operating s...   14            
1and1internet/ubuntu-16-apache-php-7.0                 ubuntu-16-apache-php-7.0                        13                   [OK]
ppc64le/ubuntu                                         Ubuntu is a Debian-based Linux operating s...   12            
eclipse/ubuntu_jdk8                                    Ubuntu, JDK8, Maven 3, git, curl, nmap, mc...   6                    [OK]
1and1internet/ubuntu-16-nginx-php-5.6-wordpress-4      ubuntu-16-nginx-php-5.6-wordpress-4             6                    [OK]
codenvy/ubuntu_jdk8                                    Ubuntu, JDK8, Maven 3, git, curl, nmap, mc...   4                    [OK]
darksheer/ubuntu                                       Base Ubuntu Image -- Updated hourly             4                    [OK]
pivotaldata/ubuntu                                     A quick freshening-up of the base Ubuntu d...   2             
smartentry/ubuntu                                      ubuntu with smartentry                          1                    [OK]
1and1internet/ubuntu-16-sshd                           ubuntu-16-sshd                                  1                    [OK]
ossobv/ubuntu                                          Custom ubuntu image from scratch (based on...   0             
paasmule/bosh-tools-ubuntu                             Ubuntu based bosh-cli                           0                    [OK]
1and1internet/ubuntu-16-healthcheck                    ubuntu-16-healthcheck                           0                    [OK]
pivotaldata/ubuntu-gpdb-dev                            Ubuntu images for GPDB development              0             
```

### docker pull {image-name:tag} : 해당 명령어로 docker hub에서 이미지를 내려받을 수 있습니다. tag를 생략하면 가장 최근의 버젼으로 내려받습니다.

```
$ docker pull ubuntu:16.04

16.04: Pulling from library/ubuntu
18d680d61657: Pull complete
0addb6fece63: Pull complete
78e58219b215: Pull complete
eb6959a66df2: Pull complete
Digest: sha256:76702ec53c5e7771ba3f2c4f6152c3796c142af2b3cb1a02fce66c697db24f12
Status: Downloaded newer image for ubuntu:16.04

$ docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              16.04               4a689991aa24        2 days ago          116 MB
hello-world         latest              4ab4c602aa5e        6 weeks ago         1.84 kB

```

이미지를 다운로드 받을 때 버젼의 태그명 없이 다운로드받을 경우 아래와 같습니다.

```
$ docker pull ubuntu

Using default tag: latest
latest: Pulling from library/ubuntu
473ede7ed136: Pull complete
c46b5fa4d940: Pull complete
93ae3df89c92: Pull complete
6b1eed27cade: Pull complete
Digest: sha256:29934af957c53004d7fb6340139880d23fb1952505a15d69a03af0d1418878cb
Status: Downloaded newer image for ubuntu:latest

$ docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              16.04               4a689991aa24        2 days ago          116 MB
ubuntu              latest              ea4c82dcd15a        2 days ago          85.8 MB
hello-world         latest              4ab4c602aa5e        6 weeks ago         1.84 kB

```
<br>
Docker는 이미지를 컨테이너화 시켜 올렸다 내립니다.<br>
컨테이너는 이미지가 사용할 메모리 용량만큼만의 메모리를 격리시켜 사용하는 기술입니다.<br>
즉, 컨테이너화 시킨다는것은 이미지만큼의 메모리용량을 격리시킨다는 이야기입니다.<br>
그리고 Docker는 컨테이너를 내려도 컨테이너만 내렸을 뿐이지 삭제시키지는 않습니다.<br>
<br>
아래의 명렁어 처럼 컨테이너의 이름으로 직접 rm(삭제)를 해주어야 완벽하게 컨테이너가 삭제됩니다.<br>
이런 작업은 효율적인 메모리관리를 위해 꼭 필요합니다.

```
$ docker run ubuntu

$ docker container ls -all

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
fef37a3fdb10        ubuntu              "/bin/bash"         25 seconds ago      Exited (0) 24 seconds ago                   vibrant_cori

$ docker container rm vibrant_cori
vibrant_cori

$ docker container ls -all
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

```

만약 exited된 컨테이너가 많을 경우 아래의 명령어로 한번에 처리할 수 있습니다.

```
$ docker rm $(docker ps -a -q -f status=exited)
```
