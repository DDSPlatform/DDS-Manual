#### BRIQUE Analytics 설치 가이드 (개인 PC용)

본 문서는 BRIQUE Analytics를 개인 Linx PC 환경에서 독립 서버로 구동하기 위한 설치 방법을 포함하고 있음



##### Revision History

| 등록일자   | 작성자 | 내용      |
| ---------- | ------ | --------- |
| 2021-11-25 | 최민우 | 신규 작성 |



------

##### 시스템 요구사양

- 운영체제 (64비트)

  - Linux RHEL 계열
    - CentOS 7 / 8
    - Fedora 32 이상
    - RedHat 7 이상
  
  - Linux Debian 계열
    - Debian Buster 10 (Stable) 이상
    - Ubuntu 18.04, 20.04  

- 메모리
  - 16 GB 이상

- CPU

  - x64 4 코어 이상
- Storage
  - 100 GB 이상



---
##### 사전 설치 시 확인 사항

- 인터넷 연결이 지원되지 않는 환경인 경우 다음 소프트웨어들이 미리 설치되어 있어야 합니다.
  - Linux: `curl`  `wget`  `docker`
- 본 예제 Script는 cent-os 기반으로 설명을 진행함



---

##### STEP 1 :  설치 파일 다운로드

- 홈페이지의 다운로드 링크 혹은 다음 URL에서 설치환경에 맞는 패키지를 다운로드

  - Debian 계열: https://ba.brique.kr/file/installer/v210r1/ba_2.1.0-r1-1_amd64.deb
  - RHEL 계열: https://ba.brique.kr/file/installer/v210r1/ba-2.1.0-r1.noarch.rpm
  
  

- 다운로드 받은 패키지가 있는 경로로 이동하여 패키지를 설치

  - Debian 계열 설치 명령어

    ```shell
    $ dpkg -i ba_2.1.0-r1-1_amd64.deb
    ```

  - RHEL 계열 설치 명령어

    ```shell
    $ sudo yum localinstall -y ba-2.1.0-r1.noarch.rpm
    ```

    - 설치 예제

      ```shell
      # 본 예제는 /mnt/E_DRIVE/bainstall 아래 설치 파일을 다운로드 함
      
      [brique@localhost E_DRIVE]$ mkdir bainstall  #설치 Directory 생성
      [brique@localhost E_DRIVE]$ cd bainstall/
      [brique@localhost bainstall]$ curl -O https://ba.brique.kr/file/installer/v210r1/ba-2.1.0-r1.noarch.rpm # 설치파일 다운로드
      
      [brique@localhost bainstall]$ sudo yum localinstall -y ba-2.1.0-r1.noarch.rpm  # 설치 진행
      Last metadata expiration check: 2:07:33 ago on Tue 14 Dec 2021 12:32:10 PM KST.
      Dependencies resolved.
      =============================================================================================================================================================================================================================================================================================================================
       Package                                                                 Architecture                                                                Version                                                                         Repository                                                                         Size
      =============================================================================================================================================================================================================================================================================================================================
      Installing:
       ba                                                                      noarch                                                                      2.1.0-r1                                                                        @commandline                                                                       25 k
      
      Transaction Summary
      =============================================================================================================================================================================================================================================================================================================================
      Install  1 Package
      
      Total size: 25 k
      Installed size: 77 k
      Downloading Packages:
      Running transaction check
      Transaction check succeeded.
      Running transaction test
      Transaction test succeeded.
      Running transaction
        Preparing        :                                                                                                                                                                                                                                                                                                     1/1
        Installing       : ba-2.1.0-r1.noarch                                                                                                                                                                                                                                                                                  1/1
        Verifying        : ba-2.1.0-r1.noarch                                                                                                                                                                                                                                                                                  1/1
      
      Installed:
        ba-2.1.0-r1.noarch
      
      Complete!
      
      ```

    - 정상 설치 되었을 경우 아래 위치에 설치 데이터가 존재해야 함 

      ```shell
      [brique@localhost bainstall]$ cd /usr/bin/ba-script/
      [brique@localhost ba-script]$ ll
      total 88
      -rw-r--r--. 1 root root  1098 Dec 13 15:55 ba-env.template
      -rwxr-xr-x. 1 root root   580 Dec 13 15:55 docker-node-swarm.sh
      -rwxr-xr-x. 1 root root 41673 Dec 13 15:55 install.sh
      -rwxr-xr-x. 1 root root   626 Dec 13 15:55 package.sh
      -rwxr-xr-x. 1 root root  2524 Dec 13 15:55 remove.sh
      -rw-r--r--. 1 root root  4753 Dec 13 15:55 requirements-python.txt
      -rw-r--r--. 1 root root  3090 Dec 13 15:55 requirements-r.txt
      -rwxr-xr-x. 1 root root 11370 Dec 13 15:55 start.sh
      -rwxr-xr-x. 1 root root   626 Dec 13 15:55 stop.sh
      [brique@localhost ba-script]$
      ```

      

##### STEP 2 :  Offline시 설치 파일 사전 다운로드

- 설치 시 사용되는 파일 및 Docker Image 파일을 datafile이라는 Directory 생성후 사전 다운로드를 진행함

- 설치파일 다운로드

  - 다운로드  Directory 생성

    ```shell
    # datafile Directory 생성
    [brique@localhost bainstall]$ mkdir datafile
    [brique@localhost bainstall]$ cd datafile  
    ```

  - 설치 대상 파일 위치

    - 한국어 버젼
    - https://ba.brique.kr/file/installer/v210r1/ba-v210.tar.gz # 어플리케이션 데이터 파일
    - 중국어 버젼(Cowin)
      - https://ba.brique.kr/file/installer/v210r1/ba-v210-cowin.tar.gz # 어플리케이션 데이터 파일
        - **다운 받은 후 파일명을 ba-v210-cowin.tar.gz -> ba-v210.tar.gz으로 반드시 변경**

    - https://ba.brique.kr/file/installer/v210r1/ba-v210.tar.gz # 어플리케이션 데이터 파일
    - https://ba.brique.kr/file/installer/v210r1/python36.tar.gz # Python 3.6 설치 파일
    - https://ba.brique.kr/file/installer/v210r1/python36-package-full.tar.gz # Python 3.6 패키지 파일
    - https://ba.brique.kr/file/installer/v210r1/r360.tar.gz # R 3.6.0 설치 파일
    - https://ba.brique.kr/file/installer/v210r1/r360-package-full.tar.gz # R 3.6.0 패키지 파일
    - https://ba.brique.kr/file/installer/v210r1/library_basic.tar.gz # Basic Library File

  - 다운로드 예제

    ```shell
    ##### 언어 버전 필수 선택 사항 #####
    ##### 한글 버전
       [brique@localhost datafile]$ curl -O https://ba.brique.kr/file/installer/v210r1/ba-v210-cowin.tar.gz
    ##### 중국어 버전, 파일명 반드시 Rename 필요 #####
       [brique@localhost datafile]$ curl -O https://ba.brique.kr/file/installer/v210r1/ba-v210-cowin.tar.gz 
       [brique@localhost datafile]$ mv ba-v210-cowin.tar.gz  ba-v210.tar.gz
    #####
    
    [brique@localhost datafile]$ curl -O https://ba.brique.kr/file/installer/v210r1/python36.tar.gz
    [brique@localhost datafile]$ curl -O https://ba.brique.kr/file/installer/v210r1/python36-package-full.tar.gz
    [brique@localhost datafile]$ curl -O https://ba.brique.kr/file/installer/v210r1/r360.tar.gz
    [brique@localhost datafile]$ curl -O https://ba.brique.kr/file/installer/v210r1/r360-package-full.tar.gz
    [brique@localhost datafile]$ curl -O https://ba.brique.kr/file/installer/v210r1/library_basic.tar.gz
    ```

  - 다운로드 결과

    - 다음과 같은 파일이 다운로드 되어 있으면 정상

      ```shell
      [brique@localhost datafile]$ ll
      total 2777208
      -rw-rw-r--. 1 brique brique  426973599 Dec 14 15:07 ba-v210.tar.gz
      drwxrwxr-x. 2 brique brique       4096 Dec 13 14:58 imgs
      -rw-rw-r--. 1 brique brique      37828 Dec 14 15:23 library_basic.tar.gz
      -rw-rw-r--. 1 brique brique 1729393867 Dec 14 15:18 python36-package-full.tar.gz
      -rw-rw-r--. 1 brique brique  109989133 Dec 14 15:10 python36.tar.gz
      -rw-rw-r--. 1 brique brique  446065759 Dec 14 15:22 r360-package-full.tar.gz
      -rw-rw-r--. 1 brique brique  131383068 Dec 14 15:20 r360.tar.gz
      ```

- Docker image 파일 다운로드 

  - 다운로드 Directory  생성

    - datafile 아래에 imgs 디렉토리 생성

      ```shell
      [brique@localhost bainstall]$ mkdir datafile
      [brique@localhost bainstall]$ cd datafile  
      ```

  - Docker images 설치 대상 파일 위치

    - https://ba.brique.kr/file/installer/v210r1/docker-image/api.tar.gz # 어플리케이션 도커 이미지 파일
    - https://ba.brique.kr/file/installer/v210r1/docker-image/platform-http.tar.gz
    - https://ba.brique.kr/file/installer/v210r1/docker-image/platform-database.tar.gz
    - https://ba.brique.kr/file/installer/v210r1/docker-image/platform-workflow.tar.gz
    - https://ba.brique.kr/file/installer/v210r1/docker-image/platform-result.tar.gz
    - https://ba.brique.kr/file/installer/v210r1/docker-image/kafka.tar.gz
    - https://ba.brique.kr/file/installer/v210r1/docker-image/kafdrop.tar.gz
    - https://ba.brique.kr/file/installer/v210r1/docker-image/redis-slave.tar.gz
    - https://ba.brique.kr/file/installer/v210r1/docker-image/zoo.tar.gz
    - https://ba.brique.kr/file/installer/v210r1/docker-image/python36-cpu.tar.gz
    - https://ba.brique.kr/file/installer/v210r1/docker-image/python36download.tar.gz
    - https://ba.brique.kr/file/installer/v210r1/docker-image/r360-image.tar.gz
    - https://ba.brique.kr/file/installer/v210r1/docker-image/postgres13.tar.gz
  
  - Docker images 다운로드 예제
  
      ```shell
      [brique@localhost imgs]$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/api.tar.gz # 어플리케이션 도커 이미지 파일
      [brique@localhost imgs]$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/platform-http.tar.gz
      [brique@localhost imgs]$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/platform-database.tar.gz
      [brique@localhost imgs]$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/platform-workflow.tar.gz
      [brique@localhost imgs]$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/platform-result.tar.gz
      [brique@localhost imgs]$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/kafka.tar.gz
      [brique@localhost imgs]$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/kafdrop.tar.gz
      [brique@localhost imgs]$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/redis-slave.tar.gz
      [brique@localhost imgs]$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/zoo.tar.gz
      [brique@localhost imgs]$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/python36.tar.gz
      [brique@localhost imgs]$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/python36download.tar.gz
      [brique@localhost imgs]$ curl -O https://ba.brique.kr/file/installer/v210r1/docker-image/r360-image.tar.gz
      ```


  - Docker images 다운로드 결과

      ```
      [brique@localhost imgs]$ ll
      total 25214800
      -rw-rw-r--. 1 brique brique  638053376 Dec 13 12:49 api.tar.gz
      -rw-rw-r--. 1 brique brique  615183360 Dec 13 12:43 kafdrop.tar.gz
      -rw-rw-r--. 1 brique brique  560834560 Dec 13 12:31 kafka.tar.gz
      -rw-rw-r--. 1 brique brique  523188224 Dec 13 12:35 platform-database.tar.gz
      -rw-rw-r--. 1 brique brique 3103157760 Dec 13 13:28 platform-http.tar.gz
      -rw-rw-r--. 1 brique brique 3103156736 Dec 13 12:00 platform-result.tar.gz
      -rw-rw-r--. 1 brique brique 3103158272 Dec 13 13:28 platform-workflow.tar.gz
      -rw-rw-r--. 1 brique brique  321848832 Dec 13 12:44 postgres13.tar.gz
      -rw-rw-r--. 1 brique brique 4130060800 Dec 13 13:16 python36-cpu.tar.gz
      -rw-rw-r--. 1 brique brique 3841901568 Dec 13 11:44 python36download.tar.gz
      -rw-rw-r--. 1 brique brique 5378486272 Dec 13 12:28 r360-image.tar.gz
      -rw-rw-r--. 1 brique brique   33388032 Dec 13 11:52 redis-slave.tar.gz
      -rw-rw-r--. 1 brique brique  467464704 Dec 13 12:49 zoo.tar.gz
      ```








------

##### STEP 3 : BRIQUE Analytics 설치 

- 설치 Root 위치에서 아래 명령어를 통해 설치를 진행

  - 설치 명령어  : sudo ba install [설치 경로]
    - 설치 경로는 datafile Directory가 생성된 위치(본예제 위치: /mnt/E_DRIVE/bainstall)

- 설치 도중 문의 항목이 나올 경우 Enter 입력시 Default값으로 설치를 진행

  ```shell
  ## 설치 시작
  [brique@localhost bainstall]$sudo ba install /mnt/E_DRIVE/bainstall
  
  tee: install_log.txt: Permission denied
  Installing BRIQUE Analytics
  Data Directory:
  [sudo] password for brique:
  [Step 1] Checking supported OS: Supported OS
  [Step 2] Check internet connection: You are online.
  Proceeding to online installation.
  [Step 3] Installing necessary packages:
  > To run BA, we need to install these packages: curl, wget, docker.
  >> Checking curl status: Installed.
  >> Checking wget status: Installed.
  >> Checking docker status: Installed.
  >>> Verifying docker service can be started..
  >>> Docker service is started completely.
  [Step 4] Starting swarm mode in docker
  > Initializing swarm mode:
  Error response from daemon: This node is already part of a swarm. Use "docker swarm leave" to leave this swarm and join another one.
  >> Done
  > Creating docker network ba-eco_nw...
  Error response from daemon: network with name ba-eco_nw already exists
  >> Done
  > Creating docker network ba-prod_nw...
  Error response from daemon: network with name ba-prod_nw already exists
  >> Done
  [Step 5] Installing BA
  > 5.1. Getting current user, host information
  >> Current user: brique
  >> Current user group: brique
  >> Current host IP address: 127.0.0.1
  >> Current hostname:  localhost.localdomain
  > 5.2. Enter directory path where you want to install Brique Analytics. (default: /opt/ba)
  # ba 설치 Directory 위치 지정 Default는 /opt/ba
  # /opt/ba 위치에 DiskSize가 100GB이상 존재 하는지 확인 해야 함
  >> Directory:
  >> Installing Brique Analytics at default directory: /opt/ba
  >> BA Directory: /opt/ba
  >>> Creating BA Directory. May need to input user password.
  > 5.3. BA configuration
  >> Postgresql port (default: 5432):
  >> Postgresql username (default: ba210 - We strongly recommend you to use only lowercase alphabets and numbers):
  >> Postgresql password (default: ba210):
  >> Redis password (default: ba210):
  >> Redis port (default: 6379):
  >> Kafdrop (Kafka Manager UI) port (default: 9000):
  >> Port prefix for BA (For example, platform port: 8081, main: 8080, auth: 8082 => port prefix is 808) (default: 808):
  >> Port for BA main (BA Main Server with Web UI, must be consistent with defined port prefix) (default: 8080):
  >> Port for BA platform (BA Core Engine, must be consistent with defined port prefix) (default: 8081):
  >> Port for BA auth (Authentication Server for BA, must be consistent with defined port prefix) (default: 8082):
  >> Port for BA admin (Administrator Page for BA, must be consistent with defined port prefix) (default: 8083):
  >> Port for BA batch (Background Job Manager for BA, must be consistent with defined port prefix) (default: 8084):
  >> BA configuration summary:
          Postgresql port: 5432
          Postgresql user: ba210
          Postgresql pass: ba210
          Redis port: 6379
          Kafdrop port: 9000
          BA prefix port: 808
          BA main port: 8080
          BA platform port: 8081
          BA auth port: 8082
          BA admin port: 8083
          BA batch port: 8084
  >> Entering to /opt/ba
  
  #설치는 자동으로 진행 됨
  
  ...
  
  #아래 메세지 나오면, 설치 완료
  # 설정한 환경변수에 따라 Main 서비스로 접근할 수 있는 URL을 출력합니다.
  # 기본 사용자 정보는 ID: admin, PW: brique_admin 입니다.
  ==> BA is installed completely. You can access BA at http://127.0.0.1:8080 with default username/password: admin/brique_admin
  ```

  


------

  

##### STEP 4 : UI 접속 및 동작 확인

크롬 브라우져를 통행 BRIQUE Analytic  UI에 접속

- url : http://localhost:8080 

- 초기 ID : admin

- 초기 Password : brique_admin

  

------

##### Trouble  Shoot

###### 설치 상태에서 Service Port를 808x -> 908x로 변경하여 재 설치 하고자 할 때 
- 재 설치 명령어도 동일 install을 사용한다.
``` shell
# 설치 와 동일한 명령어로 재 설치 진행 
[brique@localhost bainstall]$ sudo ba install /mnt/E_DRIVE/bainstall
Installing BRIQUE Analytics
Data Directory: /mnt/E_DRIVE/bainstall
> You are running installer under root.
You are running an instance of BA. You have to stop and remove this instance first. Do you want to continue? (y/n)
Error response from daemon: This node is not a swarm manager. Use "docker swarm init" or "docker swarm join" to connect this node to swarm and try again.
Error response from daemon: This node is not a swarm manager. Use "docker swarm init" or "docker swarm join" to connect this node to swarm and try again.
Error response from daemon: This node is not a swarm manager. Use "docker swarm init" or "docker swarm join" to connect this node to swarm and try again.
postgres13
postgres13
Error: No such network: ba-eco_nw
Error: No such network: ba-prod_nw
Error response from daemon: This node is not part of a swarm
Do you want to uninstall docker? (press y to accept) #n 입력
Do you want to uninstall wget? (press y to accept)  #n 입력
Do you want to remove all BA data? (press y to accept) #y 입력

Do you want to remove BA database data? (press y to accept) #y 입력
Removed BA completely. For more information, please visit https://ba.brique.kr/.
> Environment variables for BA were found. Looks like you already have installed BA, below are the parameters which were used in previous installation.
CUR_HOST_IP=127.0.0.1
CUR_HOST_NAME=localhost.localdomain
CUR_USER=root
CUR_GROUP=root
BA_HOME=/opt/ba
PORT_POSTGRES=5432
PORT_REDIS=6379
PORT_KAFDROP=9000
PORT_PREFIX=808
PORT_MAIN=8080
PORT_PLATFORM=8081
PORT_AUTH=8082
PORT_ADMIN=8083
PORT_BATCH=8084
POSTGRES_USER=ba210
POSTGRES_PASS=ba210
REDIS_PASS=ba210
BA_DATA_URL=https://ba.brique.kr/file/installer/v210r1/
BA_DATA_FILE=ba-v210.tar.gz
DOCKER_IMAGE_POSTGRES=brique/ba-eco-postgres13:v2.1.0-r1
REDIS_TOKEN_BATCH=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJjcmVfdXNlciI6IlNZU1RFTSIsImlzcyI6ImJyaXF1ZSIsImlkIjoiYmF0Y2giLCJyb2xlX2NkIjoiUl9NU1QiLCJ0eXBlIjoib3V0IiwiY3JlX2R0IjoxNjI3NTU0MTk5Njc0fQ.VGhKXbf7jaIGi_TwZXOtZjOdAUsIt-QW6Ttt3TF-Io4
REDIS_TOKEN_PLATFORM=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJjcmVfdXNlciI6IlNZU1RFTSIsImlzcyI6ImJyaXF1ZSIsImlkIjoicGxhdGZvcm0iLCJyb2xlX2NkIjoiUl9NU1QiLCJ0eXBlIjoib3V0IiwiY3JlX2R0IjoxNjI3NTU0MjM3MTQxfQ.tR8o9nwzwfQtTTNDJacn3l1V93p6TmKc3gmFa2ifQLE
PYTHON_36_DATA_FILE=python36.tar.gz
R360_DATA_FILE=r360.tar.gz
BA_BASIC_LIB_FILE=library_basic.tar.gz
PYTHON_36_PACKAGE_FILE=python36-package-full.tar.gz
R360_PACKAGE_FILE=r360-package-full.tar.gz

> Do you want to re-use above parameters? (press y to use them again) #n 입력

[Step 1] Checking supported OS: Supported OS
[Step 2] Check internet connection: You are online.
> BA data tarballs were found. Proceed to offline install? (y/n) # offline 설치일 경우 y 입력
Proceeding to offline installation.
[Step 3] Installing necessary packages:
> To run BA, we need to install these packages: curl, wget, docker.
>> Checking curl status: Installed.
>> Checking wget status: Installed.
>> Checking docker status: Installed.
>>> Verifying docker service can be started..
>>> Docker service is started completely.
[Step 4] Starting swarm mode in docker
> Initializing swarm mode:
Swarm initialized: current node (53ezww5689fq249ky9gm7q8zu) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-10nnaw8lkyu63yovlplhkwkvncdv6k7qxgliiz4tl345lx7m41-0pa2t9qovgxkrcuq07el9drxu 192.168.0.27:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.

>> Done
> Creating docker network ba-eco_nw...
ox38an703mhw5xw4q4ha5yq5l
>> Done
> Creating docker network ba-prod_nw...
fyn6in0cbqwjfh38nvyepp0sc
>> Done
[Step 5] Installing BA
> 5.1. Getting current user, host information
>> Current user: root
>> Current user group: root
>> Current host IP address: 127.0.0.1
>> Current hostname:  localhost.localdomain
> 5.2. Enter directory path where you want to install Brique Analytics. (default: /opt/ba)
>> Directory:
>> Installing Brique Analytics at default directory: /opt/ba
>> BA Directory: /opt/ba
>>> Creating BA Directory. May need to input user password.
sending incremental file list
ba-v210.tar.gz
        517.23M 100%  126.93MB/s    0:00:03 (xfr#1, to-chk=5/6)
> 5.3. BA configuration
>> Postgresql port (default: 5432):
>> Postgresql username (default: ba210 - We strongly recommend you to use only lowercase alphabets and numbers):
>> Postgresql password (default: ba210):
>> Redis password (default: ba210):
>> Redis port (default: 6379):
>> Kafdrop (Kafka Manager UI) port (default: 9000):

### 808x Port를 908x로 사용하고자 하는 경우 아래 처럼 Port를 별도로 지정
>> Port prefix for BA (For example, platform port: 8081, main: 8080, auth: 8082 => port prefix is 808) (default: 808): 908  
>> Port for BA main (BA Main Server with Web UI, must be consistent with defined port prefix) (default: 8080): 9080
>> Port for BA platform (BA Core Engine, must be consistent with defined port prefix) (default: 8081): 9081
>> Port for BA auth (Authentication Server for BA, must be consistent with defined port prefix) (default: 8082): 9082
>> Port for BA admin (Administrator Page for BA, must be consistent with defined port prefix) (default: 8083): 9083
>> Port for BA batch (Background Job Manager for BA, must be consistent with defined port prefix) (default: 8084): 9084

>> BA configuration summary:
        Postgresql port: 5432
        Postgresql user: ba210
        Postgresql pass: ba210
        Redis port: 6379
        Kafdrop port: 9000
        BA prefix port: 908
        BA main port: 9080
        BA platform port: 9081
        BA auth port: 9082
        BA admin port: 9083
        BA batch port: 9084
>> Entering to /opt/ba
> 5.4. Checking BA data file
ls: cannot access 'data/api': No such file or directory
>> Extracting ba-v210.tar.gz file:   [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]
> 5.5. Updating role for current node inside docker swarm
> 5.6. Creating Postgresql docker container
>> Postgresql data already exists. Do you want to reuse this data? (y/n)
>> Starting Postgres docker container
Loaded image: brique/ba-eco-postgres13:v2.1.0-r1
e0dfd5685fde2ee7f9214eab06bcdcdae59c598470372fa59a6ad3e847001181
>>> Initializing Postgres docker container....
>>> Postgres docker container is ready to use.
>> Creating Postgres database schema
CREATE ROLE

...

> 5.7. Creating Redis docker container
>> Redis data already exists. Do you want to reuse this data? (y/n) #n 입력
>> Deploying redis stack
Loaded image: brique/ba-redis-slave:v1.3.1-a-20102215
Creating service ba-eco-redis_redis
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
OK
OK
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
OK
OK

> 5.8. Creating Kafka docker container
>> Deploying kafka stack
Loaded image: brique/ba-eco-zookeeper:v1.3.1-a-20102215
Loaded image: brique/ba-eco-kafka:v1.3.1-a-20102215
Loaded image ID: sha256:5b5ea1807970a300ff2a9c52119a42e2ea678a5985f62e439680115bf7bc54bc
Creating service ba-eco-zk_kafka1
Creating service ba-eco-zk_kafdrop
Creating service ba-eco-zk_zoo1
ba-eco-zk_kafka1.0.clwwqmbk7svr@localhost.localdomain    |  08:22:45.73
ba-eco-zk_kafka1.0.clwwqmbk7svr@localhost.localdomain    |  08:22:45.73 Welcome to the Bitnami kafka container
ba-eco-zk_kafka1.0.clwwqmbk7svr@localhost.localdomain    |  08:22:45.73 Subscribe to project updates by watching https://github.com/bitnami/bitnami-docker-kafka
ba-eco-zk_kafka1.0.clwwqmbk7svr@localhost.localdomain    |  08:22:45.73 Submit issues and feature requests at https://github.com/bitnami/bitnami-docker-kafka/issues
ba-eco-zk_kafka1.0.clwwqmbk7svr@localhost.localdomain    |  08:22:45.73
ba-eco-zk_kafka1.0.clwwqmbk7svr@localhost.localdomain    |  08:22:45.73 INFO  ==> ** Starting Kafka setup **
ba-eco-zk_kafka1.0.clwwqmbk7svr@localhost.localdomain    |  08:22:45.78 WARN  ==> You set the environment variable 
...
>>> Kafka stack is created completely.

> 5.9. Creating BA (Platform, API, UI) docker container
ls: cannot access 'data/interpreter/exec/python36': No such file or directory
>> Extracting python36.tar.gz file:   [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]
ls: cannot access 'data/interpreter/exec/r360': No such file or directory
>> Extracting r360.tar.gz file:   [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]
>> Deploying BA stack
Loaded image: brique/ba-api:v2.1.0-r1
Loaded image: brique/ba-app-http-actor:v2.1.0-r1
Loaded image: brique/ba-app-workflow-actor:v2.1.0-r1
Loaded image: brique/ba-app-result-actor:v2.1.0-r1
Loaded image: brique/ba-app-database-actor:v2.1.0-r1
Loaded image: brique/ba-python-36-cpu-slim:v2.0.1-a
Loaded image: brique/ba-python-36-download:v2.0.1-a
Loaded image: brique/ba-r-360-slim:v2.0.1-a
Creating service ba-prod_r360
Creating service ba-prod_python36download
Creating service ba-prod_platform-database
Creating service ba-prod_python36cpu
Creating service ba-prod_main
Creating service ba-prod_batch
Creating service ba-prod_platform-workflow
Creating service ba-prod_platform-result
Creating service ba-prod_platform-http
Creating service ba-prod_auth
Creating service ba-prod_admin
>>> [1/11] main... -> Done
>>> [2/11] auth... -> Done
>>> [3/11] admin... -> Done
>>> [4/11] batch... -> Done
>>> [5/11] platform-http... -> Done
>>> [6/11] platform-database... -> Done
>>> [7/11] platform-result... -> Done
>>> [8/11] platform-workflow... -> Done
>>> [9/11] python36cpu... -> Done
>>> [10/11] r360... -> Done
>>> [11/11] python36download... -> Done
> 5.10. Checking BA services status
>> BA api is booting up...
>> BA api is started completely.
>> Import basic libraries
>>> Extracting library_basic.tar.gz file:   [>>>>]
>>> Importing tmp/library_basic/lib_exp_20211125104952781.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  3755    0    63  100  3692    151   8853 --:--:-- --:--:-- --:--:--  9004
{"status_code":401,"message":"LOGGED IN FAILED. INVALID TOKEN"}
>>> Importing tmp/library_basic/lib_exp_20211125105014040.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 20220    0    63  100 20157    969   302k --:--:-- --:--:-- --:--:--  303k
{"status_code":401,"message":"LOGGED IN FAILED. INVALID TOKEN"}
>>> Importing tmp/library_basic/lib_exp_20211125105022307.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  6051    0    63  100  5988    954  90727 --:--:-- --:--:-- --:--:-- 91681
{"status_code":401,"message":"LOGGED IN FAILED. INVALID TOKEN"}
>>> Importing tmp/library_basic/lib_exp_20211125105024189.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 11822    0    63  100 11759    741   135k --:--:-- --:--:-- --:--:--  135k
{"status_code":401,"message":"LOGGED IN FAILED. INVALID TOKEN"}
>> Do you want to install the basic python packages? (y/n)  #y 입력
>> Extracting python36-package-full.tar.gz file:   [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]
>> Do you want to install the basic R packages? (y/n) #y입력
>> Extracting r360-package-full.tar.gz file:   [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]
>> BA platform is booting up...
>> BA platform is started completely.


==> BA is installed completely. You can access BA at http://127.0.0.1:9080 with default username/password: admin/brique_admin
[brique@localhost bainstall]$

```


