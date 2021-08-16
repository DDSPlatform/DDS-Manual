#### BRIQUE Analytics 설치 가이드 (개인 PC용)

본 문서는 BRIQUE Analytics를 개인 PC 환경에서 독립 서버로 구동하기 위한 설치 방법을 포함하고 있습니다.

-----------------------

#### 시스템 요구사항

##### 운영체제 (64비트)

- Linux RHEL 계열
  - CentOS 7 / 8
  - Fedora 32 이상
  - RedHat 7 이상
- Linux Debian 계열
  - Debian Buster 10 (Stable) 이상
  - Ubuntu 18.04, 20.04
- Windows
  - Windows 10 64-bit Home, Pro, Enterprise, Education (Build 18362 이상)

##### 메모리

- 16 GB 이상

##### CPU

- x64 4 코어 이상

##### Storage

- 100 GB 이상

##### 추가 패키지

- 인터넷 연결이 지원되지 않는 환경인 경우 다음 소프트웨어들이 미리 설치되어 있어야 합니다.
  - Linux: `curl`  `wget`  `docker`
  - Windows: `Docker Desktop`  `WSL 2 (Ubuntu 20.04 Backend)`

----------------------------------------------

#### 설치

##### Linux 환경에서 설치

- 홈페이지의 다운로드 링크 혹은 다음 URL에서 설치환경에 맞는 패키지를 다운로드 합니다.

  - DEB 패키지: https://ba.brique.kr/file/installer/v210r1/ba_2.1.0-r1-1_amd64.deb
  - RPM 패키지: https://ba.brique.kr/file/installer/v210r1/ba-2.1.0-r1.noarch.rpm

- 다운로드 받은 패키지가 있는 경로로 이동하여 패키지를 설치합니다.

  - DEB 패키지

    ```shell
    $ dpkg -i ba_2.1.0-r1-1_amd64.deb
    ```

  - RPM 패키지

    ```shell
    $ yum localinstall -y ba-2.1.0-r1.noarch.rpm
    ```



- 설치할 대상 환경이 인터넷 연결을 지원하지 않는 경우, 다음 파일들을 추가로 다운로드하여 설치환경에 수동으로 업로드 해야 합니다.
  - https://ba.brique.kr/file/installer/v210r1/ba-v210.tar.gz # 어플리케이션 데이터 파일
  - https://ba.brique.kr/file/installer/v210r1/python36.tar.gz # Python 3.6 설치 파일
  - https://ba.brique.kr/file/installer/v210r1/python36-package-full.tar.gz # Python 3.6 패키지 파일
  - https://ba.brique.kr/file/installer/v210r1/r360.tar.gz # R 3.6.0 설치 파일
  - https://ba.brique.kr/file/installer/v210r1/r360-package-full.tar.gz # R 3.6.0 패키지 파일

  위 파일들은 설치 환경에서 ba install 명령어를 실행할 때 매개변수로 지정할 디렉토리 밑의 혹은 ba install 명령어를 실행할 작업 디렉토리 (Working Directory) 밑의 `datafile/` 디렉토리에 위치해야 합니다.

  - https://ba.brique.kr/file/installer/v210r1/docker-image/api.tar.gz # 어플리케이션 도커 이미지 파일
  - https://ba.brique.kr/file/installer/v210r1/docker-image/platform-http.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/platform-database.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/platform-workflow.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/platform-result.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/kafka.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/kafdrop.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/redis-slave.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/zoo.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/python36.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/python36download.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/r360-image.tar.gz

  위 파일들은 BA 어플리케이션을 실행할 Docker image로, Docker가 설치된 BA 설치 환경에서 다음과 같이 로드할 수 있습니다.

  ```shell
  $ docker image load --input=api.tar.gz ## api.tar.gz 아카이브 파일을 읽어들입니다.
  ```

  총 30 GB의 디스크 공간이 추가로 필요합니다.



- 패키지가 설치되었으면 다음 명령어로 BA 설치를 시작합니다.

  ```shell
  $ ba install
  ```

  오프라인인 경우, 다음 명령어로 설치파일이 있는 디렉토리 ($INSTALL_DIR)를 매개변수로 지정해 줍니다.
  
  ```shell
  $ ba install /home/brique/ba
  ```

---------------------------------------

##### Windows 환경에서 설치

- 홈페이지의 다운로드 링크 혹은 다음 URL에서 패키지 `.zip` 파일을 다운로드 합니다.

  - Windows 설치파일: https://ba.brique.kr/file/installer/v210r1/ba-v210r1-win64-installer.zip

- 다운로드 받은 파일의 압축을 해제합니다.

- 설치할 대상 환경이 인터넷 연결을 지원하지 않는 경우, 다음 파일들을 추가로 다운로드하여 설치환경에 수동으로 업로드 해야 합니다.

  - https://ba.brique.kr/file/installer/v210r1/ba-v210.tar.gz # 어플리케이션 데이터 파일
  - https://ba.brique.kr/file/installer/v210r1/python36.tar.gz # Python 3.6 설치 파일
  - https://ba.brique.kr/file/installer/v210r1/python36-package-full.tar.gz # Python 3.6 패키지 파일
  - https://ba.brique.kr/file/installer/v210r1/r360.tar.gz # R 3.6.0 설치 파일
  - https://ba.brique.kr/file/installer/v210r1/r360-package-full.tar.gz # R 3.6.0 패키지 파일

  위 파일들은 설치 환경에서 `.\ba.ps1 install` 명령어를 실행할 때 매개변수로 지정할 디렉토리 밑의 혹은 명령어를 실행할 작업 디렉토리 (Working Directory) 밑의 `datafile/` 디렉토리에 위치해야 합니다.

  - https://ba.brique.kr/file/installer/v210r1/docker-image/api.tar.gz # 어플리케이션 도커 이미지 파일
  - https://ba.brique.kr/file/installer/v210r1/docker-image/platform-http.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/platform-database.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/platform-workflow.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/platform-result.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/kafka.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/kafdrop.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/redis-slave.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/zoo.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/python36.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/python36download.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/docker-image/r360-image.tar.gz

  위 파일들은 BA 어플리케이션을 실행할 Docker image로, Docker가 설치된 BA 설치 환경에서 다음과 같이 로드할 수 있습니다.

  ```powershell
  docker image load --input=api.tar.gz ## api.tar.gz 아카이브 파일을 읽어들입니다.
  ```

  총 30 GB의 디스크 공간이 추가로 필요합니다.



- 압축을 해제하였으면 관리자 권한으로 Windows Powershell을 실행합니다.

![img](./img/01-01-설치매뉴얼_01_StandAlone_01_PowerShell.png)

- Powershell 창에서 다음 명령어를 실행합니다.

```Powershell
Set-ExecutionPolicy unrestricted
```



- 패키지 `.zip` 파일을 압축해제 한 경로로 이동해, `ba.ps1` 스크립트를 다음 명령어와 같이 실행합니다.

```powershell
.\ba.ps1 install 
```

​		또는 다음 명령어와 같이 설치 경로 ($INSTALL_DIR)를 매개변수로 지정할 수 있습니다.

```powershell
.\ba.ps1 install C:\Users\Me\ba
```

-----------------------------------

##### 설치 진행

설치가 시작되면 다음과 같이 프롬프트 메세지가 출력됩니다. 설치환경에 맞게 매개변수 등을 설정해줍니다.

```shell
## 설치파일 디렉토리를 매개변수로 받은 경우 출력합니다.
## 설치에 필요한 .tar.gz 압축파일들이 위치한 경로이며 BA를 설치하는 경로 $BA_HOME은 별도 지정합니다.
Install Directory: /home/brique/Downloads

## Root 권한으로 installer를 실행하는 경우 알림 메세지를 출력합니다.
> You are running installer under root.

## BA가 이미 설치되어 동작중인 환경이면 다음과 같이 중지 후 재설치 여부를 묻는 메세지가 출력됩니다.
You are running an instance of BA. You have to stop and remove this instance first. Do you want to continue? (press y to accept) # y를 입력하면 동작중인 BA를 중지하고 재설치를 진행합니다.

## 마찬가지로 BA가 사용하는 환경 매개변수가 이미 존재하는 경우 다음과 같이 재사용 여부를 묻는 메세지가 출력됩니다.
> Environment variables for BA were found. Looks like you already have installed BA, below are the parameters which were used in previous installation.

> Do you want to re-use above parameters? (press y to use them again) 
# y를 입력하면 환경 매개변수를 재사용합니다.

## 설치환경이 BA에서 지원하는 운영체제인지 확인합니다.
[Step 1] Checking supported OS: 
Supported OS # 설치가 가능한 운영체제입니다.

## 인터넷 연결이 지원되는 환경인지 확인합니다.
[Step 2] Check internet connection: 
You are online. # 인터넷 연결이 지원되는 환경입니다.
You are offline. Checking data files in datafile directory. # 지원되지 않는 환경입니다.
## 인터넷 연결이 지원되지 않는 환경인 경우, $INSTALL_DIR 내부의 datafile 디렉토리를 검사하여 필요한 설치파일들이 있어야 설치를 진행할 수 있습니다.

## 필요한 소프트웨어 패키지들이 설치되어 있는지 확인합니다.
[Step 3] Installing necessary packages: 
> To run BA, we need to install these packages: curl, wget, docker.
>> Checking curl status: Installed. # curl 패키지가 설치되어 있습니다.
>> Checking wget status: Installed. # wget 패키지가 설치되어 있습니다.
>> Checking docker status: Installed. # docker 패키지가 설치되어 있습니다.

>>> Verifying docker service can be started. # Docker 데몬이 동작중인지 검사합니다.
>>> Docker service is started completely. # Docker 데몬이 실행중이며 설치를 진행할 수 있습니다.

## 호스트를 Docker Swarm Node로 초기화합니다.
[Step 4] Starting swarm mode in docker 

## BA를 설치합니다.
[Step 5] Installing BA
# 사용자와 호스트 정보를 읽어들입니다.
> 5.1. Getting current user, host information 
>> Current user: brique
>> Current user group: brique
>> Current host IP address: 192.168.0.1
>> Current hostname: myHost
# BA를 설치할 경로를 확인합니다.
> 5.2. Enter directory path where you want to install Brique Analytics. (default: /opt/ba) 
# BA 설치경로 ($BA_HOME)는 기본적으로 /opt/ba로 세팅되어 있습니다. 
# Enter를 누르면 기본값인 /opt/ba에 BA를 설치합니다.
# 다른 경로에 설치하기를 원하는 경우 직접 경로를 입력합니다.

# 지정된 BA 설치 경로를 출력합니다.
>> BA Directory: /opt/ba

# $BA_HOME 디렉토리가 이미 존재하는 경우 해당 디렉토리를 재사용할 지 여부를 확인합니다.
>>> /opt/ba directory already exists. Do you want to reuse contents inside this directory? (y/n)
# y를 입력하면 해당 디렉토리의 내용을 그대로 사용합니다.
# n을 입력하면 해당 디렉토리를 삭제하고 데이터파일을 다운로드하거나 $INSTALL_DIR/datafile 에서 데이터를 가져옵니다.

# $BA_HOME 디렉토리가 없는 경우 생성합니다.
>>> Creating BA Directory. May need to input user password.

# BA 환경변수를 설정합니다.
# 값을 입력하지 않고 Enter를 누르면 기본값을 사용합니다.
> 5.3. BA configuration
>> Postgresql port (default: 5432): # BA의 사용자 데이터를 관리할 Postgres DB의 포트번호입니다.
>> Postgresql username (default: ba210 - We strongly recommend you to use only lowercase alphabets and numbers): # Postgres DB에서 사용할 사용자 이름입니다. 영문 소문자 알파벳과 숫자만을 사용하기를 권장합니다.
>> Postgresql password (default: ba210): # Postgres DB에서 사용할 사용자 비밀번호입니다.
>> Redis password (default: ba210): # BA 실행 데이터를 관리할 Redis DB의 비밀번호입니다.
>> Redis port (default: 6379): # Redis DB의 포트번호입니다.
>> Kafdrop (Kafka Manager UI) port (default: 9000): # Kafdrop의 포트번호입니다.
>> Port prefix for BA (For example, platform port: 8081, main: 8080, auth: 8082 => port prefix is 808) (default: 808): # BA 서비스의 포트번호 접두사를 설정합니다.
>> Port for BA main (BA Main Server with Web UI, must be consistent with defined port prefix) (default: 8080): # BA 메인 UI의 포트번호입니다.
>> Port for BA platform (BA Core Engine, must be consistent with defined port prefix) (default: 8081): # BA Platform의 포트번호입니다.
>> Port for BA auth (Authentication Server for BA, must be consistent with defined port prefix) (default: 8082): # BA 인증서비스의 포트번호입니다.
>> Port for BA admin (Administrator Page for BA, must be consistent with defined port prefix) (default: 8083): # BA 관리자 페이지의 포트번호입니다.
>> Port for BA batch (Background Job Manager for BA, must be consistent with defined port prefix) (default: 8084): # BA 배치 페이지의 포트번호입니다.

# 설정한 BA 환경변수들을 출력합니다.
>> BA configuration summary: 
	Postgresql port: 5432
	Postgresql user: ba210
	Portgresql pass: ba210
	Redis port: 6379
	Kafdrop port: 9000
	BA prefix port: 808
	BA main port: 8080
	BA platform port: 8081
	BA auth port: 8082
	BA admin port: 8083
	BA batch port: 8084

# BA 설치경로로 이동합니다.
>> Entering to /opt/ba

# 설치경로를 확인합니다.
> 5.4. Checking BA data file
# 설치경로에 어플리케이션 데이터가 이미 있는 경우 재사용할 지 여부를 확인합니다.
>> BA data directory already exists. Do you want to reuse this data? (y/n) 
# 설치경로에 어플리케이션 데이터 아카이브 파일이 이미 있는 경우 재사용할 지 여부를 확인합니다.
>> ba-v210.tar.gz data file already exists. Do you want to reuse this data? (y/n)
# 설치경로에 어플리케이션 데이터 아카이브 파일 (ba-v210.tar.gz)이 없는 경우 다운로드합니다.
>> Downloading BA data file from https://ba.brique.kr/file/installer/v210r1/ba-v210.tar.gz to /opt/ba/tmp 

# 어플리케이션 데이터를 재사용 하지 않는 경우 다운로드 한 혹은 이미 존재하는 .tar.gz 파일을 사용합니다.
# 설치경로 $BA_HOME 밑에 data/ 디렉토리와 badata/ 디렉토리가 생성됩니다.
>> Extracting $BA_DATA_FILE file: [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>] 

# 현재 노드의 Docker Node role을 업데이트합니다.
> 5.5. Updating role for current node inside docker swarm 

# Postgres DBMS 도커 컨테이너를 구동합니다.
> 5.6. Creating Postgresql docker container
# $BA_HOME 경로 밑 data/postgresql/ 디렉토리가 이미 존재하는 경우 데이터를 재사용할 지 확인합니다.
>> Postgresql data is existed. Do you want to use these data again? (press y to accept)
# n을 입력하면 초기화된 상태의 BA 데이터베이스를 새로 생성합니다.

>> Starting Postgres docker container
>>> Initializing Postgres docker container...
>>> Postgres docker container is ready to use.

# 데이터가 없는 경우 데이터베이스를 초기화하고 스키마를 새로 생성합니다.
>> Creating Postgres database schema

# Redis 서비스를 구동합니다.
> 5.7. Creating Redis docker container 
# $BA_HOME 경로 밑 data/eco/redis/appendonly.aof 파일이 이미 존재하는 경우 데이터를 재사용할 지 확인합니다.
>> Redis data already exists. Do you want to reuse this data? (y/n)
>> Deploying redis stack
>>> Redis stack is still creating...
>>> Redis stack is created completely.

# Kafka 스택 (Kafka, Zookeeper, Kafdrop)을 구동합니다.
> 5.8. Creating Kafka docker container
>> Deploying kafka stack
>>> Kafka stack is still creating...
>>> Kafka stack is created completely.

# BA 스택 (Main, Platform, Auth, Admin, Batch 및 인터프리터)을 구동합니다.
> 5.9. Creating BA (Platform, API, UI) docker container
# $BA_HOME 경로 밑 data/interpreter/exec/python36 디렉토리가 이미 존재하는 경우 해당 데이터를 재사용할 지 확인합니다.
>> Python 3.6 data already exists. Do you want to reuse this data? (y/n) 
# 없거나 재사용하지 않는 경우 다운로드 합니다.
# 인터넷 연결이 없는 환경인 경우 셋업된 datafile/ 디렉토리 내의 아카이브를 이용합니다.
>> Downloading Python 3.6 data from https://ba.brique.kr/file/installer/v210r1/python36.tar.gz to /opt/ba/tmp 
# $BA_HOME 밑의 data/interpreter/exec/ 경로에 압축을 해제합니다.
>> Extracting $PYTHON_36_DATA_FILE file:   [>>>>>>>>>>>>>>>>>>>>>>>>>>>]

# $BA_HOME 경로 밑 data/interpreter/exec/r360 디렉토리가 이미 존재하는 경우 해당 데이터를 재사용할 지 확인합니다.
>> R 3.6.0 data already exists. Do you want to reuse this data? (y/n)
# 없거나 재사용하지 않는 경우 다운로드 합니다.
# 인터넷 연결이 없는 환경인 경우 셋업된 datafile/ 디렉토리 내의 아카이브를 이용합니다.
>> Downloading R 3.6.0 data from https://ba.brique.kr/file/installer/v210r1/r360.tar.gz to /opt/ba/tmp 
# $BA_HOME 밑의 data/interpreter/exec/ 경로에 압축을 해제합니다.
>> Extracting $R360_DATA_FILE file:   [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>] 

# Docker compose 파일을 이용해서 BA 서비스들을 배포합니다.
>> Deploying BA stack
>>> [1/11] ba-prod_main... -> Done
>>> [2/11] ba-prod_auth... -> Done
>>> [3/11] ba-prod_admin... -> Done
>>> [4/11] ba-prod_batch... -> Done
>>> [5/11] ba-prod_platform-http... -> Done
>>> [6/11] ba-prod_platform-database... -> Done
>>> [7/11] ba-prod_platform-result... -> Done
>>> [8/11] ba-prod_platform-workflow... -> Done
>>> [9/11] ba-prod_python36cpu... -> Done
>>> [10/11] ba-prod_r360... -> Done
>>> [11/11] ba-prod_python36download... -> Done

# BA 서비스 상태를 체크합니다.
> 5.10. Checking BA services status
# API 서비스의 상태를 체크합니다.
>> BA api is booting up...
>> BA api is started completely.

# Python에서 사용할 기본 패키지들을 설치할 지 여부를 확인합니다.
>> Do you want to install the basic python packages? (y/n)
# 인터넷 연결이 있는 환경인 경우 다운로드 합니다.
>> Downloading Python 3.6 package data from $BA_DATA_URL$PYTHON_36_PACKAGE_FILE to $BA_HOME/tmp
# 패키지들을 data/interpreter/exec/ 경로에 압축 해제합니다.
>> Extracting $PYTHON_36_PACKAGE_FILE file:   [>>>>>>>>>>>>>>>>>>>>>]

# R에서 사용할 기본 패키지들을 설치할 지 여부를 확인합니다.
>> Do you want to install the basic R packages? (y/n)
# 인터넷 연결이 있는 환경인 경우 다운로드 합니다.
>> Downloading R 3.6.0 package data from $BA_DATA_URL$R360_PACKAGE_FILE to $BA_HOME/tmp
# 패키지들을 data/interpreter/exec/ 경로에 압축 해제합니다.
>> Extracting $R360_PACKAGE_FILE file:   [>>>>>>>>>>>>>>>>>>>>>]

# Platform 서비스의 상태를 체크합니다.
>> BA platform is booting up...
>> BA platform is started completely.
# 설치가 완료되었습니다. 설정한 환경변수에 따라 Main 서비스로 접근할 수 있는 URL을 출력합니다.
# 기본 사용자 정보는 ID: admin, PW: brique_admin 입니다.
==> BA is installed completely. You can access BA at http://192.168.0.1:8080 with default username/password: admin/brique_admin
```

