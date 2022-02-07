#### BRIQUE Analytics 설치 매뉴얼 (Stand Alone - Linux)

본 문서는 BRIQUE Analytics를 Linux 환경의 독립 서버로 구동하기 위한 설치 방법을 포함하고 있음




------

##### 시스템 요구사양



###### Operating System

- CentOS 7.x 이상
- RedHat 7 이상



###### S/W

- curl
- wget
- docker ([Install Docker Engine](https://docs.docker.com/engine/install/#server), `Server` section)



###### H/W

- CPU

  2.5GHz 4core X 1cpu 이상

- Memory

  16GB 이상

- HDD

  100GB 이상



------

##### 온라인 설치



###### 1. 설치파일 다운로드

```sh
# 설치 디렉토리 생성
$ mkdir ~/bainstall

# 설치파일 다운로드
$ cd ~/bainstall
$ curl -O https://ba.brique.kr/file/installer/v210r1/ba-2.1.0-r1.noarch.rpm
```



###### 2. 설치

```sh
# 설치 디렉토리로 이동
$ cd ~/bainstall

# Installer 설치
$ sudo yum localinstall -y ba-2.1.0-r1.noarch.rpm
......
Complete!

# 설치
$ sudo ba install ~/bainstall

......
# 기본값으로 설치하기 위해 Enter 키를 입력하여 진행

......
BA is installed completely. You can access BA at http://127.0.0.1:8080 with default username/password: admin/brique_admin
```



###### 3. 동작 확인

크롬 브라우져를 통해 BRIQUE Analytics에 접속

- 접속 URL

  http://localhost:8080

- 접속계정

  admin / brique_admin



------

##### 오프라인 설치



###### 1. 설치파일 다운로드

```sh
# 설치 디렉토리 생성
$ mkdir ~/bainstall
$ mkdir ~/bainstall/datafile
$ mkdir ~/bainstall/datafile/imgs

# 설치파일 다운로드 디렉토리로 이동
$ cd ~/bainstall/datafile

# BA 설치파일 다운로드
$ curl -O https://ba.brique.kr/file/installer/v210r1/ba-2.1.0-r1.noarch.rpm
$ curl -O https://ba.brique.kr/file/installer/v210r1/ba-v210.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/library_basic.tar.gz

# Python3.6 설치 및 패키지 파일 다운로드
$ curl -O https://ba.brique.kr/file/installer/v210r1/python36.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/python36-package-full.tar.gz

# R3.6.0 설치 및 패키지 파일 다운로드
$ curl -O https://ba.brique.kr/file/installer/v210r1/r360.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/r360-package-full.tar.gz

# Docker Image 다운로드 디렉토리로 이동
$ cd ~/bainstall/datafile/imgs

# Docker Image 파일 다운로드
$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/api.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/platform-http.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/platform-database.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/platform-workflow.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/platform-result.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/kafka.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/kafdrop.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/redis-slave.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/zoo.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/python36.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/python36download.tar.gz
$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/r360-image.tar.gz
```



###### 2. 설치

```sh
# 설치 디렉토리로 이동
$ cd ~/bainstall

# Installer 설치
$ sudo yum localinstall -y ba-2.1.0-r1.noarch.rpm
......
Complete!

# 설치
$ sudo ba install ~/bainstall

......
# 기본값으로 설치하기 위해 Enter 키를 입력하여 진행

......
BA is installed completely. You can access BA at http://127.0.0.1:8080 with default username/password: admin/brique_admin
```



###### 3. 동작 확인 (온라인 설치와 동일)

크롬 브라우져를 통해 BRIQUE Analytics에 접속

- 접속 URL

  http://localhost:8080

- 접속계정

  admin / brique_admin



------

##### 설치 제거

###### 1. 실행 중단

```sh
# 서비스 중단
sudo ba stop 
......

==> BA is stopped completely. To run BA again, use this command: ba start
```



###### 2. 설치파일 제거

```sh
# 설치 제거
sudo ba remove 
......

Removed BA completely. For more information, please visit https://ba.brique.kr/.
```

