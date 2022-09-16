# mysqldb 컨테이너에 bash 쉘로 연결 후 컨테이너 IP 확인을 확인하려다 해결하는 에러
## sh: ip: command not found
### 1. 명령어가 설치되어 있지 않아 나는 에러라고 발견
- ip 명령어가 존재하지 않는 오류가 발생한것으로 관련된 라이브러리를 설치해준다.
- 이를 해결하기위해 iproute 를 설치하면 되는데 명령어는 아래와 같다
> yum install iproute
bash: yum: command not found
혹시 yum 패키지가 설치되어있지 않다면 아래 방법으로도 가능하다.

> apt-get install iproute
-> 나는 둘다 없었음.
![image](https://user-images.githubusercontent.com/30613069/190542807-4148627c-d745-46e8-8860-546f3e0000bf.png)

### 2. ubuntu에서 apt install yum 를 해보라는 것에 대한 오류도 발견
![image](https://user-images.githubusercontent.com/30613069/190543091-33d2d380-b824-4175-8902-99c54daefd76.png)
-> are you root? <- 에서 root 가 뭔지 구글링 

- 리눅스에서 특정 명령을 실행하거나 파일에 접근하려면 루트(root) 권한이 필요한데, 일반 사용자(유저)가 root 권한을 얻기 위해 su, sudo 명령어를 사용한다.
- 위 에러는 root 권한을 갖지 않은 채 권한이 필요한 행위를 자꾸 하려고 하니 오류가 났음
- sudo 쓰니 해결
- 하지만 근본적인 yum 해결은 아님

### 3. ubuntu에서 package를 다운로드하는 홈페이지 주소가 추가되어 있지 않아서 그렇다.
-> /etc/apt/source.list에 다음 url을 추가한다. (혹시 모르니 source.list파일 백업 필수)
> deb http://archive.ubuntu.com/ubuntu bionic main restricted universe multiverse
> deb http://archive.ubuntu.com/ubuntu bionic-security main restricted universe multiverse
> deb http://archive.ubuntu.com/ubuntu bionic-updates main restricted universe multiverse

![image](https://user-images.githubusercontent.com/30613069/190543723-3f090e89-801d-4652-b8d6-d67a0e6572d4.png)
1. 백업 파일 만들기 -> $sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak **띄어쓰기 조심!**

2. deb 추가 -> $echo "deb deb http://archive.ubuntu.com/ubuntu bionic main restricted universe multiverse" | sudo tee -a /etc/apt/sources.list 
$echo "deb http://archive.ubuntu.com/ubuntu bionic-security main restricted universe multiverse" | sudo tee -a /etc/apt/sources.list 
$echo "deb http://archive.ubuntu.com/ubuntu bionic-updates main restricted universe multiverse" | sudo tee -a /etc/apt/sources.list 

3. 잘 추가 되었나 확인 -> $vi /etc/apt/soucres.list

4. 업데이트 -> $sudo apt-get update

5. 다시 iproute 추가 ->  apt-get install iproute
>  yum은 레드햇 계열 리눅스 파일 관리자라고 한다. 우분투에서는 그냥 apt 쓰면 된다고 해서 apt로 사용
![image](https://user-images.githubusercontent.com/30613069/190544275-833f6ab9-5519-49f4-8424-b9a588242c22.png)

```cmd
>> apt-get install iproute

Reading package lists... Done
Building dependency tree       
Reading state information... Done
Package iproute is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source
However the following packages replace it:
  iproute2

E: Package 'iproute' has no installation candidate
```
-> 위와 같이 떠서 iproute2로 재설치 진행

6. iproute2 추가 ->  apt-get install iproute2


출처: https://smoh.tistory.com/284 [Simple is Beautiful.:티스토리]
