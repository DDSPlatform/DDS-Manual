#### BRIQUE Analytics 설치 가이드 (Stand Alone 버전)



본 문서는 BRIQUE Analytics를 독립서버로 구동하기 위한 설치 방법을 포함하고 있음



------------------------------------------------------

##### H/W 요구사양

- Operating System
  - Linux
    - CentOS 7.x 이상
    - RedHat 7 이상
  - Windows
    - Windows 10 64-bit
      - Home or Pro 2004 (build 19041) 이상 
      - Enterprise or Education 1909 (Build 18363) 이상
    - Windows 11 64-bit
      - Home or Pro version 21H2 이상
      - Enterprise or Education 21H2 이상
  
  
  
- Memory
  - 최소 16GB 이상
  
- CPU
  - 2.5GHz 4core X 1cpu 이상
  
- HDD
  - 100GB 이상



------

##### S/W 요구사항

BRIQUE Analytics는 Docker 기반의 이미지로 배포되며, 이를 위해서 운영체제에 맞는 Docker 엔진을 필요로 함

- Linux
  
  https://docs.docker.com/engine/install/
  
- Windows
  
  https://docs.docker.com/desktop/windows/install/



------------------------------------------

##### 1. 설치파일 다운로드

Linux 터미널 또는 Windows Power Shell을 이용해서 Docker Hub에 등록된 BA 공식 이미지 다운로드


```shell
# Docker 이미지 다운로드
$ docker pull brique/brique-analytics:v2.2.0-r1
```



------------------------------------------------------------------------------------------------------------------

##### 2. 실행

Linux 터미널 또는 Windows Power Shell을 이용해서 BA 서비스 시작 명령어 실행

```sh
# BRIQUE Analytics 설치폴더 생성
$ mkdir -p /home/ba/db /home/ba/resource /home/ba/script /home/ba/license

# BRIQUE Analytics 서비스 실행
$ docker run -it -d --name brique-analytics \
-p 8080:8080 \
-p 8081:8081 \
-p 8082:8082 \
-p 8084:8084 \
-p 8086:8086 \
-e ADVERTISE_ADDR=192.168.0.1 \
-e ADVERTISE_PORT_MAIN=8080 \
-e ADVERTISE_PORT_PLATFORM=8081 \
-e ADVERTISE_PORT_AUTH=8082 \
-e ADVERTISE_PORT_BATCH=8084 \
-e ADVERTISE_PORT_ADMIN=8086 \
-v /home/ba/db:/var/lib/pgsql/13 \
-v /home/ba/resource:/opt/ba/badata/resource \
-v /home/ba/script:/opt/ba/badata/script \
-v /home/ba/license:/opt/ba/badata/license \
brique/brique-analytics:v2.2.0-r1
```



```sh
#============================================================================
# BA 서비스 실행을 위한 환경변수 및 외부저장소 마운트 설명
#============================================================================
$ docker run -it -d --name {컨테이너명} \
-p {$ADVERTISE_PORT_MAIN}:8080 \
-p {$ADVERTISE_PORT_PLATFORM}:8081 \
-p {$ADVERTISE_PORT_AUTH}:8082 \
-p {$ADVERTISE_PORT_BATCH}:8084 \
-p {$ADVERTISE_PORT_ADMIN}:8086 \
-e ADVERTISE_ADDR={$ADVERTISE_ADDR} \
-e ADVERTISE_PORT_MAIN={$ADVERTISE_PORT_MAIN} \
-e ADVERTISE_PORT_PLATFORM={$ADVERTISE_PORT_PLATFORM} \
-e ADVERTISE_PORT_AUTH={$ADVERTISE_PORT_AUTH} \
-e ADVERTISE_PORT_BATCH={$ADVERTISE_PORT_BATCH} \
-e ADVERTISE_PORT_ADMIN={$ADVERTISE_PORT_ADMIN} \
-v {ExternalVolumeForDB}:/var/lib/pgsql/13 \
-v {ExternalVolumeForResource}:/opt/ba/badata/resource \
-v {ExternalVolumeForScript}:/opt/ba/badata/script \
-v {ExternalVolumeForLicense}:/opt/ba/badata/license \
brique/brique-analytics:v2.2.0-r1
```



###### 진행상황 확인

Docker 컨테이너 로그를 통해 서비스 실행 과정에 대한 확인이 가능함



- DBMS 디렉토리가 초기화되지 않은 경우

  ```Sh
  $ docker logs -f {myContainerName}
  Initializing BRIQUE Analytics docker container.
  Checking internal postgresql Database...
  The files belonging to this database system will be owned by user "postgres".
  This user must also own the server process.
  
  The database cluster will be initialized with locale "ko_KR.UTF-8".
  The default database encoding has accordingly been set to "UTF8".
  initdb: could not find suitable text search configuration for locale "ko_KR.UTF-8"
  The default text search configuration will be set to "simple".
  
  Data page checksums are disabled.
  
  fixing permissions on existing directory /var/lib/pgsql/13/data ... ok
  creating subdirectories ... ok
  selecting dynamic shared memory implementation ... posix
  selecting default max_connections ... 100
  selecting default shared_buffers ... 128MB
  selecting default time zone ... Asia/Seoul
  creating configuration files ... ok
  running bootstrap script ... ok
  performing post-bootstrap initialization ... ok
  syncing data to disk ... ok
  
  ......
  
  Initialized Database ba220r1
  Starting Redis...
  Redis started.
  Starting Kafka...
  Formatting /data/kafka/kraft-combined-logs
  Kafka started.
  Advertise address: 127.0.0.1
  Checking script directory...
  Starting BRIQUE Analytics web server...
  BRIQUE Analytics web server started.
  Starting BRIQUE Analytics script engine...
  BRIQUE Analytics script engine started.
  Starting BRIQUE Analytics interpreter...
  BRIQUE Analytics interpreter started.
  BRIQUE Analytics - Ready to Use!
  Connect to 127.0.0.1:8080 in your web browser.
  Log in with default user account `admin` with password `brique_admin`
  ```

  

- 외부 매핑된 DBMS 디렉토리가 있고 이미 생성된 DB 스키마가 존재하는 경우

  ```sh
  $ docker logs -f {myContainerName}
  Initializing BRIQUE Analytics docker container.
  Checking internal postgresql Database...
  Database for BRIQUE Analytics already exists. Skipping tablespace initialization.
  Starting Postgres...
  Postgres started.
  Starting Redis...
  Redis started.
  Starting Kafka...
  Formatting /data/kafka/kraft-combined-logs
  Kafka started.
  Advertise address: 192.168.0.92
  Checking script directory...
  Starting BRIQUE Analytics web server...
  BRIQUE Analytics web server started.
  Starting BRIQUE Analytics script engine...
  BRIQUE Analytics script engine started.
  Starting BRIQUE Analytics interpreter...
  BRIQUE Analytics interpreter started.
  BRIQUE Analytics - Ready to Use!
  Connect to 192.168.0.92:48080 in your web browser.
  Log in with default user account `admin` with password `brique_admin`
  ```



###### 환경변수 설명

| 환경변수                | 기본 값   | 설명                                              |
| ----------------------- | --------- | ------------------------------------------------- |
| ADVERTISE_ADDR          | 127.0.0.1 | BRIQUE Analytics 접속 IP                          |
| ADVERTISE_PORT_MAIN     | 8080      | 메인 API 서비스 포트                              |
| ADVERTISE_PORT_PLATFORM | 8081      | Platform 서비스 포트                              |
| ADVERTISE_PORT_AUTH     | 8082      | 인증 API 서비스 포트                              |
| ADVERTISE_PORT_BATCH    | 8084      | 배치 API 서비스 포트                              |
| ADVERTISE_PORT_ADMIN    | 8086      | 관리 API 서비스 포트                              |
| REDIS_PASS              | ba220r1   | (Optional) Redis (6379) 패스워드                  |
| POSTGRES_USER           | ba220r1   | (Optional) PostgreSQL DBMS (5432) 사용자 계정     |
| POSTGRES_PASS           | ba220r1   | (Optional) PostgreSQL DBMS (5432) 사용자 패스워드 |



###### 외부저장소 마운트 설명

| 외부 저장소               | 설명                                                   |
| ------------------------- | ------------------------------------------------------ |
| ExternalVolumeForDB       | PostgreSQL 루트 경로, 워크플로우 정보가 저장될 위치    |
| ExternalVolumeForResource | 사용자 생성 리소스 (File, JDBC, Scripts)가 저장될 위치 |
| ExternalVolumeForScript   | 사용자 생성 스크립트 및 타스크 실행 결과가 저장될 위치 |
| ExternalVolumeForLicense  | 발급받은 라이선스 파일이 저장될 위치                   |



------

##### 3. 동작 확인

크롬 브라우져를 통해 BRIQUE Analytics에 접속

- 접속 URL

  http://localhost:8080

- 접속계정

  admin / brique_admin



------

##### 4. 라이선스

최초 설치 시, Docker 이미지 내에 2023년 1월 1일까지의 라이선스가 포함되어 있으며, 라이선스 만료 또는 새로운 라이선스를 사용하고자 하는 경우, 담당자 이메일로 신규발급 요청을 해야함

`admin@brique.co.kr`

