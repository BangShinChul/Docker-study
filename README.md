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
