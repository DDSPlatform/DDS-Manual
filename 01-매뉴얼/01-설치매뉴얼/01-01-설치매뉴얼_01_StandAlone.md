#### BRIQUE Analytics 설치 가이드 (개인 PC용)

본 문서는 BRIQUE Analytics를 개인 PC 환경에서 독립 서버로 구동하기 위한 설치 방법을 포함하고 있습니다



------

#### 시스템 요구사항



##### 운영체제 (64비트)

- RHEL 계열
  - CentOS 7
  - CentOS 8
  - Fedora 32
  - RedHat 7 이상
- Ubuntu 계열
  - Ubuntu 18.04
  - Ubuntu 20.04
- Debian 계열
  - Buster 10 (Stable)
- Windows 계열
  - Windows 10 64bit Home
  - Windows 10 64bit Pro
  - Windows 10 64bit Enterprise
  - Windows 10 64bit Education (Build 18362 이상)



##### H/W 사양

- Memory

  16 GB 이상

- CPU

  x64 CPU 4 코어 이상 (Intel, AMD)

- HDD

  SSD 100 GB 이상



##### S/W (Required)

인터넷이 제공되지 않는 환경에서는 다음의 소프트웨어 패키지들이 설치되어 있어야 합니다



- Linux

  - `curl, wget, docker` 

    (참고: [Install Docker Engine](https://docs.docker.com/engine/install/#server), `Server` 섹션)

- Windows

  - `Docker desktop, enabled WSL 2`  그리고 `Ubuntu 20.04 WSL backend`

    (참고: [Install Docker Desktop on Windows](https://docs.docker.com/docker-for-windows/install/))




------

#### Linux 환경에 설치



다음 URL로부터 BRIQUE Analytics 설치 파일을 다운로드 합니다

```sh
http://ba.brique.kr/file/installer/v130r1/ba-v130r1-linux-installer.tar.gz
```



터미널에서 `tar`를 이용해 압축을 해제합니다

```shell
$ tar -zxvf ba-v130r1-linux-installer.tar.gz
```



인터넷이 제공되지 않는 환경에서는 다음 작업이 필요합니다 (30 GB의 디스크 공간이 추가로 필요합니다)

```shell
## 압축을 해제한 경로에서 서브 디렉토리 생성
$ mkdir -p datafile/imgs 

## 설치에 필요한 파일들을 다운로드하여 설치할 호스트의 datafile 디렉토리에 복사
$ http://ba.brique.kr/file/installer/v130r1/ba-v131.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/library_basic.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/python36-package-full.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/python36.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/r360-package-full.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/r360.tar.gz

## 설치에 필요한 파일들을 다운로드하여 설치할 호스트의 datafile/imgs 디렉토리에 복사
$ http://ba.brique.kr/file/installer/v130r1/docker-image/api.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/docker-image/batch-api.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/docker-image/kafdrop.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/docker-image/kafka.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/docker-image/oracle12c.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/docker-image/platform-cpu.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/docker-image/python36-cpu.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/docker-image/python36-download.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/docker-image/r360.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/docker-image/redis-slave.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/docker-image/ui.tar.gz
$ http://ba.brique.kr/file/installer/v130r1/docker-image/zoo.tar.gz
```



`init.sh` 스크립트 파일을 실행하여 설치를 시작합니다

```shell
$ sudo chmod 755 init.sh
$ ./init.sh
```



단계별 설치 과정

```shell
## init.sh를 실행한 경로를 표시
Install Directory: /home/brique/Documents

## Root 권한으로 실행한 경우
> You are running installer under root.

## BA가 이미 동작중인 호스트인 경우
You are already running an instance of BA. You have to stop and remove this instance first. Do you want to continue? (press y to accept) 
## y: 동작중인 BA를 중지하고 데이터를 삭제

## BA에서 사용하는 환경변수가 시스템에 이미 있는 경우
> ba-env already exists. Looks like you have already installed BA, these are the configuration parameters used in the previous installation.

> Do you want to re-use these above parameters? (press y to use them again)?
## y: 환경변수를 재사용

## 운영체제 확인
[Step 1] Checking supported OS: 
## BA가 지원하는 운영체제인 경우
Supported OS 
## BA에서 지원되지 않는 운영체제인 경우
Your OS is not supported yet. We only supported RHEL (CentOS, RedHat, Fedora) and Ubuntu. Exiting.

## 인터넷 연결 확인
[Step 2] Check internet connection: 
## 인터넷 연결이 있는 경우
You are online.
## 인터넷에 연결할 수 없는 환경인 경우
You are offline. Checking data files are existes in datafile directory. # If your machine cannot connect to internet

## 필수 패키지 설치
[Step 3] Installing necessary packages: 
> To run BA, the following packages are required: curl, wget, docker.
## 호스트에 curl 패키지가 이미 있는 경우
>> Checking curl status: Installed.
## 호스트에 wget 패키지가 이미 있는 경우
>> Checking wget status: Installed.
## 호스트에 docker 패키지가 이미 있는 경우
>> Checking docker status: Installed.

>>> Verifying docker service is available.
>>> Docker service is started completely.

## 도커 스웜 활성화
[Step 4] Starting swarm mode in docker 

## BA 설치
[Step 5] Installing BA
## 현재 사용자와 호스트 정보를 확인
> 5.1. Getting current user, host information
## BA를 설치할 경로 입력 (입력값이 없으면 /opt/ba 디렉토리에 설치함)
> 5.2. Which directory do you want to install BA? (default: /opt/ba)

## /opt/ba 디렉토리가 이미 존재하는 경우
>>> /opt/ba directory already exists. Do you want to RE-USE contents inside this directory? (press y to accept)
## y: 존재하는 데이터를 재사용함

## BA 구성
> 5.3. BA configuration
>> Oracle port (default: 1521) # Oracle DBMS에서 사용할 포트번호 지정
>> Oracle username (default: BA131) # Oracle 사용자 이름 지정
>> Oracle password (default: BA131): # Oracle 비밀번호 지정
>> Redis password (default: ba131): # Redis 비밀번호 지정
>> Redis port (default: 6379): # Redis 포트번호 지정
>> Kafdrop (Kafka Manager UI) port (default: 9000): # Kafdrop 포트번호 지정
>> Port prefix for BA (For example, platform port: 8081, api: 8082, ui: 8080 => port prefix is 808) (default: 808): # BA 서비스들이 사용할 포트 접두사 (Prefix) 지정
>> Port for BA platform (BA Core Engine, need same with defined port prefix) (default: 8081): # BA Platform 포트번호 지정
>> Port for BA api (BA backend REST API, need same with defined port prefix) (default: 8082): # BA API 포트번호 지정
>> Port for BA ui (BA UI, need same with defined port prefix) (default: 8080): # BA UI 포트번호 지정
>> Port for BA batch (For manage scheduled job in BA, need same with defined port prefix) (default: 8084): # BA Batch 포트번호 지정

## 구성정보 요약
>> BA configuration summary:

>> Entering to /opt/ba: Go to ba directory

## BA 데이터파일 확인
> 5.4. Checking BA data file
## /opt/ba/data 디렉토리가 이미 존재하는 경우
>> BA data directory already exists. Do you want to use these data again? (press y to accept)
## y: 존재하는 데이터를 재사용함

## 기본 데이터파일이 없는 경우 인터넷에서 다운로드
>> Downloading BA data file from ... to /opt/ba/tmp 

## 압축 해제
>> Extracting $BA_DATA_FILE file: [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]

## 도커 스웜의 노드 Role 업데이트
> 5.5. Updating role for current node inside docker swarm 

## Oracle DBMS 설치
> 5.6. Creating Oracle docker container
## /opt/ba/data/oracle12c 디렉토리가 이미 존재하는 경우
>> Oracle data is existed. Do you want to use these data again? (press y to accept)
## y: 존재하는 데이터베이스를 재사용함

>> Starting Oracle docker container
>>> Oracle docker container is still creating.........
>>> Oracle docker container is created completely.

## 데이터 없이 처음 설치하는 경우
>> Creating Oracle database schema

## Redis 설치
> 5.7. Creating Redis docker container 
## Redis 데이터파일이 이미 존재하는 경우 (/opt/ba/data/ba/config/swarm/redis/appendonly.aof)
>> Redis data is existed. Do you want to use these data again? (press y to accept)
## y: 존재하는 Redis 데이터를 불러옴

>> Deploying redis stack
>>> Redis stack is still creating...
>>> Redis stack is created completely.

## Kafka, Zookeeper, Kafdrop 스택 설치
> 5.8. Creating Kafka docker container 
>> Deploying kafka stack
>>> Kafka stack is still creating...
>>> Kafka stack is created completely.

## BA 설치
> 5.9. Creating BA (Platform, API, UI) docker container
## Python 3.6 인터프리터 데이터가 존재하는 경우 (/opt/ba/data/ba/interpreter/exec/python36)
>> Python 3.6 data is existed. Do you want to use these data again? (press y to accept) # 
## y: 존재하는 인터프리터 데이터 재사용

## Python 3.6 인터프리터 데이터를 /opt/ba/tmp에 다운로드
>> Downloading Python 3.6 data from ... to /opt/ba/tmp

## 데이터를 /opt/ba/data/ba/interpreter/exec 경로에 압축 해제
>> Extracting $PYTHON_36_DATA_FILE file:   [>>>>>>>>>>>>>>>>>>>>>>>>>>>] 

## R 3.6.0 인터프리터 데이터가 존재하는 경우 (/opt/ba/data/ba/interpreter/exec/r360)
>> R 3.6.0 data is existed. Do you want to use these data again? (press y to accept)
## y: 존재하는 인터프리터 데이터 재사용

## R 3.6.0 인터프리터 데이터를 /opt/ba/tmp에 다운로드
>> Downloading R 3.6.0 data from ... to /opt/ba/tmp 

## 데이터를 /opt/ba/data/ba/interpreter/exec/ 경로에 압축 해제
>> Extracting $R360_DATA_FILE file:   [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>] 

## BA Stack 배포
>> Deploying BA stack
>>> [1/7] ba-v131_api... -> Done
>>> [2/7] ba-v131_platformcpu... -> Done
>>> [3/7] ba-v131_ui... -> Done
>>> [4/7] ba-v131_python36cpu... -> Done
>>> [5/7] ba-v131_r360... -> Done
>>> [6/7] ba-v131_python36download... -> Done
>>> [7/7] ba-v131_batch... -> Done

## BA 서비스 상태 확인
> 5.10. Checking BA services status
>> BA api is still starting...
>> BA api is started completely.
>> Import basic libraries

## BA에서 기본으로 제공하는 Python 패키지들 설치
>> Do you want to install list of python packages? (press y to accept)
## y: 설치

## Python 패키지들을 /opt/ba/tmp에 다운로드
>> Downloading Python 3.6 package data from ... to /opt/ba/tmp

## 패키지들을 /opt/ba/data/ba/interpreter/exec/ 경로에 압축 해제
>> Extracting $PYTHON_36_PACKAGE_FILE file:   [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>] 

## BA에서 기본으로 제공하는 R 패키지들 설치
>> Do you want to install list of R packages? (press y to accept)
## y: 설치

## R 패키지들을 /opt/ba/tmp에 다운로드
>> Downloading R 3.6.0 package data from ... to /opt/ba/tmp

## 패키지들을 /opt/ba/data/ba/interpreter/exec/ 경로에 압축 해제
>> Extracting $R_360_PACKAGE_FILE file:   [>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]

>> BA platform is still starting...
>> BA platform is started completely.

==> BA is installed completely. You can access BA ui at http://$CUR_HOST_IP:$PORT_UI with default username/password: admin/brique_admin

```



------

#### Windows 환경에 설치



BA 설치파일을 다음 URL에서 다운로드 합니다

```http
http://ba.brique.kr/file/installer/v130r1/ba-v130r1-win64-installer.zip
```



.zip 파일 압축 해제



인터넷이 제공되지 않는 환경에서는 다음 작업이 필요합니다 (30 GB의 디스크 공간이 추가로 필요합니다)

```powershell
## 설치에 필요한 파일들을 다운로드하여 ba-script\datafile 디렉토리에 복사
> http://ba.brique.kr/file/installer/v130r1/ba-v131.tar.gz
> http://ba.brique.kr/file/installer/v130r1/library_basic.tar.gz
> http://ba.brique.kr/file/installer/v130r1/python36-package-full.tar.gz
> http://ba.brique.kr/file/installer/v130r1/python36.tar.gz
> http://ba.brique.kr/file/installer/v130r1/r360-package-full.tar.gz
> http://ba.brique.kr/file/installer/v130r1/r360.tar.gz

## 설치에 필요한 파일들을 다운로드하여 ba-script\datafile\imgs 디렉토리에 복사
> http://ba.brique.kr/file/installer/v130r1/docker-image/api.tar.gz
> http://ba.brique.kr/file/installer/v130r1/docker-image/batch-api.tar.gz
> http://ba.brique.kr/file/installer/v130r1/docker-image/kafdrop.tar.gz
> http://ba.brique.kr/file/installer/v130r1/docker-image/kafka.tar.gz
> http://ba.brique.kr/file/installer/v130r1/docker-image/oracle12c.tar.gz
> http://ba.brique.kr/file/installer/v130r1/docker-image/platform-cpu.tar.gz
> http://ba.brique.kr/file/installer/v130r1/docker-image/python36-cpu.tar.gz
> http://ba.brique.kr/file/installer/v130r1/docker-image/python36-download.tar.gz
> http://ba.brique.kr/file/installer/v130r1/docker-image/r360.tar.gz
> http://ba.brique.kr/file/installer/v130r1/docker-image/redis-slave.tar.gz
> http://ba.brique.kr/file/installer/v130r1/docker-image/ui.tar.gz
> http://ba.brique.kr/file/installer/v130r1/docker-image/zoo.tar.gz
```



BA 설치를 위해서는 `Windows PowerShell` (버전 5 이상) 실행 권한이 필요합니다. 아래 명령어를 `PowerShell`에서 실행하여 `PS1` 스크립트를 실행할 권한을 부여합니다 (관리자 권한으로 실행한 상태여야 합니다)

```
Set-ExecutionPolicy unrestricted
```



`ba-setup.exe` 파일을 마우스 오른쪽 클릭 - 관리자 권한으로 실행하여 설치를 시작합니다.



------

#### BA 시작하기



설치가 완료되면, 다음과 같은 메세지가 터미널에 출력됩니다. <IP> 는 설치한 호스트의 IP 주소, <PORT> 는 BA UI에 접속할 수 있는 포트번호가 출력됩니다

```sh
==> BA is installed completely. You can access BA ui at http://<IP>:<PORT> with default username/password: admin/brique_admin
```



웹 브라우저를 열고 (`Chromium` 엔진 기반의 브라우저들 - Google Chrome, MS Edge 등 - 을 사용하시길 권장합니다), 터미널에서 출력된 IP 주소와 포트번호로 접속하여 BRIQUE Analytics를 사용하실 수 있습니다



##### 리눅스 명령어

터미널에서 아래 명령어들을 실행할 수 있습니다.

- `ba start`: BRIQUE Analytics 서비스를 시작합니다
- `ba stop`: BRIQUE Analytics 서비스를 중지합니다
- `ba remove`: BRIQUE Analytics를 시스템에서 삭제합니다 (데이터 경로에 있는 모든 파일들이 삭제됩니다)
- `ba package python`: BRIQUE Analytics에서 기본적으로 제공하는 모든 Python 패키지들을 설치합니다
- `ba package r`: BRIQUE Analytics에서 기본적으로 제공하는 모든 R 패키지들을 설치합니다
- `ba version`: BRIQUE Analytics의 버전을 확인합니다 (최신 버전은 현재 v1.3.0-r1이며, UI 및 성능이 개선되고 버그가 수정된 v2.1.0-r1 이 2021년 7월에 공개될 예정입니다)
- `ba help`: Brique Analytics 도움말을 출력합니다



##### 윈도우즈 명령어

Shift 키를 누른 채로 `ba-setup.exe` 아이콘을 우클릭하시고, `관리자 권한으로 실행`을 클릭합니다. 터미널이 열리면 다음과 같은 메뉴가 출력됩니다

```
Which action do you want to do? (Default: 1)
[1] Install Brique Analytics.
[2] Start Brique Analytics.
[3] Stop Brique Analytics.
[4] Remove Brique Analytics.
[5] Show Brique Analytics' version
[6] Quit.
```



