# AWS CodePipeline

> AWS CodePipeline은 빠르고 안정적인 애플리케이션 및 인프라 업데이트를 위해 릴리스 파이프라인을 자동화하는 데 도움이 되는 완전관리형 지속적 전달 서비스입니다. CodePipeline은 코드 변경이 발생할 때마다 사용자가 정의한 릴리스 모델을 기반으로 릴리스 프로세스의 빌드, 테스트 및 배포 단계를 자동화합니다. 따라서 기능과 업데이트를 신속하고 안정적으로 제공할 수 있습니다. AWS CodePipeline을 GitHub 또는 자체 사용자 지정 플러그인과 같은 타사 서비스와 손쉽게 통합할 수 있습니다. AWS CodePipeline에서는 사용한 만큼만 비용을 지불합니다. 선결제 금액이나 장기 약정이 없습니다.

- AWS의 CI/CD 툴로써 AWS CodeCommit, AWS CodeBuild, AWS CodeDeploy를 파이프라인처럼 하나로 연결시켜 관리를 도와준다.
- CodeCommit 등은 GitHub로 대체되기도 하고 CodeBuild 단계를 스킵하거나 새로운 단계를 추가하는 등 유연한 설계가 가능하다.
- 프리티어에서 활성 파이프라인 1개가 무료이고 사용한 만큼 비용을 지불한다. (하지만 CodeBuild에서 미친듯이 까먹게 된다는건 안써져있다.)  


<img src="https://user-images.githubusercontent.com/42149645/145908600-c966f4b9-6117-4f79-838e-ae321dd699a0.PNG" alt="codepipeline1" width="800" height="auto"/>

## 1. 기본 설정

<img src="https://user-images.githubusercontent.com/42149645/145908654-9f824f99-7a22-40b5-b74f-f4b96bcf26ed.PNG" alt="codepipeline2" width="800" height="auto"/>

- 기본적인 파이프라인 이름을 설정해준다. 
- iam 서비스 역할도 연결시켜야하는데 파이프라인 생성시 맞춤 역할을 생성해줄 수 있어 그 방법으로 하였다.(너무 많이 하면 과하게 많아지므로 설정해 두는 것을 권장)  

## 2. CodeCommit


<img src="https://user-images.githubusercontent.com/42149645/145908658-150b9066-6822-4635-b199-9a82cbf238a4.PNG" alt="codepipeline3" width="800" height="auto"/>    

- CodeCommit 단계. AWS는 CodeCommit을 사용하는 방법을 권장하지만 대부분 깃허브를 사용하기 때문에 Github(버전2)를 사용하면 된다. 

<img src="https://user-images.githubusercontent.com/42149645/145908663-75ade4d1-6c97-4e05-943c-8b9752035f5a.PNG" alt="codepipeline4" width="800" height="auto"/>       

- 깃허브에 연결을 누르면 깃허브 설정을 클릭만으로 알아서 해준다.  

## 3. CodeBuild

<img src="https://user-images.githubusercontent.com/42149645/145908665-440c3fc9-cd8c-49a8-85e4-c46879eca569.PNG" alt="codepipeline5" width="800" height="auto"/>        

- CodeBuilde단계. 빌드한 프로젝트의 환경 설정, 환경변수 등을 설정한다. 

<img src="https://user-images.githubusercontent.com/42149645/145908665-440c3fc9-cd8c-49a8-85e4-c46879eca569.PNG" alt="codepipeline6" width="800" height="auto"/>        

<img src="https://user-images.githubusercontent.com/42149645/145908677-ad826c51-95a9-4c68-944c-cbc33dd1c13c.PNG" alt="codepipeline7" width="800" height="auto"/>        

<img src="https://user-images.githubusercontent.com/42149645/145908680-2314de13-bec0-41f1-9729-23532a9927d2.PNG" alt="codepipeline8" width="800" height="auto"/>        

### 환경
- 사용하는 운영체제 타입을 고를 수 있으며 리눅스와 우분투가 기본이다. 도커 이미지 지정을 사용할 경우 리눅스가 고정이며 도커 이미지를 사용할 경우 권한이 있음을 눌러 권한을 주어야 한다.  
- 혹시라도 현재 사용중인 ec2 운영체제 타입이 안맞을 경우 문제가 생긴다.  
- 그 외에 빌드 제한시간, 인증서, vpc, 환경변수 등을 추가로 선택할 수 있다. 환경변수는 빌드와 배포 단계에서 함께 쓰기 위해(앱 단에서 test와 product 환경변수를 라우팅함) ecs에서 적용시켰다.
### buildspec
- 가장 중요한 빌드 설정. 빌드 단계에 들어오면 프로젝트 루트에 buildspec.yaml을 자동으로 찾아 사용하거나 현재 화면에서 명령을 삽입할 수 있다. 
- buildspec 명령어는 yaml 명령어를 사용하는데 빌드 각 단계당 실행 명령어, artifact 설정을 하면 된다.
- ec2 단일 서버 CodeBuild, nodejs
```
version: 0.2

# Linux 사용자만 사용할 수 있습니다.이 buildspec 파일의 명령을 실행하는 Linux 사용자를 지정합니다.run-as를 지정하지 않으면 모든 명령이 root로 실행됩니다.
# 필수 시퀀스입니다. 빌드의 각 단계 동안 CodeBuild가 실행하는 명령을 나타냅니다
phases:
  # 설치 중에 CodeBuild가 실행하는 명령을 나타냅니다. 빌드 환경에서 패키지를 설치하는 경우에만 install 단계를 사용하는 것이 좋습니다. 예를 들어, Mocha나 RSpec 같은 코드 테스팅 프레임워크를 설치하기 위해 이 단계를 사용할 수 있습니다.
  install:
    runtime-versions:
      nodejs: 14
    commands:
      - echo Insatlling NPM Packages and wget Enviorment File
  # 빌드 전에 CodeBuild가 실행하는 명령을 나타냅니다. 예를 들어, Amazon ECR에 로그인하기 위해 이 단계를 사용할 수 있습니다. 또는 npm 종속성을 설치할 수도 있습니다.
  pre_build:
    commands:
      - npm install
      - echo npm installed
    commands:
      - echo Build started on `date`
  # 빌드 후에 CodeBuild가 실행하는 명령을 나타냅니다(있는 경우). 예를 들어, Maven을 사용하여 빌드 결과물을 JAR 또는 WAR 파일에 패키지할 수 있으며, Amazon ECR에 Docker 이미지를 푸시할 수도 있습니다.
  build:
    commands:
      - npm run test
  post_build:
    commands:
      - echo Build started on `date`
# CodeBuild가 빌드 출력을 찾을 수 있는 위치 및 CodeBuild가 Amazon S3 출력 버킷에 업로드하기 위해 빌드 출력을 준비하는 방식에 대한 정보를 나타냅니다.
artifacts:
  # 빌드 환경의 빌드 출력 결과물을 포함하는 위치를 나타냅니다.
  files:
    - "**/*"
```  
- ecs는 docker를 이용하기 때문에 조금 다른 설정이 필요하다.
- ecs, docker 컴퓨팅, ecr로 전송
```
version: 0.2

phases:
  pre_build:
    commands:
      - aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin 303022694345.dkr.ecr.ap-northeast-2.amazonaws.com
  build:
    commands:
      - docker build --tag mingijuk-ecr .
      - docker tag mingijuk-ecr:latest 303022694345.dkr.ecr.ap-northeast-2.amazonaws.com/mingijuk-ecr:latest
  post_build:
    commands:
      - echo Build started on `date`
      - echo Pushing docker image
      - docker push 303022694345.dkr.ecr.ap-northeast-2.amazonaws.com/mingijuk-ecr:latest
      - printf '{"name":"%s","imageUri":"%s"}' mingijuk-ecr 303022694345.dkr.ecr.ap-northeast-2.amazonaws.com/mingijuk-ecr:latest > imageDetail.json
artifacts:
  files:
    - imageDetail.json
    - appspec.yaml
    - taskdef.json
```
### 로그
- CloudWatch 로그 또는 s3로그를 선택할 수 있는데 사용성에서 CloudWatch 로그를 권장하고 로그를 아무것도 선택하지 않는건 빌드 실패 원인을 찾기 힘들기 때문에 매우 권장하지 않는다.
## 4. CodeDeploy

- CodeDeploy 단계, 다양한 배포 공급자를 고를 수 있는데 CodeDeploy선택 전에 CodeDeploy로 가서 미리 애플리케이션과 배포 그룹을 생성하고 와야 한다.  

<img src="https://user-images.githubusercontent.com/42149645/145908681-cb2e6d8e-5bc7-4ffa-92e0-73fdc77b7749.PNG" alt="codepipeline9" width="800" height="auto"/>      

- 애플리케이션은 ec2, lambda, ecs 중 선택 가능한데 ecs는 ecs에서 설정 시 자동으로 만들어주기 때문에 할 필요가 없다.  

<img src="https://user-images.githubusercontent.com/42149645/145908684-42377eee-e09b-4b0f-ba35-b8a52eb1f19d.PNG" alt="codepipeline10" width="800" height="auto"/>      

<img src="https://user-images.githubusercontent.com/42149645/145908685-ff2dfaa4-89cd-4ad8-b598-5a10812d3cc1.PNG" alt="codepipeline11" width="800" height="auto"/>      

<img src="https://user-images.githubusercontent.com/42149645/145908697-db7609c6-11fb-4c4e-81b4-0c87573ad274.PNG" alt="codepipeline12" width="800" height="auto"/>      

- 이후 배포 그룹을 생성해야 한다 
### 서비스 역할
- 서비스의 역할 iam을 선택한다. 자동 생성이 아니므로 직접 만들어서 권한을 주어야 하며 이후 배포 파일이 어디를 액세스 해야 하는지, 어떤 권한이 필요한지 잘 선택하지 않으면 빌드 오류가 발생한다.
### 배포 유형
- 기본과 블루/그린이 있는데 블루/그린 배포를 하게 되면 ec2 인스턴스가 최소 2개 필요하며 그룹 설정을 따로 해주어야 한다.
### 환경 구성
- Auto Scaling도 마찬가지로 인스턴스를 추가하여 Scale up을 동적으로 해준다. ec2 인스턴스를 ec2 name 등의 키로 찾을 수 있기 때문에 ec2에 이름 설정을 해주면 좋다.
### 배포 설정
### 로드밸런서
- 로드밸런서 설정을 해줄 수 있다. 로드밸런서도 미리 만들어주어야 설정이 가능하다.

<img src="https://user-images.githubusercontent.com/42149645/145908699-d0fc6d14-881e-4141-9cb3-2f69b37a3489.PNG" alt="codepipeline13" width="800" height="auto"/>      

- 현재 ecs로 연결된 배포 설정으로 블루/그린 배포를 위해 로드밸런서를 설정해주었다. 

### appspec.yaml
- 빌드와 동일하게 배포에도 설정 파일이 필요한데 appspec.yaml 파일을 통해 설정한다.
- ecs에서는 이미지파일 설정인 taskdef.json 파일도 필요하다.

---

- ec2 단일 서버, nodejs 환경, pm2로 실행, appspce.yaml
```
version: 0.0
os: linux
files:
  - source: /
    destination: /home/ubuntu/mingijuk
    file_exists_behavior: OVERWRITE
hooks:
  ApplicationStop:
    - location: /code_deploy/application_stop.sh
      timeout: 500
  BeforeInstall:
    - location: /code_deploy/before_install.sh
      timeout: 500
  ApplicationStart:
    - location: /code_deploy/application_start.sh
      timeout: 500
```
각 단계마다 설정 파일의 위치를 추가로 정할 수 있다.
- /code_deploy/application_stop.sh
```
npm uninstall -g pm2

if pgrep node; 
then pkill node; 
fi
```
- /code_deploy/before_install.sh
```
#!/bin/bash

# EC2 서버에 node와 nvm 설치하기
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
. ~/.nvm/nvm.sh
nvm install node

# EC2 서버 작업 폴더 확인
DIR="/home/ubuntu/mingijuk"

if [ -d "$DIR" ]; then
  echo folder exists
else 
  mkdir ${DIR}
fi

sudo rm -rf /home/ubuntu/mingijuk/node_modules
# 한국 시간(KST) 으로 Timezone 변경
sudo rm -rf /etc/localtime
sudo ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime
```
- /code_deploy/application_start.sh 
```
#!/bin/bash

# EC2 서버에 node와 nvm 설치하기
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
. ~/.nvm/nvm.sh
nvm install node

# 밍기적 폴더 권한 추가
sudo chmod -R 777 /home/ubuntu/mingijuk
cd /home/ubuntu/mingijuk

# npm과 node 설치
export NVM_DIR="$HOME/.nvm"	
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # loads nvm	
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # loads nvm bash_completion (node is in path now)


# node_modules 설치
npm install
echo "npm installed"

#PM2 설치
npm install -g pm2
echo "pm2 installed"

# node 어플리케이션 background에서 실행시키기 (by doing so, the server won't be terminated due to inactivates)
# node app.js 만 입력시 foreground로 실행이 됌
# node dist/app.js > app.out.log 2> app.err.log < /dev/null & 
pm2 start NODE_ENV=production node server.js
pm2 save
```

---

- ecs 블루/그린 배포, https 포트포워딩 ecr에서 이미지 가져오기, nodejs환경, appspce.yaml
```
version: 0.0
Resources:
  - TargetService:
      Type: AWS::ECS::Service
      Properties:
        TaskDefinition: <TASK_DEFINITION>
        LoadBalancerInfo:
          ContainerName: "mingijuk-ecr"
          ContainerPort: 8080
```
- taskdef.json (중요 정보가 많아 자습서로 대체함)
```
{
    "executionRoleArn": "arn:aws:iam::account_ID:role/ecsTaskExecutionRole",
    "containerDefinitions": [
        {
            "name": "sample-website",
            "image": "<IMAGE1_NAME>",
            "essential": true,
            "portMappings": [
                {
                    "hostPort": 80,
                    "protocol": "tcp",
                    "containerPort": 80
                }
            ]
        }
    ],
    "requiresCompatibilities": [
        "FARGATE"
    ],
    "networkMode": "awsvpc",
    "cpu": "256",
    "memory": "512",
    "family": "ecs-demo"
}
```

> 출처
> https://aws.amazon.com/ko/codepipeline/