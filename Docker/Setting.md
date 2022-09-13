# Docker 세팅!

## 1. Docker Desktop 다운로드
https://www.docker.com/products/docker-desktop/
> 자신의 운영체제에 맞는 걸로 다운로드

## 2. 설치 완료 시, PowerShell/cmd 로 Docker 버전 확인
> docker -v
![image](https://user-images.githubusercontent.com/30613069/189896181-5b066b5d-9360-4f5c-ad2c-f1dc56d95121.png)

## 3. hoxy, wsl2 관련 error가 뜬다면..!?
> https://docs.docker.com/desktop/windows/wsl/
> wsl2 설치해주고 다시 컴퓨터 재시작하면, docker 실행 가능했었음..!

## 4. MySQL Docker 이미지 다운
> docker pull mysql
> 위 명령어로 최신 MySQL 이미지를 다운로드! 태그에 버전을 지정X, 최신버전 다운로드함!
> docker pull mysql:8.0.22 <- 이런 식으로 특정 버전 받고 싶을 시, 버전을 명시해줘야함

## 5. MySQL Docker 컨테이너 생성 및 실행
> docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=<password> -d -p 3306:3306 mysql:latest
> mysql-container 이름을 가진 컨테이너 생성
```powershell
PS C:\Users\user> docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=<password> -d -p 3306:3306 mysql:latest
6d1f570e5ed56fd82ba337ed1e4fb4a9de66fa25864d12e51836b16f4cbce235
docker: Error response from daemon: Ports are not available: exposing port TCP 0.0.0.0:3306 -> 0.0.0.0:0: listen tcp 0.0.0.0:3306: bind: Only one usage of each socket address (protocol/network address/port) is normally permitted.

  
PS C:\Users\user> docker run --name sql -e MYSQL_ROOT_PASSWORD=Password -e MYSQL_DATABASE=mydb -d -p 3306:3306 mysql:latest  10af3698ac3e154c93a463cd01c296fb523f2c038305c31341f0ffa595dac72d
docker: Error response from daemon: Ports are not available: exposing port TCP 0.0.0.0:3306 -> 0.0.0.0:0: listen tcp 0.0.0.0:3306: bind: Only one usage of each socket address (protocol/network address/port) is normally permitted.
```
> 실행
```powershell
PS C:\Users\user> docker start sql
Error response from daemon: Ports are not available: exposing port TCP 0.0.0.0:3306 -> 0.0.0.0:0: listen tcp 0.0.0.0:3306: bind: Only one usage of each socket address (protocol/network address/port) is normally permitted.
Error: failed to start containers: sql

PS C:\Users\user> netstat -ano | findstr 3306
>>
  TCP    0.0.0.0:3306           0.0.0.0:0              LISTENING       6816
  TCP    0.0.0.0:33060          0.0.0.0:0              LISTENING       6816
  TCP    [::]:3306              [::]:0                 LISTENING       6816
  TCP    [::]:33060             [::]:0                 LISTENING       6816
```
> netstat -ano | findstr 3306 <- 명령어 이용해 3306 포트 사용하고 있는 게 있는 
> 위 에러는 3306포트를 이미 사용하고 있어서 나는 에러, 그래서 다시 3307 포트로 재지정함.  
  
## 6. 완성
  ![image](https://user-images.githubusercontent.com/30613069/189900384-fa5e6794-bbb6-4359-bd12-e6127d6da032.png)
