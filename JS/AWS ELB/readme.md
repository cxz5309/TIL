# AWS ELB(Elastic Load Balancing)
![elb1](/public/JS/elb1.png)  
- AWS의 로드밸런싱 기능을 담당한다. 

<img src="https://user-images.githubusercontent.com/42149645/145919236-aff7896a-7f98-4da8-8df6-47158a940dd6.PNG" alt="ecs23" width="800" height="auto"/>    

---

## 1. 로드밸런서 타입 선택
- L4 로드밸런서인 NLB(Network Load Balancer), L7 로드밸런서인 ALB(Application Load Balancer), L3로드밸런서인 GLB(Gateway Load Balancer)를 기본 옵션으로 두고, 이전 버전인 Classic Load Balancer도 사용 가능하다.

<img src="https://user-images.githubusercontent.com/42149645/145920309-b56d127a-44c1-4bae-8cfc-fc5124b82cbb.PNG" alt="elb2" width="800" height="auto"/>    

<img src="https://user-images.githubusercontent.com/42149645/145920317-ab3dfc5e-568d-418c-ba07-a84fd98b4fba.PNG" alt="elb3" width="800" height="auto"/>    


## 로드밸런서 생성


<img src="https://user-images.githubusercontent.com/42149645/145920321-c76801d6-d88d-4ea0-8b74-3c9f437e0a94.PNG" alt="elb4" width="800" height="auto"/>    

<img src="https://user-images.githubusercontent.com/42149645/145920324-48679229-ab5e-4e0c-aec6-19f2940c44f3.PNG" alt="elb5" width="800" height="auto"/>    

<img src="https://user-images.githubusercontent.com/42149645/145920325-fd333f2e-5e57-4058-a86a-6e423cf76d77.PNG" alt="elb6" width="800" height="auto"/>    

<img src="https://user-images.githubusercontent.com/42149645/145920327-e25e057f-e966-4093-905e-5cd9b2b92c25.PNG" alt="elb7" width="800" height="auto"/>    

### 네트워크 매핑
- vpc 영역을 선택한 후 가용 영역을 매핑한다.
### 보안 그룹
- 보안 그룹을 선택한다. 로드밸런서 설정 이후에는 로드밸런서의 DNS로 접속해야 하기 때문에 이전 ec2 보안 그룹과 같은 세팅을 하였다.
### 리스너와 라우팅
- ALB이기 때문에 포트단에서 라우팅이 가능하다. 리스너가 수신한 트래픽은 사양에 따라 라우팅된다.  
- 먼저 타겟 그룹을 생성 후 설정해야 한다! 2. 타겟 그룹 설정에서 설명

<img src="https://user-images.githubusercontent.com/42149645/145920331-358e88f8-16e8-4245-be92-f897a1155457.PNG" alt="elb8" width="800" height="auto"/>    


- HTTPS 프로토콜을 선택할 경우 SSL 세팅을 해주어야 한다. ACM(AWS Certificate Manager) 에 인증서를 등록하고 사용하였다. 인증서는 무료 발급 기관인 Let's Encrypt에서 발급받았는데 AWS에서도 무료로 발급이 가능하다고 한다!  
### 요약
- 만들어질 로드밸런서 상태 확인
---
## 2. 타겟 그룹 설정 1

<img src="https://user-images.githubusercontent.com/42149645/145920974-db641fb5-7279-4927-94d8-6560a48c9e21.PNG" alt="elb9" width="800" height="auto"/>    

<img src="https://user-images.githubusercontent.com/42149645/145920979-1afb211b-a667-4c0c-8979-6bffdf1cc688.PNG" alt="elb10" width="800" height="auto"/>    

- 블루/그린 배포일 경우 반드시 2개 이상의 타겟 그룹 설정이 필요하다. 다만 그린 영역의 타겟 그룹은 먼저 생성할 경우 ecs에서 보이지 않기에 ecs에서 새로 생성하는 작업이 필요하다. 

## 기본 구성
- 로드밸런서를 통해 포워딩되는 tcp 또는 포트 설정. 기본 tcp 80번 포트로 설정되어 있다.
- vpc 설정이 가능하다.

## 헬스 체크
- 헬스체크가 가능한 api 상대 주소를 입력할 수 있다. 
> - 기본 '/' 로 백엔드 기본 주소이나 /api를 기본으로 라우팅되게 만들었기 때문에 기본주소 / 에서는 res의 상태가 false로 반환되었었고 처음에 이해하지 못했을 때 매우매우 많이 해메다가 해결하였다.   


---
## 3 타겟 그룹 설정 2

<img src="https://user-images.githubusercontent.com/42149645/145920982-1999332c-0394-49de-9d31-44e3f20be8e7.PNG" alt="elb11" width="800" height="auto"/>    

- 가용 인스턴스 중 타겟을 등록한다. ecs 블루/그린 배포에서 이 작업이 꼭 필요한 줄 알았으나 ecs에서 자동으로 동적 등록해준다.
