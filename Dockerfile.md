DockerFile
==========

> docker 이미지 작성 기능
> 이미지 생성을 위한 스크립트 작성, 이미지 생성
> customed image 생성, 배포 가능

# Dockerfile 옵션

## 1. FROM
> Docker Base Image 지정 명령(FROM httpd:alpine).  

> 이미 구현되어 있는 이미지 명시 
EX)
```
FROM {baseImage명}:{version}
FROM ubuntu:18.04
```


## 2. LABEL
> 버전 정보, 작성자와 같은 이미지 설명을 작성하기 위한 명령(LABEL version="1.0.0"). 
> {key} = {value} 형태로 사용 

## 3. CMD
> docker 컨테이너가 시작할 때, 쉘 명령을 지정하는 명령. RUN과 비슷하지만 RUN은 이미지 작성시 실행하는 명령, CMD는 컨테이너를 시작할 때 실행하는 명령어(CMD ['python', 'app.py'].  

```
1. 더 선호되는 방식 
CMD ["param1", "param2", ...]

CMD ["/bin/sh", "-c", "echo", "Hello"]
CMD ["executable", "param1", "param2", ...]
2. 
CMD <command> <param1> <param2> ....
```

## 4. RUN
> 쉘 명령을 실행하는 명령(RUN["apt-get", "install", "nginx"]). RUN은 이미지 작성시 실행되며, 일종의 새로운 이미지 layer를 만드는 역할.  

## 5. ENTRYPOINT
> docker 컨테이너가 시작할 때 실행하는 쉘 명령어를 지정하는 명령. docker run 커멘드 실행시, 별도 명령어도 넣을 수 있는데,
이 때 CMD 명령은 해당 명령을 덮어씌워짐. entrypoint로 지정한 명령은 docker run 커멘트 실행시 함께 넣어진 별도 명령어가 있더라도, 덮어씌워지지 않고 실행됩    

## 6. EXPOSE
> docker 컨테이너 외부에 오픈할 포트 설정(EXPORT 8080).  

## 7. ENV
> docker 컨테이너 내부에서 사용할 환경 변수 지정(ENV PATH /usr/bin:$PATH).  

## 8. WORKDIR
> docker 컨테이너에서의 작업 디렉토리 설정.  

## 9. COPY
> 파일, 디렉토리를 docker 컨테이너에 복사. ADD와 달리 URL은 지정할 수 없으며, 압축 파일을 자동으로 풀어주지 않음(COPY test.sh /root/test.sh).  
```
COPY {복사할 파일} {붙여넣을 디렉토리 위치}
```


# DockerFile 빌드

```
# dockerfile 빌드
$ docker build -t {이미지명} {작성한 도커파일 경로}
$ docker build -t frontend .
# -t == -tag

# Dockerfile로 빌드한 이미지 실행
$ docker run --name {실행image명} -v $(pwd):{workdir} -p {입력포트}:{컨테이너내부포트} {컨테이너명}
$ docker run --name front       -v $(pwd):/home/app -p  8080:8080              front-container

# docker logs 컨테이너ID 또는 이름
$ docker logs httpdweb1


```




























