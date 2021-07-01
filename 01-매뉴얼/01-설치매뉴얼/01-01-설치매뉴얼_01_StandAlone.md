#### Required H/W Specification

- Minimum 8GB Memory
- Minimum 50GB HDD



#### Prerequisite

- Linux CentOS 7.x
- docker 19.x
- docker-compose 1.2x.x



#### Install

```sh
# hostname 변경
$ sudo hostnamectl set-hostname ba-srv

# hosts 파일에 설치되는 장비의 IP등록
$ sudo vi /etc/hosts
192.168.x.x    ba-srv

# /opt 밑으로 이동
$ cd /opt

# 설치파일 다운로드
$ sudo curl -L "https://ba.brique.kr/ba-v1.2.0-r1.tar.gz" -o ba-v1.2.0-r1.tar.gz

# 압축해제
$ sudo tar xvfz ba-v1.2.0-r1.tar.gz

# IP설정
$ cd /opt/ba
$ ./init_ip.sh

# 방화벽 해제
$ sudo systemctl stop firewalld
$ sudo systemctl disable firewalld

$ sudo iptables -t filter -F
$ sudo iptables -t filter -X

$ sudo systemctl restart docker
```



#### Run

```sh
# BA 설치위치로 이동
$ cd /opt/ba

# Timeout설정
$ export DOCKER_CLIENT_TIMEOUT=1200
$ export COMPOSE_HTTP_TIMEOUT=1200

# BA 컨테이너 생성 및 시작
$ docker-compose up

========================================================================================
#*********** 다음 로그가 출력될 때 까지 대기 ************************************************
========================================================================================
oracle_1          | Database ready to use. Enjoy! ;)
========================================================================================

# CRTL + C로 종료 후, 컨테이너 재시작
$ docker-compose start

# Docker Container 확인 (State가 전체 UP인 상태여야 함. 아닌 경우, 중지 후 재시작)
$ docker-compose ps

# State 전체가 Up이 아닌 경우에만, BA 컨테이너 중지 후, 재시작
$ docker-compose stop
$ docker-compose start

# SQLPLUS 접속
$ docker-compose exec oracle sqlplus
# user-name: system
# password: oracle

SQL*Plus: Release 12.1.0.2.0 Production on Thu Jun 18 05:09:55 2020

Copyright (c) 1982, 2014, Oracle.  All rights reserved.

Enter user-name: system
Enter password:
Last Successful login time: Thu Jun 18 2020 05:07:40 +00:00

Connected to:
Oracle Database 12c Standard Edition Release 12.1.0.2.0 - 64bit Production

# 초기스크립트 실행
SQL> @/u01/app/oracle/init.sql

# SQLPLUS 종료
SQL> quit

```



#### Use

- Chrome 브라우저를 이용해서 접속
- http://{ip}:8080
- User ID: data
- Password: 1



------

#### Troubleshoot

------

- 최초 컨테이너 실행 시, 오라클 설치가 정상적으로 진행되지 않은 경우

  ```sh
  # BA 설치파일을 삭제하고 재 설치
  $ docker-composer down
  $ sudo rm -rf /opt/ba
  $ cd /opt
  $ sudo tar xvfz ba-v1.2.0-r1.tar.gz
  $ cd /opt/ba
  $ ./init_ip.sh
  $ docker-compose up
  
  # Oracle 초기데이터 설정
  $ docker-compose exec oracle sqlplus
  SQL> @/u01/app/oracle/init.sql
  SQL> quit
  ```



- 모든 컨테이너가 정상적으로 실행됐는데 다음과 같은 오류가 나는 경우

  ```
  [2020-06-19 12:21:19,269] [ERROR] [kr.co.brique.ba.platform.dao.RedisPoolDAO] [] 	[1|0|0|0][0ms] java.lang.RuntimeException: java.net.UnknownHostException: 192.168.0.31:6379
  ```

  

  ```sh
  # 컨테이너 재 시작
  $ docker-compose stop
  $ docker-compser start
  ```

  

- docker-composer up 실행 시 오류가 나는 경우

  ```sh
  Creating network "ba_default" with the default driver
  ERROR: Failed to Setup IP tables: Unable to enable SKIP DNAT rule:  (iptables failed: iptables --wait -t nat -I DOCKER -i br-afcf4a202cbb -j RETURN: iptables: No chain/target/match by that name. (exit status 1))
  
  # 이런 에러가 발생하는 원인는, Docker는 실행 시, IPTables안에 docker chain을 만드는데, 그 docker가 시작된 후, firewalld 등 다른 시스템에 의한 iptables에 변경이 발생 시(e.g. by a restart of firewalld), docker에서 위와 같은 에러가 발생 할 수 있다고 한다.
  ```

  

  ```sh
  $ sudo iptables -t filter -F
  $ sudo iptables -t filter -X
  $ systemctl restart docker
  ```

  

