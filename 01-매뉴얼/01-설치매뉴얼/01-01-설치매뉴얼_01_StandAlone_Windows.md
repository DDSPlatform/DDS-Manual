#### BRIQUE Analytics 설치 매뉴얼 (StandAlone - Windows)



본 문서는 BRIQUE Analytics를 Windows 환경의 독립 서버로 구동하기 위한 설치 방법을 포함하고 있음




-----------------------

##### 시스템 요구사양

###### Operating System

- Windows 10 64-bit Home
- Windows 10 Pro
- Windows 10 Enterprise
- Windows 10 Education (Build 18326 이상)



###### S/W

- Docker Desktop for Windows
- WSL 2 (Windows Subsystem for Linux 2) 활성화 및 Ubuntu 20.04 WSL backend ([Install Docker Desktop on Windows](https://docs.docker.com/docker-for-windows/install/))



###### H/W

- CPU

  2.5GHz 4core X 1cpu 이상

- Memory

  16GB 이상

- HDD

  100GB 이상



------

##### 필요 S/W 설치



###### 1. WSL 설치

1. 관리자 권한으로 Widnows Power Shell 시작

   시작 > Windows PowerShell > **<u>관리자 권한</u>**으로 실행

   

   ![Window Power Shell 시작](H:/공유 드라이브/BRIQUE/(B)과제/(BB)내부/BA/v2.1.0-r1/03.매뉴얼/04.운영자/img/install-windows1.png)

   

   ```powershell
   Windows PowerShell
   Copyright (C) Microsoft Corporation. All rights reserved.
   
   새로운 크로스 플랫폼 PowerShell 사용 https://aka.ms/pscore6
   
   PS C:\WINDOWS\system32>
   ```

   

2. WSL 설정

   ```powershell
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

   

3. Windows 재 부팅

   

4. WSL2 Linux 커널 업데이트 패키지(wsl_update_x64.msi) 다운로드 및 설치

   [x64 머신용 최신 WSL2 Linux 커널 업데이트 패키지](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

   

5. WSL 기본 버전 설정

   ```powershell
   PS C:\WINDOWS\system32> wsl --set-default-version 2
   WSL 2와의 주요 차이점에 대한 자세한 내용은 https://aka.ms/wsl2를 참조하세요
   작업을 완료했습니다.
   
   PS C:\WINDOWS\system32>
   ```

   

------

###### 2. Docker Desktop for Windows 설치

1. 설치파일 다운로드

   [Docker Desktop for Mac and Windows | Docker](https://www.docker.com/products/docker-desktop)

   

2. 설치

   설치 도중 아래 Configuration 모두 Check 후 설치 진행
   ![설치 Configuration](H:/공유 드라이브/BRIQUE/(B)과제/(BB)내부/BA/v2.1.0-r1/03.매뉴얼/04.운영자/img/install-windows3.png)

   

3. Docker Desktop 환경설정

   - 바탕 화면에 생성된 Docker Desktop 실행

   - Windows System Tray의 Docker Desktop Icon에서 환경설정 메뉴로 이동
     ![Window Power Shell 시작](H:/공유 드라이브/BRIQUE/(B)과제/(BB)내부/BA/v2.1.0-r1/03.매뉴얼/04.운영자/img/install-windows5.png)

     

   - General Tab에 Use the WSL2 based engine이 선택(체크)되어 있는지 확인

   - 선택이 안되어 있다면 선택(체크) 후, Apply & Restart 버튼 클릭

     ![General 설정](H:/공유 드라이브/BRIQUE/(B)과제/(BB)내부/BA/v2.1.0-r1/03.매뉴얼/04.운영자/img/install-windows6.png)

     

   - Resource > WSL Integration 메뉴로 이동

   - Enable Integration with my default WSL distro가 선택(체크)되어있는지 확인

   - 선택이 안되어 있다면 선택(체크) 후, Apply & Restart 버튼 클릭

     ![Resource 설정](H:/공유 드라이브/BRIQUE/(B)과제/(BB)내부/BA/v2.1.0-r1/03.매뉴얼/04.운영자/img/install-windows7.png)



------

##### 온라인 설치



###### 1. 설치파일 다운로드

- https://ba.brique.kr/file/installer/v210r1/ba-v210r1-win64-installer.zip

- 압축해제

  C:\ba-v210r1-win64-installer



###### 2. 설치

```powershell
#===============================================================================
# 1.실행정책 설정
#===============================================================================
PS C:\WINDOWS\system32> Set-ExecutionPolicy unrestricted

실행 규칙 변경
실행 정책은 신뢰하지 않는 스크립트로부터 사용자를 보호합니다. 실행 정책을 변경하면 about_Execution_Policies 도움말
항목(https://go.microsoft.com/fwlink/?LinkID=135170)에 설명된 보안 위험에 노출될 수 있습니다. 실행 정책을
변경하시겠습니까?
[Y] 예(Y)  [A] 모두 예(A)  [N] 아니요(N)  [L] 모두 아니요(L)  [S] 일시 중단(S)  [?] 도움말 (기본값은 "N"): A

#===============================================================================
# 2.설치폴더로 이동 후, 설치 실행
#===============================================================================
PS C:\WINDOWS\system32> cd c:\ba-v210r1-win64-installer
PS C:\ba-v210r1-win64-installer> ./ba.ps1 install

......
보안 경고
신뢰하는 스크립트만 실행하십시오. 인터넷의 스크립트는 유용할 수 있지만 사용자 컴퓨터를 손상시킬 수도 있습니다.
스크립트를 신뢰하는 경우 Unblock-File cmdlet을 사용하면 이 경고 메시지 없이 스크립트를 실행할 수 있습니다.
C:\ba-v210r1-win64-installer\ba.ps1을(를) 실행하시겠습니까?
[D] 실행 안 함(D)  [R] 한 번 실행(R)  [S] 일시 중단(S)  [?] 도움말 (기본값은 "D"): R
......

#-------------------------------------------------------------------------------
# 다음 오류 발생 시, Docker Desktop이 초기화 될때까지 기다려야 함
#-------------------------------------------------------------------------------
docker : 'docker' 용어가 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램 이름으로 인식되지 않습니다. 이름이 정확한지 확인하고 경로가 포함된 경우 경로가 올바른지 검증한 다음 다시 시도하십시오.
#-------------------------------------------------------------------------------
# 반복적인 오류 발생 시, Docker Desktop을 실행 후, install 재 실행
#-------------------------------------------------------------------------------

......

# 기본값으로 설치하기 위해 Enter 키를 입력하여 진행

......

#===============================================================================
# 3.설치폴더 변경 (필요시)
#===============================================================================
......
[Step 5] Installing BA
>> Current host IP address: 192.168.0.103
>> Current hostname: DESKTOP-6680PQ4
> 5.2. Enter directory path where you want to install Brique Analytics. (default: C:\Users\brique\ba)
>> Directory: C:\BA
......

#===============================================================================
# 4.설치완료
#===============================================================================
......

==> BA is installed completely. You can access BA ui at http://127.0.0.1:8080 with default username/password: admin/brique_admin
```



###### 3. 설치 확인

```powershell
# 데이터베이스 설치 확인
PS C:\ba-v210r1-win64-installer> docker ps -a | findstr post
7e98feba59fe   brique/ba-eco-postgres13:v2.1.0-r1          "docker-entrypoint.s??   37 minutes ago   Up 37 minutes               0.0.0.0:5432->5432/tcp                   postgres13

# 서비스 설치 확인
PS C:\ba-v210r1-win64-installer> docker service ls
ID             NAME                        MODE         REPLICAS   IMAGE                                       PORTS
......
1dgnurndg9el   ba-prod_admin               replicated   1/1        brique/ba-api:v2.1.0-r1
l8c1foyp488j   ba-prod_auth                replicated   1/1        brique/ba-api:v2.1.0-r1
l5y191c8opng   ba-prod_batch               replicated   1/1        brique/ba-api:v2.1.0-r1
o7zbvfldie3g   ba-prod_main                replicated   1/1        brique/ba-api:v2.1.0-r1
......

PS C:\ba-v210r1-win64-installer>
```



###### 4. 동작확인

크롬 브라우져를 통해 BRIQUE Analytics에 접속

- 접속 URL

  http://localhost:8080

- 접속계정

  admin / brique_admin



------

##### 오프라인 설치



###### 1. 설치파일 다운로드

- BA 설치파일 다운로드 및 압축해제

  - 압축해제 위치 (C:\ba-v210r1-win64-installer)
  - https://ba.brique.kr/file/installer/v210r1/ba-v210r1-win64-installer.zip

- BA 파일 다운로드

  - 다운로드 위치 (C:\ba-v210r1-win64-installer\datafile)
  - https://ba.brique.kr/file/installer/v210r1/ba-v210.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/library_basic.tar.gz

- Python3.6 설치 및 패키지 파일 다운로드

  - 다운로드 위치 (C:\ba-v210r1-win64-installer\datafile)
  - https://ba.brique.kr/file/installer/v210r1/python36.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/python36-package-full.tar.gz

- R3.6.0 설치 및 패키지 파일 다운로드

  - 다운로드 위치 (C:\ba-v210r1-win64-installer\datafile)
  - https://ba.brique.kr/file/installer/v210r1/r360.tar.gz
  - https://ba.brique.kr/file/installer/v210r1/r360-package-full.tar.gz

  

- Docker Image 파일 다운로드

  - 다운로드 위치 (C:\ba-v210r1-win64-installer\datafile\imgs)
  - https://ba.brique.kr/file/installer/v210r1/docker-image/api.tar.gz
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



###### 2. 설치

```powershell
#===============================================================================
# 1.실행정책 설정
#===============================================================================
PS C:\WINDOWS\system32> Set-ExecutionPolicy unrestricted

실행 규칙 변경
실행 정책은 신뢰하지 않는 스크립트로부터 사용자를 보호합니다. 실행 정책을 변경하면 about_Execution_Policies 도움말
항목(https://go.microsoft.com/fwlink/?LinkID=135170)에 설명된 보안 위험에 노출될 수 있습니다. 실행 정책을
변경하시겠습니까?
[Y] 예(Y)  [A] 모두 예(A)  [N] 아니요(N)  [L] 모두 아니요(L)  [S] 일시 중단(S)  [?] 도움말 (기본값은 "N"): A

#===============================================================================
# 2.설치폴더로 이동 후, 설치 실행
#===============================================================================
PS C:\WINDOWS\system32> cd c:\ba-v210r1-win64-installer
PS C:\ba-v210r1-win64-installer> ./ba.ps1 install C:\ba-v210r1-win64-installer

......
보안 경고
신뢰하는 스크립트만 실행하십시오. 인터넷의 스크립트는 유용할 수 있지만 사용자 컴퓨터를 손상시킬 수도 있습니다.
스크립트를 신뢰하는 경우 Unblock-File cmdlet을 사용하면 이 경고 메시지 없이 스크립트를 실행할 수 있습니다.
C:\ba-v210r1-win64-installer\ba.ps1을(를) 실행하시겠습니까?
[D] 실행 안 함(D)  [R] 한 번 실행(R)  [S] 일시 중단(S)  [?] 도움말 (기본값은 "D"): R
......

#-------------------------------------------------------------------------------
# 다음 오류 발생 시, Docker Desktop이 초기화 될때까지 기다려야 함
#-------------------------------------------------------------------------------
docker : 'docker' 용어가 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램 이름으로 인식되지 않습니다. 이름이 정확한지 확인하고 경로가 포함된 경우 경로가 올바른지 검증한 다음 다시 시도하십시오.
#-------------------------------------------------------------------------------
# 반복적인 오류 발생 시, Docker Desktop을 실행 후, install 재 실행
#-------------------------------------------------------------------------------

......

# 기본값으로 설치하기 위해 Enter 키를 입력하여 진행

......

#===============================================================================
# 3.설치폴더 변경 (필요시)
#===============================================================================
......
[Step 5] Installing BA
>> Current host IP address: 192.168.0.103
>> Current hostname: DESKTOP-6680PQ4
> 5.2. Enter directory path where you want to install Brique Analytics. (default: C:\Users\brique\ba)
>> Directory: C:\BA
......

#===============================================================================
# 4.설치완료
#===============================================================================
......

==> BA is installed completely. You can access BA ui at http://127.0.0.1:8080 with default username/password: admin/brique_admin
```



###### 3. 설치 확인 (온라인 설치와 동일)

```powershell
# 데이터베이스 설치 확인
PS C:\ba-v210r1-win64-installer> docker ps -a | findstr post
7e98feba59fe   brique/ba-eco-postgres13:v2.1.0-r1          "docker-entrypoint.s??   37 minutes ago   Up 37 minutes               0.0.0.0:5432->5432/tcp                   postgres13

# 서비스 설치 확인
PS C:\ba-v210r1-win64-installer> docker service ls
ID             NAME                        MODE         REPLICAS   IMAGE                                       PORTS
......
1dgnurndg9el   ba-prod_admin               replicated   1/1        brique/ba-api:v2.1.0-r1
l8c1foyp488j   ba-prod_auth                replicated   1/1        brique/ba-api:v2.1.0-r1
l5y191c8opng   ba-prod_batch               replicated   1/1        brique/ba-api:v2.1.0-r1
o7zbvfldie3g   ba-prod_main                replicated   1/1        brique/ba-api:v2.1.0-r1
......

PS C:\ba-v210r1-win64-installer>
```



###### 4. 동작 확인 (온라인 설치와 동일)

크롬 브라우져를 통해 BRIQUE Analytics에 접속

- 접속 URL

  http://localhost:8080

- 접속계정

  admin / brique_admin



------

##### 설치 제거 



###### 1. 실행 중단

```powershell
# 서비스 중단
PS C:\WINDOWS\system32> cd c:\ba-v210r1-win64-installer
PS C:\ba-v210r1-win64-installer>  ./ba.ps1 stop
......

==> BA is stopped completely. To run BA again, using this command: ba start
```



###### 2. 설치파일 제거

```powershell
# 설치 제거
PS C:\WINDOWS\system32> cd c:\ba-v210r1-win64-installer
PS C:\ba-v210r1-win64-installer> ./ba.ps1 remove
......

Removed BA completely. For more information, please visit https://ba.brique.kr/.
```



------

##### 문제 해결



###### 1. 윈도우 재 시작 시 서비스 구동

  - Docker Desktop 실행 후, 서비스 실행여부 확인
    ![Docker Desktop 시작](H:/공유 드라이브/BRIQUE/(B)과제/(BB)내부/BA/v2.1.0-r1/03.매뉴얼/04.운영자/img/install-windows14.png)

    

  - 데이터베이스 및 서비스 실행여부 확인

    ```powershell
    PS C:\WINDOWS\system32> docker ps -a | findstr post
    c9338738d6c9   brique/ba-eco-postgres13:v2.1.0-r1          "docker-entrypoint.s??   2 hours ago         Exited (255) About a minute ago   0.0.0.0:5432->5432/tcp                   postgres13
    
    #-------------------------------------------------------------------------------
    # Exit 상태인 경우, 데이터베이스 재 실행
    #-------------------------------------------------------------------------------
    PS C:\WINDOWS\system32> docker start postgres13
    
    # 데이터베이스 실행 재 확인
    PS C:\WINDOWS\system32> docker ps -a | findstr post
    c9338738d6c9   brique/ba-eco-postgres13:v2.1.0-r1          "docker-entrypoint.s??   2 hours ago          Up 3 seconds                      0.0.0.0:5432->5432/tcp                   postgres13
    
    # 서비스 실행 확인 (서비스는 자동으로 실행되기 때문에 모든 서비스가 1/1이 될 때까지 대기)
    PS C:\WINDOWS\system32> docker service ls
    ID             NAME                        MODE         REPLICAS   IMAGE                                       PORTS
    ......
    1dgnurndg9el   ba-prod_admin               replicated   1/1        brique/ba-api:v2.1.0-r1
    l8c1foyp488j   ba-prod_auth                replicated   1/1        brique/ba-api:v2.1.0-r1
    l5y191c8opng   ba-prod_batch               replicated   1/1        brique/ba-api:v2.1.0-r1
    o7zbvfldie3g   ba-prod_main                replicated   1/1        brique/ba-api:v2.1.0-r1
    ......
    
    PS C:\WINDOWS\system32>
    ```

  

------

###### 2. 서비스 재 시작

```powershell
# 워크플로우 실행이 안되는 경우
PS C:\WINDOWS\system32> docker service scale ba-prod_platform-workflow=0
PS C:\WINDOWS\system32> docker service scale ba-prod_platform-workflow=1

# 워크플로우 실행결과가 표현이 안되는 경우
PS C:\WINDOWS\system32> docker service scale ba-prod_platform-result=0
PS C:\WINDOWS\system32> docker service scale ba-prod_platform-result=1
```



------

###### 3. 로그인 오류

- 데이터베이스 및 서비스 실행여부 확인

```powershell
# 데이터베이스 서비스 실행여부 확인
PS C:\WINDOWS\system32> docker ps -a | findstr post
c9338738d6c9   brique/ba-eco-postgres13:v2.1.0-r1          "docker-entrypoint.s??   2 hours ago         Exited (255) About a minute ago   0.0.0.0:5432->5432/tcp                   postgres13

#-------------------------------------------------------------------------------
# Exit 상태인 경우, 데이터베이스 재 실행
#-------------------------------------------------------------------------------
PS C:\WINDOWS\system32> docker start postgres13

# 데이터베이스 실행 재 확인
PS C:\WINDOWS\system32> docker ps -a | findstr post
c9338738d6c9   brique/ba-eco-postgres13:v2.1.0-r1          "docker-entrypoint.s??   2 hours ago          Up 3 seconds                      0.0.0.0:5432->5432/tcp                   postgres13

PS C:\WINDOWS\system32>
```

