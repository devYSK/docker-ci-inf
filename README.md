# docker-ci-inf
인프런 John Ahn님의 따라하며 배우는 도커와 CI환경을 공부하면서 정리한 Repo입니다.

# 도커를 쓰는 이유

* 어떠한 프로그램을 다운 받는 과정을 굉장히 간단하게 `만들기 위해서`!

* 서버, 패키지버전, 운영체제 등에 따라 프로그램 설치 과정중 많은 에러들이 발생

* 도커를 사용하면 에러도 덜 발생하고 설치 과정도 매우 간단해진다.

# 도커란 무엇인가

* 컨테이너를 사용하여 응용프로그램을 더 쉽게 만들고 배포하고 실행할 수 있도록 설계된 도구.

* 컨테이너 기반의 오픈소스 가상화 플랫폼이며 생태계

* ## 서버에서의 컨테이너 개념
    * 컨테이너 안에 다양한 프로그램, 실행환경을 컨테이너로 추상화하고 동일한 인터페이스 제공
    * 프로그램의 배포 및 관리를 단순하게 만듬
    * 프로그램을 손쉽게 이동, 배포, 관리를 할 수 있게 해줌
    * AWS, Azure, GCP 등 어디든 실행가능하게 해줌
        * MySQL, Node, Webpack 등

# 도커이미지와 도커 컨테이너 정의

## 컨테이너
> 코드와 모든 종속성을 패키지화 하여 응용프로그램이 한 컴퓨팅 환경에서 다른 컴퓨팅 환경으로 빠르고 안정적으로 실행되도록하는 소프트웨어의 표준 단위

* 간단하고 편리하게 프로그램을 실행시켜주는것
* `도커 이미지`

## 컨테이너 이미지

> 코드, 런타임, 도구, 라이브러리 및 설정과 같은 응용프로그램을 실행하는데 필요한 모든것을 포함하는, 가볍고 독립적이며 실행가능한 `소프트웨어 패키지`

* 컨테이너 이미지는 런타임에 컨테이너가 되고, 도커 컨테이너의 경우 도커 엔진에서 실행될 때 이미지가 컨테이너가 된다.

* 리눅스나 윈도우 기반 App 모두에서 사용할 수 있는 컨테이너화 된 소프트웨어는 인프라에 관계없이 항상 동일하게 실행

* 컨테이너는 SW를 환경으로부터 격리시키고 개발과 스테이징의 차이에도 불구하고 균일하게 작동하도록 보장

* `도커이미지의 인스턴스`

> 도커 이미지는 프로그램을 실행하는데 필요한 설정이나 종속성을 갖고 있으며,  
도커 이미지를 이용해서 컨테이너를 생성!,  
도커 컨테이너를 이용하여 프로그램을 실행!


# Mac Os에서의 도커 설치

1. Docker사이트로 이동 - Docker.com
2. get started 버튼 클릭
3. 도커 다운로드
4. 설치
5. 회원가입
6. 로그인
7. 도커설치 확인
8. 명령어 docker version

# 도커 사용할때의 흐름

* 명령어 docker run [이미지 이름]

## 명령어를 사용했을때의 흐름
1. 명령어를 치면
2. 도커 클라이언트(명령어를 입력한 컴퓨터)에서 도커 서버로 명령어 전달. 
3. 도커 이미지 보관 장소에서 이미지가 있는지 확인 
  * 없으면 unable to find image라고 나옴
4. 없다면 도커 허브에서 이미지들을 가져온다.
  * pulling from library/이미지명 라고 나옴

  * ![](images/e882dc9d.png) 

  
* 정리하자면
  1. 도커 CLI에 커맨드 입력
  2. 도커 서버(도커 Daemon)이 명령어(커맨드)를 받아 그것에 따라 작업한다.

# 도커와 가상화 기술과의 차이를 통한 컨테이너 이해

* 하이퍼바이저 기반의 가상화
> 논리적으로 공간을 분할하여 VM이라는 독립적 가상 환경의 서버  
> 호스트 시스템에서 다수의 게스트 OS를 구동할 수 있게하는 소프트웨어, 하드웨어를 가상화 


* ![](images/7815b03d.png)

* 도커가 VM과 비교했을 때는 컨테이너가 하이퍼바이저와 게스트 OS가 필요하지 않으므로 더 가벼움

* 어플리케이션 실행 시 컨테이너 방식에서는 호스트 OS 위에 실행 패키지인 이미지만 배포하면 된다  

* ## 공통점
  * 도커 컨테이너와 가상 머신은 기본 하드웨어에서 격리된 환경 내에 어플리케이션을 배치하는 방법

* ## 차이점
  * 격리된 환경을 얼마나 격리시키는지의 차이


* 도커 컨테이너에서 돌아가는 애플리케이션은 컨테이너가 제공하는 격리 기능 내부에 샌드박스가 있지만, 같은 호스트(OS등)의 다른 컨테이너와 `동일한 커널 을 공유`한다.
* 그래서 컨테이너 내부에서 실행되는 프로세스는 호스트 시스템에서 볼 수 있다.
* 예를 들어 도커와 함께 몽고DB 컨테이너를 시작하면 호스트OS(실행 호스트, 도커 아님, 나같은경우 맥)의 일반 쉘에서 `ps-e grep 몽고`를 실행하면 프로세스가 표시된다
* 또한 컨테이너가 전체 OS를 내장할 필요가 없으므로 매우 가볍고 5~100MB밖에 안된다.


## 도커 컨테이너 격리 방법

* Cgroup(control groups)와 네임스페이스에 대해 알아야한다.
* 다른 프로세스 사이에 벽을 만드는 리눅스 커널 기능들

* C Group(controler groups)
  * CPU, 메모리, Network Bandwith, HD I/O등 프로세스 그룹의 시스템 리소스 사용량 관리 
  * 어떤 앱이 사용량이 너무 많다면 그 앱을 Cgroup에 집어 넣어 CPU와 같은 메모리 사용 제한 가능

* 네임스페이스
  * 하나의 시스템에서 프로세스를 격리시킬 수 있는 가상화 기술
  * 별개의 독립된 공간을 사용하는 것처럼 격리된 환경을 제공하는 경량 프로세스 가상화 기술 


# 이미지로 컨테이너 만들기

* 이미지는 응용프로그램을 실행하는 필요한 모든 것을 포함
  * 컨테이너 시작 명령어
  * 파일 스냅샷(응용프로그램의 스냅샷, 디렉토리나 파일을 카피한 것)

## 이미지로 컨테이너 만드는 순서

1. Docker 클라이언트에 docker run [이미지] 명령어 입력
2. 도커 이미지에 있는 파일 스냅샷을 컨테이너 하드 디스크에 옮ㅇ


## 컨테이너들 나열하기

* ### docker ps 명령어

* CONTAINER ID : 컨테이너 고유한 아이디(해쉬값). 실제로는 더욱 길지만 일부분만 표출.
* IMAGE : 컨테이너 생성시 사용한 도커 이미지명
* COMMAND : 컨테이너 시작시 실행될 명령어. 대부분 이미지에 내장되어 있으므로 별도 설정이 필요 X
* CREATED: 컨테이너 생성된 시간
* STATUS : 컨테이너 상태. 
  * 실행중 : Up
  * 종료 : Exited
  * 일시정지 : Pause.

* PORTS : 컨테이너가 개방한 포트와 호스트에 연결한 포트. 특별한 설정을 하지 않은 경우 출력되지 않는다.
* NAMES : 컨테이너의 고유 이름.
  * 컨테이너 생성시 --name 옵션으로 이름 설정 가능. 설정하지 않으면 임의로 설정 
  * docker rename [원래컨테이너이름] [바꿀컨테이너이름] 으로 변경 가능 

## 실행되지 않은 컨테이너 포함한 모든 컨테이너 나열 명령어
* docker ps -a

# 도커 컨테이너의 생명주기 

* ![](images/d36ae0fd.png)
  * docker run = docker create + docker start (-a옵션)

* ![](images/e0843c96.png)
  * docker stop : 정리하는 시간을 주고 킬 (Grace Period)
  * docker kill : 정리하는 시간 없이 바로 멈추기 

* ![](images/639a1016.png)
  * 중지된 컨테이너 삭제 : docker rm <아이디> 
  * 모든 컨테이너 삭제 : docker rm ``docker ps -a -q``
  * 도커 이미지 삭제 docker rmi <이미지id>
  * 한번에 사용하지 않는 컨테이너, 이미지, 네트워크 모두 삭제 : docker system prune


## 이미 실행중인 컨테이너에 명령어 전달?
* docker exec <컨테이너 아이디>

### docker run vs docker exec
1. docker run은 새로운 컨테이너 만들어서 실행
2. docker exec는 이미 실행중인 컨테이너에 명령어 전달 
  * ex: docker exec <컨테이너아이디> ls 
  * docker run <이미지이름> ls

# 레디스를 이용한 컨테이너 이해

* ![](images/4092ace1.png)

* 먼저 레디스 서버를 실행한 후, 클라이언트를 통해 명령어를 전달해줘야 한다.

1. 먼저 레디스 서버 작동. docker run redis
2. 그 후 다른 터미널로 레디스 클라이언트 작동. redis-cli
* 이러면 에러가 난다. 레디스 클라이언트에서 도커 컨테이너[레디스 서버 동작중인] 접근 불가.(컨테이너 밖이라)
* 해결방법 : 같은 컨테이너 안에서 레디스 클라이언트(redis-cli)를 실행하면된다

3. docker exec -it <컨테이너아이디> redis-cli
  * -i : interactive 
  * -t : terminal
  * it 명령어를 안붙이면 터미널에서 나와진다.  

## 실행중인 컨테이너에 쉘 환경으로 접속
* docker exec -it <컨테이너아이디> sh
* 쉘에서 나오려면 컨트롤 + D 

# 직접 도커 이미지 만들기

* ![](images/9dd1fe45.png)

* 도커 이미지는 Dockerhub에 다른 사람들이 만들어 놓은 것을 이용할 수도 있고, 직접 도커 이미지를 만들어서 사용하거나 도커 허브에 업로드 할 수 있다.


# 도커 파일 만들기 

* 도커 파일이란? 
  * 도커 이미지를 만들기 위한 설정 파일. 컨테이너가 어떻게 행동해야 하는지에 대한 설정들을 정의해 주는곳 

## 도커 파일 만드는 순서 (도커 이미지가 필요한 것이 무엇인지를 생각)

1. 베이스 이미지를 명시해준다. (파일 스냅샷에 해당)
2. 추가적으로 필요한 파일을 다운 받기 위한 몇가지 명령어를 명시해준다.(파일 스냅샷에 해당)
3. 컨테이너 시작시 실행 될 명령어를 명시해준다.(시작시 실행 될 명령어에 해당)

* 도커 파일 이미지 이름 지정
* docker build -t imagename:0.0
* -t 옵션 

### 베이스 이미지

* ![](images/cce9b90e.png)

* ### 예제 : Hello문구 출력하는 도커 이미지 만들기
1. 도커 파일을 만들 폴더 하나 만들기 ex) dockerfile-folder
2. 방금 생성한 도커 파일 폴더를 에디터를 이용해서 실행(vscode 추천)
3. 파일 하나를 생성, 이름은 dockerfile(확장자 없음)
4. 그안에 먼저 어떻게 진행해 나갈지 기본적인 토대를 명시 

5. 베이스 이미지부터 실제 값으로 추가해주기
6. 베이스 이미지는 ubuntu나 centos 등을 써도 되지만 hello출력 기능은 굳이 사이즈가 큰 베이스 이미지를 쓸 필요가 없기에 사이즈가 작은 alpine 베이스 이미지 사용 
7. 컨테이너 시작시 실행될 명령어를 넣어준다.

```docker
# 베이스 이미지 명시
# FROM baseImage
FROM alpine

# 추가적으로 필요한 파일 다운로드
# RUN command


# 컨테이너 시작시 실행될 명령어 명시
# CMD [ "executable" ]
CMD [ "echo", "hello"]
```

* #### 도커파일 명령어
  * FROM : 이미지 생성시 기반이 되는 이미지 레이어 
    * <이미지이름>:<태그> 형식으로 작성
    * 태그를 안붙이면 자동적으로 가장 최신것으로 다운로드. ex) ubuntu:14.04
  * RUN : 도커 이미지가 생성되기 전에 수행할 쉘 명령어
  * CMD : 컨테이너가 시작되었을 떄 실행할 실행 파일 또는 셸 스크립트. 
    * 이 명령어는 Dockerfile내 1회만 쓸 수 있따.  


# 도커파일로 도커 이미지 만들기 

* ![](images/eba2bd12.png)

* 도커 파일에 입력된 것들이 도커 클라이언트에 전달되어서 도커 서버가 인식하게 하여야 한다
* 명령어 : docker build ./ 또는 docker build .

* ![](images/40f6bc1e.png)

* 도커 이미지에 이름주기 
* docker build -t [youngsoo/hello:latest] .
  * 옵션 [-t 나의도커아이디 / 저장소or프로젝트 이름 : 버전 ] 


# 도커를 이용해서 Node.js 어플 만들기
#### https://nodejs.org/fr/docs/guides/nodejs-docker-webapp/

# 생성한 이미지로 어플리케이션 접근이 안되는 이유(포트 맵핑)


* docker run 이미지 이름 
* 에서 다음과 같이 실행한다
* docker run -p 49160:8080 이미지이름 
  * 49160 등 내부 포트는 아무거나 줘도 된다 ( 안쓰는것)
  * 그럼 외부에서 49160 등 앞 포트로 접속하면 된다. 
  * localhost:49160


* ![](images/5068a2cd.png)

# 워크디렉토리 (Working Directory)

* 도커 이미지 안에서 어플리케이션 소스 코드를 갖고 있을 디렉토리를 생성하는 것 

* 현재 만들어놓은 이미지의 Root 디렉토리 보는법
  * docker run -it <이미지이름> 명령어


```shell
FROM node:16

# create app directory
WORKDIR /usr/src/app

# 도커 컨테이너 안에 저장
COPY package.json ./
```
* 
* ![](images/1a869fdb.png)

* 워크 디렉토리를 지정하게 되면, 루트부터 접근하는게 아닌 워크 디렉토리부터 접근하게된다
  *  따라서 명령어도 워크 디렉토리 기반에서부터 시작한다. 

* 워크 디렉토리를 지정하지 않고 그냥 copy할때의 문제점
  * 베이스 이미지에 home이라는 폴더가 있을 시, 새로 추가되는 폴더 이름이 home이라면 중복되서 그냥 덮어씌어져 버린다.
    * 원래 파일 시스템의 중요한 파일과 이름이 같으면 중요한 원래 파일이 날라간다.  
  * 모든 파일이 한 디렉토리에 들어가버리니 정리정돈이 안된다.
  * 예를들어 루트에 다 파일이 몰릴수도 있다.

# 도커 이미지 삭제

* 현재 이미지 확인 : docker images
* 이미지 삭제 : docker rmi [이미지id]
* 컨테이너 삭제 전 이미지 삭제 : docker rmi -f [이미지id]

## 컨테이너 삭제

* 동작중인 컨테이너 확인 : docker ps
* 정지된 컨테이너 확인 : docker ps -a
* 컨테이너 삭제 : docker rm [컨테이너 id]
* 삭제된 것 확인 : docker ps -a
* 복수개 삭제 : docker rm [id1], [id2]
* 컨테이너 모두 삭제 : docker rm `docker ps -a -q`

# 어플리케이션 소스 변경으로 다시 빌드하는법

어플 실행 순서
* 도커파일작성 -> 빌드 -> 도커파일로 이미지 생성 -> run -> 컨테이너 생성후 앱 실행


* 소스코드를 계속 변경시켜 변경 된 부분을 어플리케이션에 반영시킬라면 
  * 이미지 생성부터 다시 실행시켜줘야한다. 

* 그런데 이런식으로 하면 너무 비효율적이다. 
* 그럼 어떻게? 

* ![](images/80842c69.png)

* npm install 할 때 불 필요한 다운로드를 피하기 위해서 이렇게 한다
* 원래 모듈을 다시 받는 것은 모듈에 변화가 생겨야만 다시 받아야 하는데, 소스코드에 조금의 변화만 생겨도 모듈 전체를 다시 받는 문제점이 있다.
> `그러므로 RUN npm install 전 단계에서 COPY 할 때는 오직 module에 관한것만 해주고,  
>  RUN npm install 이후에 다시 모든 파일을 COPY 해준다. 

```shell
FROM node:16

# create app directory
WORKDIR /usr/src/app

# 도커 컨테이너 안에 저장
COPY package.json ./

RUN npm install

# Bundle app source
COPY ./ ./

CMD ["node", "server.js"]
```

# Docker Volume에 대하여 

* 소스를 변경할 때 마다 변경된 소스 부분은 COPY한 후 이미지를 다시 빌드를 해주고 컨테이너를 다시 실행해줘야 변경된 소스가 반영이 된다 
* 이러한 작업은 시간 소요가 크며 이미지도 너무 많이 빌드하기 때문에 VOLUME을 사용한다.
* ![](images/f21d6cd1.png)

## Volume 사용해서 어플리케이션 실행하는법
* ![](images/d39df4cf.png)

* 이렇게 volume을 이용해서 키면 빌드할 때 소스를 바꾸더라도 바꾼 코드가 적용이 된다
* docker run -p 5000:8080 -v /usr/src/app/node_modules -v $(pwd):/usr/src/app <이미지이름>
  * /usr/src/app 이건 dockerfiled의 workdir

* 이러면, 도커 이미지를 빌드하지 않고 run만 해도 바꾼 코드가 적용이 된다. 


# 도커 compose

* docker compose는 다중 컨테이너 도커 애플리케이션을 정의하고 실행하기 위한 도구 

* 실행 명령어 : docker-compose up 
* 