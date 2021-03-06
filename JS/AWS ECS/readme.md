# AWS ECS(Elastic Container Service)

> Amazon ECS는 컨테이너화된 애플리케이션의 손쉬운 배포, 관리 및 크기 조정을 지원하는 완전관리형 컨테이너 오케스트레이션 서비스입니다.  


![ecs1](/public/JS/ecs1.png)   

- ECR(Elastic Container Registry)에서 이미지를 읽은 후 ECS(Elastic Container Service)에서 관리한다. 
- ECS에 있는 각각의 어플리케이션들은 ECS로 관리되어 가용성, 리전 관리, 배치처리 등의 컴퓨팅이 손쉽게 가능해진다.

---

## 기능
- 핵심 기능
  - AWS Fargate를 통한 기본적인 서버리스: AWS Fargate는 서버리스이므로 서버 관리, 용량 계획 처리 또는 보안을 위한 컨테이너 워크로드 격리에 이점이 있다.
  - Amazon ECS Anywhere: ECS Anywhere를 사용하면 익숙한 Amazon ECS 콘솔 및 운영자 도구를 사용하여 온프레미스 컨테이너 워크로드를 관리할 수 있으므로 컨테이너 기반 애플리케이션 전체에서 일관된 경험을 얻을 수 있다. AWS Systems Manager(SSM)를 통합하면 온프레미스 하드웨어와 AWS 제어 플레인 간의 신뢰가 자동으로 안전하게 설정된다.
  - 보안 및 격리: Amazon ECS는 이미 신뢰하는 보안, 자격 증명 및 관리와 거버넌스 도구와 기본적으로 통합되므로 프로덕션으로 빠르게 전환하는 데 도움이 된다. 각 컨테이너에 대한 세분화된 권한을 할당하여 애플리케이션을 구축할 때 격리 수준을 개선할 수 있다. 
  - 자율적인 제어 플레인 작업: Amazon ECS는 제어 플레인, 노드 또는 추가 기능을 관리할 필요가 없는 완전관리형 컨테이너 오케스트레이션 서비스이다. AWS와 서드 파티 도구에 기본적으로 통합되므로 환경이 아닌 애플리케이션을 구축하는 데 집중할 수 있다.
- 개발
  - Docker 지원
  - Windows 컨테이너 호환
  - AWS Copilot : Amazon ECS 및 AWS Fargate에서 프로덕션 준비 컨테이너식 애플리케이션을 구축, 릴리스 및 운영하는 데 사용되는 개발자용 도구
  - 리포지토리 지원(ECR)
- 관리
  - 태스크 정의
  - 프로그래밍 방식 제어
  - 컨테이너 배포 : Amazon ECS는 연결된 Application Load Balancer에 자동으로 컨테이너를 등록하고 등록 취소합니다.
  - 블루/그린 배포 : 애플리케이션 업데이트 중에 가동 중단 시간을 최소화하는 데 도움이 됩니다. 트래픽을 다시 라우팅하기 전에 새로운 버전의 Amazon ECS 서비스를 기존 버전과 함께 시작하고 새로운 버전을 테스트할 수 있습니다. 또한 배포 프로세스를 모니터링하고 문제가 발생할 경우 신속하게 롤백할 수 있습니다.
  - 컨테이너 자동 복구
  - Capacity Providers : 태스크 및 서비스를 실행할 때 Fargate 및 Fargate Spot 용량에 걸쳐 미리 정의된 분할 비율로 서비스를 실행하는 것과 같은 새로운 기능을 활성화하여 여러 용량 공급자에 태스크 및 서비스를 분할할 수 있습니다.
  - 스토리지(EFS)
- 일정 예약 및 태스크 배치
  - 작업 일정 예약
  - 서비스 일정 예약
  - 데몬 일정 예약
  - 태스크 배치
- 네트워킹
  - 서비스 검색(AWS Cloud Map) : AWS Cloud Map은 애플리케이션 리소스에 대한 사용자 지정 이름을 정의할 수 있는 클라우드 리소스 검색 서비스입니다. 웹 서비스에서 항상 이 동적으로 변화하는 리소스의 최신 위치를 검색하므로 애플리케이션 가용성이 개선됩니다.
  - 서비스 메시
  - 태스크 네트워킹
  - 로드 밸런싱 : Amazon ECS는 Elastic Load Balancing과 통합되므로 Application Load Balancer 또는 Network Load Balancer를 사용하여 컨테이너에 트래픽을 분산할 수 있습니다. 
- 모니터링 및 로깅
  - 모니터링(Amazon CloudWatch)
  - 로깅(AWS CloudTrail)
  - AWS Config
- 하이브리드 배포
  - AWS Outposts

---
### 정리

- 완전관리형 컨테이너 오케스트레이션 툴이다
- 쿠버네티스보다 쉽고 aws 서비스에 대한 연결이 간단하며 aws로 모든 기능이 다 있다 보니까 간단하게 사용하기 쉽다.(그러나 돈이 나간다)
- fargate라는 서버리스 환경을 권장한다. fargate는 ec2에 비해 서버 용량 문제 등에서 자유로우며 기본적인 제공도 훌륭하다. 자습서도 대부분 이 환경이다. (그러나 돈이 나간다. 게다가 돈 안드는 ec2환경은 자습서가 적어 생각보다 어렵다..)
- ECR이라는 컨테이너 이미지 스토리지를 지원한다. 보기가 쉽게 되어 있어 사용성이 좋다..?(그러나 돈이 나간다.)
- AWS ELB(Elastic Load Balancer)를 사용한다. 컨테이너 오케스트레이션 특성상 로드밸런서는 필수이다. 
- AutoScaling이 쉽다. Capacity Providers는 먼저 원하는 작업 수를 실행하는 데에 필요한 리소스와 그에 맞는 인스턴스 수를 계산한다. 그리고 현재 돌고 있는 인스턴스 수와 비교하여 인스턴스 수를 조정하는 방식으로 인프라를 관리한다.  
- 완전관리형 오케스트레이션이므로(돈이 드므로) 다른 기본적인 기능들도 당연히 지원한다. 일정관리, 모니터링, 로깅, 보안 등 많은 기능들을 쉽게 사용 가능하다.


---

## 1. ECS 클러스터 생성
<img src="https://user-images.githubusercontent.com/42149645/145917580-4f501cb8-c85a-4222-b319-bd08c50db9ad.PNG" alt="ecs2" width="800" height="auto"/>      

<img src="https://user-images.githubusercontent.com/42149645/145917585-c4efed42-1910-4891-843b-e51a86de388c.PNG" alt="ecs3" width="800" height="auto"/>      

<img src="https://user-images.githubusercontent.com/42149645/145917587-18f6267e-b190-48f8-8228-4c5a13634cd0.PNG" alt="ecs4" width="800" height="auto"/>      

<img src="https://user-images.githubusercontent.com/42149645/145917589-79e6dff1-1b3c-4d4e-8dd8-3b780ef5bcf4.PNG" alt="ecs5" width="800" height="auto"/>      

- 첫 클러스터를 생성하게 되면 템플릿을 고를 수 있다. 
- 각각 fargate 인스턴스, ec2 리눅스 인스턴스, ec2 윈도우 인스턴스를 사용할 수 있다. 
- fargate와 윈도우를 고를 수 있다는 점이 ecs의 주요 장점이란다. (돈이 나간다)
### 클러스터 구성
- 클러스터 이름, 빈 클러스터 확인을 한다. 빈 클러스터 생성시 빈 클러스터가 생성되는데 ecs에서 자동으로 만들어주는 설정과 기능들을 스킵하니 사용하지 않는다.
### 인스턴스 구성
- 프로비저닝 모델: 정기결제 방식 선택이다. 당연히 정기결제 방식이 더 싸야 되는데 나는 그만큼도 사용할 예정이 없어서 온디맨드를 선택했다.
- ec2 인스턴스 유형: 프리티어 무료 버전인 t2.micro를 선택했다.
### 네트워킹 
- vpc를 자동으로 생성해준다. vpc는 여러 개의 인스턴스를 묶어 독립된 네트워크처럼 사용할 수 있게 하는 것으로 하나의 리전에 종속된다. 보안을 위해 사용하며 vpc간 통신을 위해 aws에서는 vpc 피어링 서비스를 제공한다.  

> [VPC란?](https://medium.com/harrythegreat/aws-%EA%B0%80%EC%9E%A5%EC%89%BD%EA%B2%8C-vpc-%EA%B0%9C%EB%85%90%EC%9E%A1%EA%B8%B0-71eef95a7098)  

- ecs의 장점으로 인스턴스를 미리 만들지 않아도 ecs생성 시 인스턴스를 생성하고 각각의 vpc를 자동으로 연결시켜준다. 동일한 vpc끼리는 쉽게 사용이 가능하고 따라서 단일 계정으로 ecs를 사용하는 것이 추가 설정이 없어 편하다. 
### 컨테이너 인스턴스 IAM 역할
- ecs에서 사용할 iam역할을 선택한다. 새 역할 생성을 선택하면 알아서 맞는 iam역할을 만들어주므로 매우 편하다.
### CloudWatch 컨테이너 인사이트
- 로그보려면 해야한다. 모니터링과 경보 생성 등 다양한 기능을 해주므로 꽤 중요하다.  

### 클러스터 생성

<img src="https://user-images.githubusercontent.com/42149645/145917594-5d5a8a2d-109c-421e-8b9e-ce40adeefe51.PNG" alt="ecs6" width="800" height="auto"/>      

<img src="https://user-images.githubusercontent.com/42149645/145917595-d933be07-40bf-4f4a-834f-99d8a68336db.PNG" alt="ecs7" width="800" height="auto"/>      

전부 마무리하게 되면 이 화면이 뜨고 클러스터를 확인할 수 있게 된다.  

<img src="https://user-images.githubusercontent.com/42149645/145917597-76085d95-4898-447d-8f48-f84dd2a2d719.PNG" alt="ecs8" width="800" height="auto"/>      

ec2 인스턴스도 자동으로 생성해준다.

---

## 2. 작업 정의

<img src="https://user-images.githubusercontent.com/42149645/145917599-049dfc7b-fba9-4f19-a736-3c4506a8a0b1.PNG" alt="ecs9" width="800" height="auto"/>      

- ecs와 내부 인스턴스를 생성했지만 아직 사실상 사용하고 있지는 않다. 실제 서비스는 작업 정의를 통해서 작업을 만들어주어야 한다.

<img src="https://user-images.githubusercontent.com/42149645/145917600-d6f4d8fe-2d92-48d5-9297-37d2748dda1e.PNG" alt="ecs10" width="800" height="auto"/>      

- 각 인스턴스에 맞는 시작 유형을 선택할 수 있다. 당연히 ec2를 선택했다.

<img src="https://user-images.githubusercontent.com/42149645/145917602-4e829e7e-d405-45af-b744-2a21a9250320.PNG" alt="ecs11" width="800" height="auto"/>      

<img src="https://user-images.githubusercontent.com/42149645/145917605-7e465926-720d-4350-9d71-b3cef234dfda.PNG" alt="ecs12" width="800" height="auto"/>      

<img src="https://user-images.githubusercontent.com/42149645/145917607-f09e8e33-b202-4008-8fff-ffb86edbb2e9.PNG" alt="ecs13" width="800" height="auto"/>      


### 작업 및 컨테이너 정의 구성
- 이름과 iam, 네트워크 모드를 지정할 수 있다.
- iam은 ecs 와 달리 여기서 바로 생성해주지 않으니 직접 필요한 권한을 추가하여 생성해야 한다.
- 네트워크 모드 : 도커에서 사용하는 네트워크 모드와 동일하다. bridge를 선택하면 외부의 포트와 컨테이너 포트 설정이 모두 필요하고 awsvpc와 host는 외부 포트 설정이 불필요하다.
  - awsvpc — 태스크에 고유한 탄력적 네트워크 인터페이스(ENI)와 기본 프라이빗 IPv4 주소가 할당됩니다. 이렇게 하면 태스크에 Amazon EC2 인스턴스와 동일한 네트워킹 속성이 적용됩니다.
  - bridge — 이 태스크는 태스크를 호스팅하는 각 Amazon EC2 인스턴스에서 실행되는 Docker의 기본 가상 네트워크를 이용합니다.
  - host — 이 태스크는 Docker의 기본 가상 네트워크를 우회하여 컨테이너 포트를 태스크를 호스팅하는 Amazon EC2 인스턴스의 ENI에 직접 매핑합니다. 따라서 포트 매핑을 사용할 때 단일 Amazon EC2 인스턴스에서 동일 태스크에 대해 다중 인스턴스화를 실행할 수 없습니다.
  - none — 태스크에 외부 네트워크 연결이 없습니다.
- HTTPS 포트포워딩 기능을 겸해 443포트로 브릿지를 선택했다.
### 작업 실행 iam 역할
- 작업을 실행하는 iam역할도 필요하다. 새 역할 생성으로 자동으로 만들어준다.
### 작업 크기
- 작업에 사용하는 메모리를 설정 가능하다. 
### 컨테이너 정의

<img src="https://user-images.githubusercontent.com/42149645/145917610-1386ccd7-a4f2-493f-a79a-084e77c9a331.PNG" alt="ecs14" width="800" height="auto"/>      

- 진짜 컨테이너 이미지를 만드는 단계, 세부적인 설정은 꽤 복잡하므로 가이드를 참고

> https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_definition_parameters.html#standard_container_definition_params  

- 이름, 이미지, 메모리 제한, 포트 매핑까지는 필수 설정이다. 
- 이미지는 도커 허브 또는 ecr에 푸시한 이미지 등 이미지가 저장된 url과 이미지 이름을 적으면 된다. 도커 허브로 하려면 로그인 인증을 해주어야 한다. 자습서를 이용하였기에 ecr을 사용하였다.

<img src="https://user-images.githubusercontent.com/42149645/145917611-6fe929ee-32d7-40d3-bb2e-7ae69a8d69b4.PNG" alt="ecs15" width="800" height="auto"/>      

- 로그 구성은 나중에 후회하지 않으려면 필수이다.
### 서비스 통합
- App Mesh
### 프록시 구성
- App Mesh
### 로그 라우터 통합
- FireLens
### 볼륨
> 일반적으로 docker container는 컨테이너 내부에 데이터를 관리하므로, 컨테이너가 파기되면 데이터가 모두 날라가게 된다. 이는 mysql 같은 데이터 스토리지를 사용할 경우 위험하게 되는데, 이를 방지하기 위해 따로 볼륨을 설정해서 데이터를 저장해줘야 한다.  
> 이에 대한 대안으로 추천되는것이 볼륨 컨테이너이다. 볼륨 컨테이너는 말 그대로 데이터를 저장하는 것이 목적인 컨테이너이다
### Tags
- 환경변수 설정을 해준다. 필수.

---

## 3. 서비스 생성

<img src="https://user-images.githubusercontent.com/42149645/145917614-0246da27-9a59-4bc9-9b32-67c1e778c323.PNG" alt="ecs17" width="800" height="auto"/>      

<img src="https://user-images.githubusercontent.com/42149645/145917617-d037410c-b5bb-49a9-b73e-651bac9e14e0.PNG" alt="ecs18" width="800" height="auto"/>      

작업 설정이 완료되었으면 실제로 작업을 실행할 서비스를 만들어주어야 한다. 사실상 ecs 관리 기능의 핵심 설정

---


## 3.1 서비스 구성
### 서비스 구성
- 이미 만들어 놓은 시작 유형, 작업 유형 서비스 이름 등을 세팅한다. Auto Scaling을 위해서는 2개 이상의 작업 개수가 필요하다.
### 배포
- 배포 옵션으로 롤링 업데이트가 기본이고 블루/그린 배포도 선택할 수 있다.
- 블루/그린 배포를 선택하게 되면 AWS CodeDeploy기반 배포이므로 AWS CodeDeploy가 자동으로 생성되게 되는데 따라서 CI/CD단부터 AWS CodeDeploy를 선택할 필요가 있다. 

> [배포 전략](../배포%20전략/readme.md)   


### 작업 배치
- 클러스터 내 인스턴스에 작업이 배치되는 방식을 지정한다. 
- 기본적으로 가용 영역(AZ) 전반에 균형적으로 배치한다. 

![ecs20](/public/JS/ecs20.png)    

- 간단하게 보이지만 꽤 중요한 전략으로 가용 영역 A, B가 나누어져 있을 때 각각 개별적으로 트래픽을 받게 된다면 A에는 각각 25%의 트래픽을, B에는 각각 6.25%의 트래픽을 받게 되어 A에게 큰 부담을 주게 된다.

![ecs19](/public/JS/ecs19.png)    

- 따라서 교차 영역 로드밸런싱을 통해 각각에 동일한 수준의 트래픽을 분산하게 하여 부담을 줄일 수 있다.
- 이 개념과 같지만 로드밸런서에서 실행하는 부하분산과 다르게 작업 배치는 작업의 배치를 결정하는 전략이다. 

---

## 3.2 네트워크 구성
### 상태 검사 유예 기간
- 로드밸런서가 상태검사에 응답시간이 걸린다면 어느정도 유예 기간을 정해준다. 기본적인 어플리케이션이라 오래걸릴 일이 없어 0으로 설정


### 로드 밸런싱

<img src="https://user-images.githubusercontent.com/42149645/145919227-71a2b5c9-739b-490a-9290-b881873baaaf.PNG" alt="ecs21" width="800" height="auto"/>      

<img src="https://user-images.githubusercontent.com/42149645/145919231-aaff00c6-32c4-483c-a896-eefa76aa37c4.PNG" alt="ecs22" width="800" height="auto"/>      

- 여러 컨테이너와 인스턴스를 사용하는 ecs에서 가용성 확보에 있어 필수적인 부분
- ELB(Elastic Load Balancing)가 자동적으로 선택되며 로드밸런서를 **미리 만들어와야 한다**. 이 단계에서 새 창을 열어 EC2 -> 로드밸런싱 -> 로드밸런서를 생성하자.  

> [AWS ELB](../AWS%20ELB/readme.md)  

- 로드 밸런서를 생성하여 선택하게 되면 현재 컨테이너 이미지 이름:포트를 로드밸런서에 추가할 수 있게 된다.   

<img src="https://user-images.githubusercontent.com/42149645/145919243-7f74745c-96e6-49e6-b395-9fdd7364fe4d.PNG" alt="ecs24" width="800" height="auto"/>      

<img src="https://user-images.githubusercontent.com/42149645/145919247-6907a408-8dde-4642-bf77-81c00b70e479.PNG" alt="ecs25" width="800" height="auto"/>    

- 작업 정의에서 정의된 프로덕션 리스너 포트와 만약 필요하다면 테스트 리스터 포트를 설정한다.
- 블루/그린 배포시 2개의 대상 그룹이 필수적이고, 롤링 업데이트시에는 1개의 대상 그룹이 나타난다. 이미 로드밸런서에 등록된 블루는 정상적으로 나타나지만 로드밸런서에 등록되지 않은 그린은 새로 생성해주어야 한다. 그린은 미리 만들어놓아도 옵션에 보이지 않는다.
- 상태 확인 경로로 **response가 true로 보내지는 경로**를 입력해주어야 한다. 이것을 몰라서 헬스체크 부분에서 오래 헤맸다.

---

## 4. Auto Scaling

<img src="https://user-images.githubusercontent.com/42149645/145919251-fcd5b9c1-842c-4a23-a887-91cd2a8459d5.PNG" alt="ecs26" width="800" height="auto"/>    

<img src="https://user-images.githubusercontent.com/42149645/145919201-c9c53464-9a9a-404a-8173-31469fba12d9.PNG" alt="ecs27" width="800" height="auto"/>    

- ecs는 오토스케일링도 필요한 경우 자동으로 해준다. 최소 작업 개수, 원하는 작업 개수, 최대 작업 개수를 조정하여 세팅한다.
- 조정 정책을 설정할 수 있는데 cpu, 메모리 등의 사용 백분율을 설정하여 경보로써 사용한다.

---

## 5. 검토

<img src="https://user-images.githubusercontent.com/42149645/145919210-3a6b43b6-5093-4382-ab4e-4835aa20d381.PNG" alt="ecs28" width="800" height="auto"/>    

<img src="https://user-images.githubusercontent.com/42149645/145919214-0cca4ff8-6c20-4860-bdc4-d2e2b53382fb.PNG" alt="ecs29" width="800" height="auto"/>    

- 전체 세팅을 확인 후 서비스를 생성한다.

---

## 6. CI/CD

> [AWS CodePipeline](../AWS%20CodePipeline/readme.md)  


- 만약 블루/그린 배포를 실행했을 시 ecs는 자동으로 컴퓨팅 플랫폼 : ecs -> 배포 유형 블루/그린의 CodeDeploy 어플리케이션을 생성해준다. 당연히 CI/CD를 세팅하려면 이것을 연결해주어야 한다. 

<img src="https://user-images.githubusercontent.com/42149645/145919218-cbe01571-8b5c-48e3-b33f-c56011fad619.PNG" alt="ecs30" width="800" height="auto"/>    

- 성공적으로 블루/그린 배포가 된 화면. 
- ec2 단일 배포 상태와 화면이 많이 다르다.
- 각 1, 2 단계에서 작업 세트의 헬스체크를 각각 실행하고, 3단계부터 1시간동안 블루와 그린 세트를 동시 실행한 후, 4단계에서 이전 작업 세트를 종료시킨다.

---

## 7. CloudWatch
- awslogs 로그 드라이버 사용 : 
https://docs.aws.amazon.com/ko_kr/AmazonECS/latest/userguide/using_awslogs.html

> 출처  
> https://velog.io/@dlawlrb/AWS-ECS-Capacity-Provider%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%98%EC%97%AC-%EC%98%A4%ED%86%A0%EC%8A%A4%EC%BC%80%EC%9D%BC%EB%A7%81%EC%9D%84-%EC%89%BD%EA%B2%8C-%EA%B4%80%EB%A6%AC%ED%95%98%EC%9E%90  
> https://aws-hyoh.tistory.com/133  
> 
> 추천 자습서   
> https://ecs-cats-dogs.workshop.aws/ko/01_intro.html  