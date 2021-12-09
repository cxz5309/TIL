# Docker란

> Docker는 애플리케이션을 신속하게 구축, 테스트 및 배포할 수 있는 소프트웨어 플랫폼입니다. Docker는 소프트웨어를 컨테이너라는 표준화된 유닛으로 패키징하며, 이 컨테이너에는 라이브러리, 시스템 도구, 코드, 런타임 등 소프트웨어를 실행하는 데 필요한 모든 것이 포함되어 있습니다. Docker를 사용하면 환경에 구애받지 않고 애플리케이션을 신속하게 배포 및 확장할 수 있으며 코드가 문제없이 실행될 것임을 확신할 수 있습니다.
![도커 개념](/public/JS/docker1.png)  

## 특징
![도커 가상화](/public/JS/docker2.png)  
- 가상화 방식을 이용한(하지만 os 자체를 가상화하지는 않는) 가상화 서비스로 컨테이너를 이용하여 프로세스를 격리하여 실행시킨다. 기존 가상화 방법에 비해 기존의 컴퓨터 자원의 손실이 거의 없다는 점이 매우 큰 차이이다.  
- 하나의 서버에 여러 개의 컨테이너를 통해 독립적으로 실행되며 새로운 컨테이너를 만드는데 1초도 되지 않는다. 이 특징은 도커의 핵심 기능 중 하나인 플랫폼간의 빠르고 원활한 이전이 가능케 한다.
- 도커는 특징적인 개념으로 이미지가 있는데 컨테이너 실행에 필요한 파일과 설정값 등을 포함하며 상태값을 가지지 않는다.
- 이미 Docker Hub에는 수많은 주요 이미지들이 등록되어 있고 필요한 경우 사용하기만 하면 된다! 내가 필요한 경우 스스로 이미지를 만들고 배포도 가능하여 컨테이너 구축의 속도를 획기적으로 상승시켰다.
- 이미지를 설치하는 방식은 여러 개의 이미지를 다운받았을 때 용량 면에서 문제가 생긴다. 하지만 도커는 이 문제를 해결하기 위해 레이어라는 개념을 도입했다. 이미지는 여러 개의 레이어로 되어 있고 유니온 파일 시스템을 이용하여 여러 레이어를 하나의 파일 시스템으로 사용할 수 있게 되었다. 
- 레이어를 통해서 새 이미지를 받을 때 기존에 있던 레이어를 사용한다면 추가된 레이어만을 받으면 되게 되었다.

## 장점
1. 더 많은 소프트웨어를 더 빨리 제공
   - Docker 사용자는 평균적으로 Docker를 사용하지 않는 사용자보다 7배 더 많은 소프트웨어를 제공합니다. Docker를 사용하면 필요할 때마다 격리된 서비스를 제공할 수 있습니다.
2. 운영 표준화
   - 작은 컨테이너식 애플리케이션을 사용하면 손쉽게 배포하고, 문제를 파악하고, 수정을 위해 롤백할 수 있습니다.
3. 원활하게 이전
   - Docker 기반 애플리케이션을 로컬 개발 시스템에서 AWS의 프로덕션 배포로 원활하게 이전할 수 있습니다.
4. 비용 절감
   - Docker 컨테이너를 사용하면 각 서버에서 좀 더 쉽게 더 많은 코드를 실행하여 사용률을 높이고 비용을 절감할 수 있습니다.

## DockerFile
- 도커에는 DockerFile이라는 설정 파일이 필요하다. 도커 이미지를 생성하는 과정을 적는데 간단하며 획기적인 방법이다.
![도커 이미지](/public/JS/docker3.jpg)
## DockerFile 커맨드
### FROM
하나의 Docker 이미지는 base 이미지부터 시작해서 기존 이미지위에 새로운 이미지를 중첩해서 여러 단계의 이미지 층(layer)을 쌓아가며 만들어진다.  
FROM 명령문은 이 base 이미지를 지정해주기 위해서 사용되는데, 보통 Dockerfile 내에서 최상단에 위치한다. base 이미지는 일반적으로 Docker Hub와 같은 Docker repository에 올려놓은 잘 알려진 공개 이미지인 경우가 많다.  
```
FROM <이미지>
FROM <이미지>:<태그>
```
```
FROM ubuntu:latest
```
```
FROM node:12
```
### WORKDIR
WORKDIR 명령문은 쉘(shell)의 cd 명령문처럼 컨테이너 상에서 작업 디텍토리로 전환을 위해서 사용된다.   WORKDIR 명령문으로 작업 디렉터리를 전환하면 그 이후에 등장하는 모든 RUN, CMD, ENTRYPOINT, COPY, ADD 명령문은 해당 디렉터리를 기준으로 실행된다.  
```
WORKDIR <이동할 경로>
```
```
WORKDIR /app
```

### RUN
RUN 명령문은 이미지 빌드 과정에서 필요한 커맨드를 실행하기 위해서 사용된다. 보통 이미지 안에 특정 소트트웨어를 설치하기 위해서 많이 사용된다.  

```
RUN ["<커맨드>", "<파라미터1>", "<파라미터2>"]
RUN <전체 커맨드>
```
- curl 도구 설치
```
RUN apk add curl
```
- npm 패키지 설치
```
RUN npm install --silent
```
### ENTRYPOINT 
ENTRYPOINT 명령문은 이미지를 컨테이너로 띄울 때 항상 실행되야 하는 커맨드를 지정할 때 사용한다.  ENTRYPOINT 명령문은 Docker 이미지를 마치 하나의 실행 파일처럼 사용할 때 유용하다. 왜냐하면 컨테이너가 뜰 때 ENTRYPOINT 명령문으로 지정된 커맨드가 실행되고, 이 커맨드로 실행된 프로세스가 죽을 때, 컨테이너로 따라서 종료되기 때문이다.  
```
ENTRYPOINT ["<커맨드>", "<파라미터1>", "<파라미터2>"]
ENTRYPOINT <전체 커맨드>
```
```
ENTRYPOINT ["npm", "start"]
```
### CMD 
CMD 명령문은 해당 이미지를 컨테이너로 띄울 때 디폴트로 실행할 커맨드나, ENTRYPOINT 명령문으로 지정된 커맨드에 디폴트로 넘길 파라미터를 지정할 때 사용한다.  
CMD 명령문은 대부분 ENTRYPOINT 명령문과 함께 사용하게 되는데, ENTRYPOINT 명령문으로는 커맨드를 지정하고 CMD 명령문으로 디폴트 파리미터를 지정해주면 매우 유연하게 이미지를 실행할 수 있게 된다.  
```
ENTRYPOINT ["node"]
CMD ["index.js"]
```
- 다음과 같이 docker run 커맨드의 인자 유무에 따라 node 커맨드로 다른 파일이 실행되게 할 수 있다.  
- node index.js 실행  
```
$ docker run test
```
- node main.js 실행
```
$ docker run test main.js
```

CMD 명령문과 RUN 명령문이 햇갈릴 수가 있는데, RUN 명령문은 이미지 빌드 시 항상 실행되며, 한 Dockerfile에 여러 개의 RUN 명령문을 선언할 수 있다.   
반면에, CMD 명령문은 이미지를 continaer로 띄울 때 딱 한 번 실행 기회를 가지게 되며, 이 기회마저도 docker run 커맨드에 인자를 넘길 경우 상실하게 된다.  

### EXPOSE 
EXPOSE 명령문은 네트워크 상에서 컨테이너로 들어오는 트래픽(traffic)을 리스닝(listening)하는 포트와 프로토콜를 지정하기 위해서 사용된다.   
프로토콜은 TCP와 UDP 중 선택할 수 있는데 지정하지 않으면 TCP가 기본값으로 사용된다.  
EXPOSE 명령문으로 지정된 포트는 해당 컨테이너의 내부에서만 유효하며, 호스트(host) 컴퓨터에서는 이 포트를 바로 접근을 할 수 있는 것은 아니다.   
호스트 컴퓨터로부터 해당 포트로의 접근을 허용하려면, docker run 커맨드를 -p 옵션을 통해 호스트 컴퓨터의 특정 포트를 포워딩(forwarding)시켜줘야 한다.  
```
EXPOSE <포트>
EXPOSE <포트>/<프로토콜>
```
- 80/TCP 포트로 리스닝
```
EXPOSE 80
```

### COPY/ADD
COPY 명령문은 호스트 컴퓨터에 있는 디렉터리나 파일을 Docker 이미지의 파일 시스템으로 복사하기 위해서 사용된다. 절대 경로와 상대 경로를 모두 지원한다.

```
COPY <src>... <dest>
COPY ["<src>",... "<dest>"]
```
- 이미지를 빌드한 디렉터리의 모든 파일을 컨테이너의 app/ 디렉터리로 복사
```
WORKDIR app/
COPY . .
```

ADD 명령문은 좀 더 파워풀한 COPY 명령문이라고 생각할 수 있다.   
ADD 명령문은 일반 파일 뿐만 아니라 압축 파일이나 네트워크 상의 파일도 사용할 수 있다.   
이렇게 특수한 파일을 다루는 게 아니라면 COPY 명령문을 사용하는 것이 권장된다.  

### ENV 
ENV 명령문은 환경 변수를 설정하기 위해서 사용한다. ENV 명령문으로 설정된 환경 변수는 이미지 빌드 시에도 사용됨은 물론이고, 해당 컨테이너에서 돌아가는 애플리케이션도 접근할 수 있다.

```
ENV <키> <값>
ENV <키>=<값>
```
- NODE_ENV 환경 변수를 production으로 설정
```
ENV NODE_ENV production
```

### ARG 
ARG 명령문은 docker build 커맨드로 이미지를 빌드 시, --build-arg 옵션을 통해 넘길 수 있는 인자를 정의하기 위해 사용한다.
```
ARG <이름>
ARG <이름>=<기본 값>
```
- 예를 들어, Dockerfile에 다음과 같이 ARG 명령문으로 port를 인자로 선언해주면,
```
ARG port
```
- 다음과 같이 docker build 커맨드에 --build-arg 옵션에 port 값을 넘길 수가 있다.
```
$ docker build --build-arg port=8080 .
```
- 인자의 디폴트값을 지정해주면, --build-arg 옵션으로 해당 인자가 넘어오지 않았을 때 사용된다.
```
ARG port=8080
```
- 설정된 인자 값은 다음과 같이 ${인자명} 형태로 읽어서 사용할 수 있다.
```
CMD start.sh -h 127.0.0.1 -p ${port}
```

</br>

- 실제 프로젝트에서 사용된 DockerFile
```
FROM node:14

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 8080

CMD ["npm", "start"]
```
## .dockerignore 
Docker 이미지를 빌드할 때 제외 시키고 싶은 파일이 있다면, .dockerignore 파일에 추가해주면 된다.
Docker는 프로젝트 최상위 디렉터리에 위치하고 있는 설정된 파일들을 무사하게 되므로, RUN과 CMD, COPY와 같은 명령문이 해당 파일을 사용할 수 없게 됩니다.
- .dockerignore
```
.git
*.md
```
- 실제 프로젝트에서 사용된 .dockerignore
```
node_modules
npm-debug.log
.git
```

## Docker Compose
흔히 하나의 컨테이너가 하나의 애플리케이션을 담당한다고 하면 여러 개의 컨테이너가 필요로 한다. 이때 필요한 기술이 도커 컴포즈(Docker Compose)이다.  
도커 컴포즈는 yaml 포맷으로 작성되며 여러 개의 컨테이너의 실행을 한 번에 관리를 할 수 있게 해 준다.  
1. docker-compose.yml
```
version: "3"
services:
  echo:
    image: example/echo:latest
    ports:
      - 9000:8080
```
- version
docker-compose.yml 내용을 해석하기 위한 문법 버전 - 3 버전은 안전 버전입니다.
- echo
services 아래의 echo는 컨테이너 이름입니다. 즉, echo는 하나의 컨테이너입니다.
- image
도커 이미지
- ports
포트 포워딩
2. 도커 컴포즈 실행
```
docker-compose up
```
-d 옵션을 주고 백그라운드에서 실행을 시킬 수도 있다.
```
docker-compose up -d
```
3. 도커 컴포즈 리스트
```
docker-compose ls
```
4. 도커 컴포즈 종료
yml파일에 명시된 컨테이너들은 down 명령어를 통해서 한 번에 종료시킬 수 있다. 
```
docker-compose down
```


> 출처  
> https://aws.amazon.com/ko/docker/  
> https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html  
> https://www.daleseo.com/dockerfile/  
> https://junlab.tistory.com/219