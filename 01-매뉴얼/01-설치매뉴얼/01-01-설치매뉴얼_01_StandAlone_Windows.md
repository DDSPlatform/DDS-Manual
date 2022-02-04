#### 01-01-설치매뉴얼_01_StandAlone 설치 가이드(Windows)



본 문서는 BRIQUE Analytics를 개인 Windows PC 환경에서 독립 서버로 구동하기 위한 설치 방법을 포함하고 있음




##### Revision History

| 등록일자   | 작성자 | 내용                             |
| ---------- | ------ | -------------------------------- |
| 2021-11-25 | 최민우 | 신규 작성                        |



-----------------------

##### 시스템 요구사항

- Windows
  - Windows 10 64-bit Home 이상
- 메모리
  - 최소 8 GB 이상,  16GB 이상 권장 
- CPU
  - x64 4 코어 이상
- 저장 공간
  - 100 GB 이상



------
##### 사전 설치 시 확인 사항
- BRIQUE Analytics 는 Linux Docker 기반으로 여러개의 서비스가 유기적으로 조합되어 구동
- 따라서 Windows에서 Docker 구동을 위해 반드시 아래 프로그램이 먼저 설치 되어야 함
  - WSL
    - Windows Subsystem for Linux 2의 줄임말로 윈도우에서 리눅스를 사용할 수 있게 해주는 기능

  - Docker Desktop for Windows
    - Docker를 Windows에서 사용 할 수 있는 기능을 제공하는 소프트웨어 





----------------------------------------------
##### STEP 1 : WSL 설치

- Widnows Power Shell 시작
  - **반드시 관리자 권한으로 실행 해야 함**(앞으로 설치 진행 시 Power Shell은 모두 관리자 모드로 열어야 함)
    ![Window Power Shell 시작](img\install-windows1.png)
  
    

  - 아래 두 명령어 실행

    -  실행 명령어
  
    ```powershell
    $ dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    $ dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    ```
    - 실행 결과
  
    ```powershell
    Windows PowerShell
    Copyright (C) Microsoft Corporation. All rights reserved.
    
    새로운 크로스 플랫폼 PowerShell 사용 https://aka.ms/pscore6
    
    PS C:\WINDOWS\system32> dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    
    배포 이미지 서비스 및 관리 도구
    버전: 10.0.19041.844
    
    이미지 버전: 10.0.19042.1348
    
    기능을 사용하도록 설정하는 중
    [==========================100.0%==========================]
    작업을 완료했습니다.
    PS C:\WINDOWS\system32> dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    
    배포 이미지 서비스 및 관리 도구
    버전: 10.0.19041.844
    
    이미지 버전: 10.0.19042.1348
    
    기능을 사용하도록 설정하는 중
    [==========================100.0%==========================]
    작업을 완료했습니다.
    PS C:\WINDOWS\system32>
    ```
  
      
  
  - **반드시 윈도우즈 재 부팅**
  
  -  [x64 머신용 최신 WSL2 Linux 커널 업데이트 패키지](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)를 다운로드 받아 안내에 따라 설치 진행
  
    - 반드시 아래와 같이 설치 완료가 되어야 함
  
      ![WSL2 설치 완료](img\install-windows2.png)
  
  
  
  
  - Power Shell을 관리자 모드로 열어 아래 명령어 실행
  
  
    - 실행 명령어
  
      ```powershell
      wsl --set-default-version 2
      ```
  
    - 실행 결과
  
      ```powershell
      PS C:\WINDOWS\system32> wsl --set-default-version 2
      WSL 2와의 주요 차이점에 대한 자세한 내용은 https://aka.ms/wsl2를 참조하세요
      작업을 완료했습니다.
      PS C:\WINDOWS\system32>
      ```



------

##### STEP 2 :  Docker Desktop for Windows 설치
- 설치 Page로 이동하여 설치 파일 다운로드
  
- [Docker Desktop for Mac and Windows | Docker](https://www.docker.com/products/docker-desktop)
  
- 설치 진행
  - 설치 도중 아래 Configuration 모두 Check 후 설치 진행
   ![설치 Configuration](img\install-windows3.png)
  
   
  
  - 설치 완료 확인
   ![설치 완료 확인](img\install-windows4.png)
  



- Docker Desktop 환경 설정

  - 바탕 화면에 생성된 Docker Desktop 실행

  - Windows의 System Tray에 Docker Desktop Icon에서 환경 설정 메뉴로 이동
    ![Window Power Shell 시작](img\install-windows5.png)
  
    
  
  - General Tab에 Use the WSL2 based engine이 Check되어 있는지 확인
  
    - UnCheck 상태라면 Check 후 Apply & Restart 버튼 클릭
  
       ![General 설정](img\install-windows6.png)
  
  

  
  - Resource > WSL Integration 메뉴로 이동
  
    - Enable Integration with my default WSL distro에 체크되어있는지 확인 후 체크
      ![Resource 설정](img\install-windows7.png)
      



- BRIQUE Analytics 설치를 위한 사전 준비 작업이 모두 완료 되었습니다.  이제 BRIQUE Anaytics 설치를 시작 해 봅시다



------

##### STEP 3 : BRIQUE Analytics 설치 

- 홈페이지의 다운로드 링크 혹은 다음 URL에서 패키지 `.zip` 파일을 다운로드 합니다.

  - Windows 설치파일 :  https://ba.brique.kr/file/installer/v210r1/ba-v210r1-win64-installer.zip

    

- #####  다운로드 받은 파일을 압축 해제

  - 본 예제에서는 아래 위치에 압축 해제를 진행
      - D:\ba-v210r1-win64-installer
      ![Un Zip](img\install-windows8.png)

  - 설치 대상 환경이 인터넷 연결을 지원하지 않는 경우 혹은 인터넷으로부터 파일을 다운로드 받지 않고 설치를 진행하고자 하는 경우, 아래 파일들을 웹 브라우저 상에서 Url을 직접 입력하거나 `wget` 등의 Command Line 툴을 이용해 다운로드해야 한다.

    - 설치를 위한 스크립트 및 설정파일

      - https://ba.brique.kr/file/installer/v210r1/ba-v210r1-win64-installer.zip
  
    - BA 구동을 위한 데이터 파일
  
      - 한국어 버젼
    
        - https://ba.brique.kr/file/installer/v210r1/ba-v210.tar.gz # 어플리케이션 데이터 파일
    
      - 중국어 버젼(Cowin)
    
        - https://ba.brique.kr/file/installer/v210r1/ba-v210-cowin.tar.gz # 어플리케이션 데이터 파일
          - **다운 받은 후 파일명을 ba-v210-cowin.tar.gz -> ba-v210.tar.gz으로 반드시 변경**
    
      - https://ba.brique.kr/file/installer/v210r1/python36.tar.gz # Python 3.6 설치 파일
    
      - https://ba.brique.kr/file/installer/v210r1/python36-package-full.tar.gz # Python 3.6 패키지 파일
    
      - https://ba.brique.kr/file/installer/v210r1/r360.tar.gz # R 3.6.0 설치 파일
    
      - https://ba.brique.kr/file/installer/v210r1/r360-package-full.tar.gz # R 3.6.0 패키지 파일
    
      - https://ba.brique.kr/file/installer/v210r1/library_basic.tar.gz # BRIQUE Analytics 기본 Library 파일
      - 위 파일들은 설치 스크립트를 실행하는 Root Directory아래 datafile이라는 폴더를 생성 한 후 Copy(Move)해야 함. 설치 파일 압축 해재 위치가 D:\ba-v210r1-win64-installer 일 경우 D:\ba-v210r1-win64-installer\datafile 위치에 Copy
    
      ```powershell
      PS D:\ba-v210r1-win64-installer\datafile>dir
      
      
          디렉터리: D:\ba-v210r1-win64-installer\datafile
      
      
      Mode                 LastWriteTime         Length Name
      ----                 -------------         ------ ----
      -a----      2021-11-29   오후 2:19      426973599 ba-v210.tar.gz
      -a----      2021-11-29   오후 2:19      109989133 python36.tar.gz
      -a----      2021-11-29   오후 2:19     1729393867 python36-package-full.tar.gz
      -a----      2021-11-29   오후 2:19      131383068 r360.tar.gz
      -a----      2021-11-29   오후 2:19      446065759 r360-package-full.tar.gz
      ```
    
      
    
    - 사용할 Docker Image File도 (주)브릭으로부터 수동으로 제공 받아야 함
    
      - Docker Image File 목록
    
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
      - 다운로드 받은 Docker Image File은 `datafile/` 밑의 `imgs/` 디렉토리 밑에 위치해야 함 (총 30 GB의 디스크 공간이 추가로 필요)
    
        - Installer가 `datafile/imgs` 디렉토리를 참조하여 설치 과정중 필요한 이미지 로드
    
      
    
    - ba-v210r1-win64-installer 압축 해제 위치가 c:\\ba-v210r1-win64-installer일 경우 최종 설치 파일 목록은 다음과 같다
    
      - Root Folder
      ![Root Folder](img\install-windows11.png)
      - Root/datafile
      ![Root/datafile](img\install-windows12.png)
      - Root/imgs
      ![Root/imgs](img\install-windows13.png)
    
      
    




- Powershell 창에서 다음 명령어를 실행 후 A 입력
  - 실행 명령어  

    ```powershell
    Set-ExecutionPolicy unrestricted
    ```

  - 실행 결과

    ```powershell
    PS C:\WINDOWS\system32> Set-ExecutionPolicy unrestricted
    
    실행 규칙 변경
    실행 정책은 신뢰하지 않는 스크립트로부터 사용자를 보호합니다. 실행 정책을 변경하면 about_Execution_Policies 도움말
    항목(https://go.microsoft.com/fwlink/?LinkID=135170)에 설명된 보안 위험에 노출될 수 있습니다. 실행 정책을
    변경하시겠습니까?
    [Y] 예(Y)  [A] 모두 예(A)  [N] 아니요(N)  [L] 모두 아니요(L)  [S] 일시 중단(S)  [?] 도움말 (기본값은 "N"): A
    PS C:\WINDOWS\system32>
    ```

  

- Powershell 창에서 압축해제 경로로 이동해 다음과 같이 설치 명령어 실행


  - 이동 및 설치 실행 명령어

      ```powershell
      PS C:\WINDOWS\system32> cd d:\
      PS D:\> cd .\ba-v210r1-win64-installer\
      PS D:\ba-v210r1-win64-installer> dir
      
      
          디렉터리: D:\ba-v210r1-win64-installer
      
      
      Mode                 LastWriteTime         Length Name
      ----                 -------------         ------ ----
      d-----      2021-11-25   오후 3:46                ba-script
      -a----      2021-11-25   오후 3:46           1137 ba.ps1
      
      
      PS D:\ba-v210r1-win64-installer> ./ba.ps1 install
      ```

      

  - 실행 도중 아래와 같은 보안 경고 사항이 나오면 R을 선택하여 설치를 계속 진행해야 함

    ```powershell
    PS D:\ba-v210r1-win64-installer> ./ba.ps1 install
    
    보안 경고
    신뢰하는 스크립트만 실행하십시오. 인터넷의 스크립트는 유용할 수 있지만 사용자 컴퓨터를 손상시킬 수도 있습니다.
    스크립트를 신뢰하는 경우 Unblock-File cmdlet을 사용하면 이 경고 메시지 없이 스크립트를 실행할 수 있습니다.
    D:\ba-v210r1-win64-installer\ba.ps1을(를) 실행하시겠습니까?
    [D] 실행 안 함(D)  [R] 한 번 실행(R)  [S] 일시 중단(S)  [?] 도움말 (기본값은 "D"): R
    
    보안 경고
    신뢰하는 스크립트만 실행하십시오. 인터넷의 스크립트는 유용할 수 있지만 사용자 컴퓨터를 손상시킬 수도 있습니다.
    스크립트를 신뢰하는 경우 Unblock-File cmdlet을 사용하면 이 경고 메시지 없이 스크립트를 실행할 수 있습니다.
    D:\ba-v210r1-win64-installer\ba-script\install.ps1을(를) 실행하시겠습니까?
    [D] 실행 안 함(D)  [R] 한 번 실행(R)  [S] 일시 중단(S)  [?] 도움말 (기본값은 "D"): R
    ```

    
    


  - BRIQUE Analytics 설치는 Docker Desktop이 실행 되어야 정상 진행

      ~~~powershell
      - 아래와 같이 오류 메세지가 보일 경우 Docker Desktop이 초기화 될때까지 기다려야 함
      
        ```powershell
        [Step 1] Checking supported OS:
        [Step 2] Check internet connection:
        You are online.
        [Step 3] Installing necessary packages:
        > For running BA on Windows, we need to enable WSL2 and Docker desktop.
        docker : 'docker' 용어가 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램 이름으로 인식되지 않습니다. 이름이 정
        확한지 확인하고 경로가 포함된 경우 경로가 올바른지 검증한 다음 다시 시도하십시오.
        위치 D:\ba-v210r1-win64-installer\ba-script\install.ps1:163 문자:16
        + $TEMP_CHECK = (docker info)
        +                ~~~~~~
            + CategoryInfo          : ObjectNotFound: (docker:String) [], CommandNotFoundException
            + FullyQualifiedErrorId : CommandNotFoundException
        ```
      
      - 오류가 반복적으로 나올 경우 바탕화면에 Docker Desktop을 실행 후 Power Shell을 다시 Open(관리자 모드)후 Install 명령어 실행
      ~~~

      

  - 아래와 같은 결과가 나오면 정상. 다음단계로 진행

      ~~~powershell
        [Step 1] Checking supported OS:
        
        ## 인터넷 연결이 있는 경우
        [Step 2] Check internet connection:
        Proceeding to online installation.
        ## 인터넷 연결이 있어도 설치디렉토리 밑 datafile/ 디렉토리와 필요한 아카이브 파일이 있는 경우 아래와 같이 오프라인 설치로 진행할 수도 있음
        [Step 2] Check internet connection:
        > BA data tarballs were found. Proceed to offline install? (y/n) y
        Proceeding to offline installation.
        
        [Step 3] Installing necessary packages:
        > For running BA on Windows, we need to enable WSL2 and Docker desktop.
        WARNING: No blkio throttle.read_bps_device support
        WARNING: No blkio throttle.write_bps_device support
        WARNING: No blkio throttle.read_iops_device support
        WARNING: No blkio throttle.write_iops_device support
        >>> Docker initialized. Proceeding to next step...
        [Step 4] Starting swarm mode in docker
        
        보안 경고
        신뢰하는 스크립트만 실행하십시오. 인터넷의 스크립트는 유용할 수 있지만 사용자 컴퓨터를 손상시킬 수도 있습니다.
        스크립트를 신뢰하는 경우 Unblock-File cmdlet을 사용하면 이 경고 메시지 없이 스크립트를 실행할 수 있습니다.
        D:\ba-v210r1-win64-installer\ba-script\docker-node-swarm.ps1을(를) 실행하시겠습니까?
        [D] 실행 안 함(D)  [R] 한 번 실행(R)  [S] 일시 중단(S)  [?] 도움말 (기본값은 "D"): R
        > Initializing swarm mode:
        Swarm initialized: current node (9j85ivfx87rojsj58b44n9u1e) is now a manager.
        
        To add a worker to this swarm, run the following command:
        
            docker swarm join --token SWMTKN-1-25zb7rk31vtv7qp7sxtz6qeg2s724y1nsvcotk7q83e2qod42r-at3a4ai9nu8yuowflfbi2h8q0 192.168.65.3:2377
        
        To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
        
        >> Done
        > Creating ba-eco_nw network:
        bqclix2job9jkb2ir7txoi36m
        >> Done
        > Creating ba-prod_nw network:
        ub40xjnm3v1lf1belpwxodpvx
        >> Done
        [Step 5] Installing BA
        >> Current host IP address: 192.168.0.103
        >> Current hostname: DESKTOP-6680PQ4
        > 5.2. Enter directory path where you want to install Brique Analytics. (default: C:\Users\brique\ba)
        >> Directory:
      ~~~

      

  - 설치 Directory 지정


  - 실제 설치 파일이 저장될 위치를 지정하고 Enter


    - `D:\BA` 라는 폴더에 설치하는 경우의 예시
    
    ~~~powershell
      [Step 5] Installing BA
      >> Current host IP address: 192.168.0.103
      >> Current hostname: DESKTOP-6680PQ4
      > 5.2. Enter directory path where you want to install Brique Analytics. (default: C:\Users\brique\ba)
      >> Directory: D:\BA
    ~~~




- 아래와 같은 문의 사항이 나오면 n으로 입력하고 진행

  ```powershell
    >> Directory: D:\BA
    >> BA Directory: D:\BA
    >>> D:\BA directory already exists. Do you want to reuse contents inside this directory? (y/n): n
  ```

  




  - BA Confiutation  설정


  -  BA에서 사용할 ID 및  사용 Port를 지정하는 항목임

  - 특별한 경우가 아니면 Enter를 입력하여 Default 값이 지정 되도록함

    ```powershell
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
    >>> Postgresql port: 5432
    >>> Postgresql user: ba210
    >>> Postgresql pass: ba210
    >>> Redis port: 6379
    >>> Kafdrop port: 9000
    >>> BA prefix port: 808
    >>> BA main port: 8080
    >>> BA platform port: 8081
    >>> BA auth port: 8082
    >>> BA admin port: 8083
    >>> BA batch port: 8084
    ```



- BA Data File Download 및 설치 진행

  - 설치할 BA Data File을 Download하기 때문에 시간이 걸릴 수 있음

  - 이번 단계에서는 다음과 같은 항목이 자동 진행됨

    - 파일 다운로드
    - DB 설치(Postgresql)
    - Redis/Kafka 설치
    - ba 어플리케이션 설치
    - python / R 설치
    - python / R Package 설치

  - 중간에 아래와 같은 항목이 나오면 Y 입력 후 계속 진행

    ```powershell
    D:\BA\tmp\library_basic의 항목에는 하위 항목이 있으며 Recurse 매개 변수를 지정하지 않았습니다. 계속하면 해당 항목과
    모든 하위 항목이 제거됩니다. 계속하시겠습니까?
    [Y] 예(Y)  [A] 모두 예(A)  [N] 아니요(N)  [L] 모두 아니요(L)  [S] 일시 중단(S)  [?] 도움말 (기본값은 "Y"): Y
    
    ...
    
    >> Do you want to install list of python packages? (y/n):y
    
    ...
    
    >> Do you want to install list of R packages? (y/n):y
    ```

    

  - 아래와 같은 항목이 나오면 모든 설치가 완료됨

    ```powershell
    ==> BA is installed completely. You can access BA ui at http://127.0.0.1:8080 with default username/password: admin/brique_admin
    ```

    

- 정상 설치 검증

  - Power Shell에서 아래 명령어를 통해 정상 설치 여부를 검증함

    - DB 설치 검증 - 아래와 같이 Up 상태 일 경우 정상 설치

      ```powershell
      PS D:\ba-v210r1-win64-installer> docker ps -a | findstr post
      7e98feba59fe   brique/ba-eco-postgres13:v2.1.0-r1          "docker-entrypoint.s??   37 minutes ago   Up 37 minutes               0.0.0.0:5432->5432/tcp                   postgres13
      PS D:\ba-v210r1-win64-installer>
      ```

      

    - 어플리케이션 설치 검증

      - 모든 Application Replicas 항목이 1/1 (Workflow의 경우 2/2)이면 정상 설치

    
    ```powershell
    PS D:\ba-v210r1-win64-installer> docker service ls
    ID             NAME                        MODE         REPLICAS   IMAGE                                       PORTS
    woy83168yg8d   ba-eco-redis_redis          replicated   1/1        brique/ba-redis-slave:v1.3.1-a-20102215
    4i2v58btanig   ba-eco-zk_kafdrop           global       1/1        obsidiandynamics/kafdrop:latest
    b72oti2h0fl4   ba-eco-zk_kafka1            global       1/1        brique/ba-eco-kafka:v1.3.1-a-20102215
    ommzmqyg3yul   ba-eco-zk_zoo1              global       1/1        brique/ba-eco-zookeeper:v1.3.1-a-20102215   *:30000->2181/tcp, *:30001->2888/tcp, *:30002->3888/tcp
    1dgnurndg9el   ba-prod_admin               replicated   1/1        brique/ba-api:v2.1.0-r1
    l8c1foyp488j   ba-prod_auth                replicated   1/1        brique/ba-api:v2.1.0-r1
    l5y191c8opng   ba-prod_batch               replicated   1/1        brique/ba-api:v2.1.0-r1
    o7zbvfldie3g   ba-prod_main                replicated   1/1        brique/ba-api:v2.1.0-r1
    0heybv4ykoyv   ba-prod_platform-database   replicated   1/1        brique/ba-app-database-actor:v2.1.0-r1
    5gxvzl02kdha   ba-prod_platform-http       replicated   1/1        brique/ba-app-http-actor:v2.1.0-r1
    u1mg51c1ir8z   ba-prod_platform-result     replicated   1/1        brique/ba-app-result-actor:v2.1.0-r1
    yumc8ufwwq2n   ba-prod_platform-workflow   replicated   2/2        brique/ba-app-workflow-actor:v2.1.0-r1
    289o10pdqmmq   ba-prod_python36cpu         replicated   1/1        brique/ba-python-36-cpu-slim:v2.0.1-a
    g9d5mdmei9ms   ba-prod_python36download    replicated   1/1        brique/ba-python-36-download:v2.0.1-a
    ezrq7quutlfn   ba-prod_r360                replicated   1/1        brique/ba-r-360-slim:v2.0.1-a
    PS D:\ba-v210r1-win64-installer>
    ```




---------------------------------------

##### STEP 4 : UI 접속 및 동작 확인

- 크롬 브라우져를 통행 BRIQUE Analytic  UI에 접속

  - url : http://localhost:8080 

  - 초기 ID : admin

  - 초기 Password : brique_admin

    ![BRIQUE UI 시작](img\install-windows9.png)

-  ID/Password 입력 후 Login버튼 클릭

  - 아래와 같이 Welcome Page가 나오면 정상 동작
    ![BRIQUE UI -Welcome Page](img\install-windows10.png)



------

##### Trouble Shoot

###### 윈도우 재 시작 시 서비스 구동

  - Docker Desktop 구동

    - 아래와 같이 서비스가 구동되고 있는지 확인
    ![Docker Desktop 시작](img\install-windows14.png)
    
  - Power Shell을 관리자 모드로 Open
  
    - DataBase 구동 확인 - 성공 메세지가 보이는지 확인
    
      - 실행 명령어
    
        ```powershell
        PS C:\WINDOWS\system32> docker ps -a | findstr post
        ```
    
      - 결과 - 오류 
    
        ```powershell
        PS C:\WINDOWS\system32> docker ps -a | findstr post
        c9338738d6c9   brique/ba-eco-postgres13:v2.1.0-r1          "docker-entrypoint.s??   2 hours ago         Exited (255) About a minute ago   0.0.0.0:5432->5432/tcp                   postgres13
        ```
    
        - 위와 같이 Exit 상태인 경우 Manual로 다음과 같이 DataBase를 구동 시켜 준다
    
          ```powershell
          PS C:\WINDOWS\system32> docker start postgres13
          ```
    
      - 결과 - 성공(상태가 Up으로 변경)
    
        ```powershell
        PS C:\WINDOWS\system32> docker ps -a | findstr post
        c9338738d6c9   brique/ba-eco-postgres13:v2.1.0-r1          "docker-entrypoint.s??   2 hours ago          Up 3 seconds                      0.0.0.0:5432->5432/tcp                   postgres13
        ```
    
    - Application 구동 확인
    
      - 실행 명령어
    
        ```powershell
        PS C:\WINDOWS\system32> docker service ls
        ```
    
      - 결과 - 모든 Service Replicas 상태가 1/1인지 확인
    
        - 일반적으로 ba-prod_platform-http가 가장 마지막에 1/1로 변경됨
        - 서비스는 자동으로 Up되기 때문에 모든 서비스가 1/1이 될 때까지 대기
    
        ```powershell
        PS C:\WINDOWS\system32> docker service ls
        ID             NAME                        MODE         REPLICAS   IMAGE                                       PORTS
        i25wps9xj83e   ba-eco-redis_redis          replicated   1/1        brique/ba-redis-slave:v1.3.1-a-20102215
        uqrihzes1t93   ba-eco-zk_kafdrop           global       1/1        obsidiandynamics/kafdrop:latest
        nafc5jquj3dz   ba-eco-zk_kafka1            global       1/1        brique/ba-eco-kafka:v1.3.1-a-20102215
        eofw1eurkou5   ba-eco-zk_zoo1              global       1/1        brique/ba-eco-zookeeper:v1.3.1-a-20102215   *:30000->2181/tcp, *:30001->2888/tcp, *:30002->3888/tcp
        o6j17pov960p   ba-prod_admin               replicated   1/1        brique/ba-api:v2.1.0-r1
        eqsukojy0xy1   ba-prod_auth                replicated   1/1        brique/ba-api:v2.1.0-r1
        z6hdym6ok5vq   ba-prod_batch               replicated   1/1        brique/ba-api:v2.1.0-r1
        yr9wbi811l4f   ba-prod_main                replicated   1/1        brique/ba-api:v2.1.0-r1
        iey4q5b4pkf8   ba-prod_platform-database   replicated   1/1        brique/ba-app-database-actor:v2.1.0-r1
        uslekdzadj38   ba-prod_platform-http       replicated   1/1        brique/ba-app-http-actor:v2.1.0-r1
        tn1d5gc68pe0   ba-prod_platform-result     replicated   1/1        brique/ba-app-result-actor:v2.1.0-r1
        8nf6gpj7s7h7   ba-prod_platform-workflow   replicated   1/1        brique/ba-app-workflow-actor:v2.1.0-r1
        4erjlf6stbw5   ba-prod_python36cpu         replicated   1/1        brique/ba-python-36-cpu-slim:v2.0.1-a
        cvi05jsliygj   ba-prod_python36download    replicated   1/1        brique/ba-python-36-download:v2.0.1-a
        mu9uuckpjnms   ba-prod_r360                replicated   1/1        brique/ba-r-360-slim:v2.0.1-a
        PS C:\WINDOWS\system32>
        ```
    
    - UI 접속
    
      - 크롬 브라우져에서 http://localhost:8080으로 Open하여 접속되는지 확인

  

------



###### 접속 후 워크플로우 실행 오류
- PowerShell 관리자로 Open

- 다음 명령어로 관련 서비스 재시작

  - 실행 명령어

    ```powershell
    PS C:\WINDOWS\system32> docker service scale ba-prod_platform-workflow=0
    PS C:\WINDOWS\system32> docker service scale ba-prod_platform-workflow=1
    ```

    




------
###### Result 버튼 클릭시 오류 발생
- PowerShell 관리자로 Open

- 다음 명령어로 관련 서비스 재시작

  - 실행 명령어

    ```powershell
    PS C:\WINDOWS\system32> docker service scale ba-prod_platform-result=0
    PS C:\WINDOWS\system32> docker service scale ba-prod_platform-result=1
    ```



------

###### 로그인 오류

- 정상적인 ID/PW를 입력 했는데 로그인이 안되는 경우
  - Data Base가 구동 중인지 확인
    - 윈도우 재 시작 시 서비스 구동 항목의 DB 구동 참조







------

