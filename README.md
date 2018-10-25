# Docker-study
Docker를 사용하면서 공부한것을 적어놓는 곳입니다.

참고 
- https://docs.docker.com/get-started/#test-docker-version
- https://docker-curriculum.com/
- https://blog.nacyot.com/articles/2014-01-27-easy-deploy-with-docker/

***

### docker install

> 아래 명령어를 통해 Ubuntu에서 docker를 설치할 수 있습니다.

```
$ sudo apt-get install docker
```

<br><br>

### docker run {image-name:tag}

> run 명령어를 통해 image를 container로 올려 실행시킵니다.

docker run -i -t --name 원하는이름명 이미지명 : 컨테이너를 원하는 이름으로 띄움과 동시에 컨테이너에 들어가는 작업을 실행시키는 명령어 입니다.

```
$ docker run hello-world
```

<br><br>

아래의 명령어 처럼 컨테이너를 실행시킬 때 -it 혹은 -i -t 를 붙여주면 컨테이너 생성과 동시에 컨테이너의 bash를 사용 접속할 수 있습니다.

```
$ docker run -it ubuntu

root@d4127a5c2503:/# cat /etc/issue
Ubuntu 18.04.1 LTS \n \l

```

<br><br>

컨테이너에 접속한 뒤 ctrl+p,q를 누르면 컨테이너를 exit하지않고 bash를 빠져나올 수 있습니다.
아래의 STATUS를 보면 STATUS가 Exited가 아니라 Up으로 되어있는걸 확인해볼 수 있습니다.

```
$ docker ps -a

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
5e35d722aa40        ubuntu              "/bin/bash"         28 seconds ago      Up 28 seconds                           test

```

<br><br>

### docker conatiner ls

> 아래의 명령어로 현재 docker 내의 컨테이너 상태를 확인할 수 있습니다.

```
$ docker container ls

# 위 명령어는 아래와 동일합니다.

$ docker ps
```

<br><br>

내려간 컨테이너까지 모두 확인해보는 명령어는 아래와 같습니다.

```
$ docker container ls --all

# 위 명령어 또한 아래와 동일합니다.

$ docker ps -a
```

<br><br>

### docker restart {image-name or container-id}

> restart 명령어를 통해 종료된 컨테이너를 재실행 시킬 수 있습니다.

아래는 ubuntu라는 이름의 Exited된 컨테이너를 restart 시키는 예제입니다.

```
$ docker ps -a

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                   PORTS               NAMES
07553afdf72c        ubuntu              "/bin/bash"         2 hours ago         Exited (0) 2 hours ago                       ubuntu

$ docker restart ubuntu

ubuntu

$ docker ps -a

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
07553afdf72c        ubuntu              "/bin/bash"         2 hours ago         Up 4 seconds                            ubuntu

```

<br><br>

### docker search {image-name}

> 원하는 도커 이미지를 docker hub에서 검색할 수 있습니다.

search를 통해 원하는 이미지를 검색해서 NAME 값을 가지고 해당 이미지를 docker에 다운로드 할 수 있습니다.

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

<br><br>


### docker pull {image-name:tag}

> 해당 명령어로 docker hub에서 이미지를 내려받을 수 있습니다. tag를 생략하면 가장 최근의 버젼으로 내려받습니다.


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

<br><br>

이미지를 다운로드 받을 때 버젼의 태그명 없이 다운로드받을 경우 아래와 같습니다.
기본적으로 지정된 태그명이 없을 경우 latest가 기본으로 세팅되어 있습니다.

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

<br><br>

### docker rm {container-name or container-id}

> rm 명령어를 통해 컨테이너를 삭제할 수 있습니다.

Docker는 이미지를 컨테이너화 시켜 올렸다 내립니다.<br>
컨테이너는 이미지가 사용할 메모리 용량만큼만의 메모리를 격리시켜 사용하는 기술입니다.<br>
즉, 컨테이너화 시킨다는것은 이미지만큼의 메모리용량을 격리시킨다는 이야기입니다.<br>
그리고 Docker는 컨테이너를 내려도 컨테이너만 내렸을 뿐이지 삭제시키지는 않습니다.<br>
<br>
아래의 명렁어 처럼 컨테이너의 이름으로 직접 rm(삭제)를 해주어야 완벽하게 컨테이너가 삭제됩니다.<br>
이런 작업은 효율적인 메모리관리를 위해 꼭 필요합니다.

```
# 삭제 테스트용 컨테이너 run
$ docker run ubuntu # 이렇게 해도 됩니다 -> $ docker run -it --name 컨테이너이름 이미지이름

# 삭제할 컨테이너를 검색하기 위해 ls 명령어 실행
$ docker container ls -all # 이것도 마찬가지로 이렇게 해도 됩니다 -> $docker ps -a

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
fef37a3fdb10        ubuntu              "/bin/bash"         25 seconds ago      Exited (0) 24 seconds ago                   vibrant_cori # 컨테이너 확인

# 컨테이너명으로 rm 명령어 실행하여 컨테이너 삭제
$ docker container rm vibrant_cori

vibrant_cori # 삭제 완료

# 컨테이너가 정상적으로 삭제되었는지 확인하기 위해 ls 명령어 실행
$ docker container ls -all
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

```

<br><br>

만약 exited된 컨테이너가 많을 경우 아래의 명령어로 한번에 처리할 수 있습니다.

```
$ docker rm $(docker ps -a -q -f status=exited)
```

<br><br>

### docker commit {container-name or container-id} {OPTION: repository-name}/{image-name}:{OPTION: tag}

> commit 명령어를 통해 컨테이너를 이미지화 시킬 수 있습니다.

현재의 올려놓은 컨테이너를 이미지화 하고 싶다면 아래의 명령어처럼 입력해줍니다.
예를 들어, test라는 이름으로 ubuntu:latest 이미지를 컨테이너로 띄웠다고 가정합니다.
이 test라는 컨테이너를 이미지화 시키는 명령어는 아래와 같습니다.

```
$ docker commit test ubuntu:test

sha256:a72c5f89f7232c7f32402b871c26f014bbe2cdc63f168eaa27731b1edc059e22

혹은

$ docker container ls -a # 이미지로 만들 컨테이너 검색

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
07553afdf72c        ubuntu              "/bin/bash"         5 minutes ago       Exited (0) 9 seconds ago                       ubuntu

# 컨테이너의 ID는 정확하게 모두 입력하지 않고 일부만 입력하더라도 다른 컨테이너와 겹치는 부분이 없다면 고유하게 인식합니다.
$ docker commit 07553 ubuntu-test/ubuntu:test # 이미지 생성 명령어 실행

sha256:11d480933762769e0adf8de5c44ccf70d7dc9633df962699013d814e56ae8409 

$ docker images # 이미지가 잘 만들어졌는지 확인하기 위해 images 명령어 실행

REPOSITORY           TAG                 IMAGE ID            CREATED              SIZE
ubuntu-test/ubuntu   test                11d480933762        About a minute ago   85.8MB # 이미지 생성 확인
ubuntu               latest              ea4c82dcd15a        6 days ago           85.8MB
postgres             latest              7a2907672aab        6 days ago           311MB
node                 latest              a2b9536415c2        8 days ago           674MB
nginx                latest              dbfc48660aeb        8 days ago           109MB
ubuntu               16.04               b9e15a5d1e1a        7 weeks ago          115MB

```
