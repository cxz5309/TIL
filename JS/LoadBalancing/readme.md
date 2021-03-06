# LoadBalancing
- 부하 분산
- 여러 대의 서버를 두는 서비스에서 필요하며 마이크로 서비스가 대세가 된 현재 거의 필수적으로 사용하는 기능이다.


---

![scale](https://post-phinf.pstatic.net/MjAxOTEyMTBfMjk1/MDAxNTc1OTU1MDI2NTY4.Zxj8nWGb6G6jtHDAZPPDf-dPZnpb_hsd7ydWw5lW7vAg.AucOXPJnmLyGiHr8KpVD9Dsy59FsWv5p7qJnSyW_YFAg.JPEG/%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1_%EC%8A%A4%EC%BC%80%EC%9D%BC.jpg?type=w1200)
## Scale-up
- 현재 사용중인 서버 자체의 가용성을 늘리는 것
- ec2 서버를 micro에서 large로 업그레이드하는 것을 예로 들 수 있다.
- fargate등의 서버리스 환경에서는 자동으로 이 기능을 해준다.
## Scale-out
- 사용중인 서버를 추가해서 새 서버에 트래픽을 분산하는 것
- 트래픽을 분산하는 것 자체가 로드밸런싱이며 Scale-out 방식을 사용했을 경우 로드밸런싱이 꼭 필요하다.

---

## 로드밸런싱 알고리즘
- 라운드로빈 방식(Round Robin Method)
서버에 들어온 요청을 순서대로 돌아가며 배정하는 방식. 

- 가중 라운드로빈 방식(Weighted Round Robin Method)
각각의 서버마다 가중치를 매기고 가중치가 높은 서버에 클라이언트 요청을 우선적으로 배분하는 방식. 주로 서버의 트래픽 처리 능력이 상이한 경우 사용되는 부하 분산 방식.

- IP 해시 방식(IP Hash Method)
클라이언트의 IP 주소를 특정 서버로 매핑하여 요청을 처리하는 방식. 사용자의 IP를 해싱해 로드를 분배하기 때문에 사용자가 항상 동일한 서버로 연결되는 것을 보장.

- 최소 연결 방식(Least Connection Method)
요청이 들어온 시점에 가장 적은 연결상태를 보이는 서버에 우선적으로 트래픽을 배분. 자주 세션이 길어지거나, 서버에 분배된 트래픽들이 일정하지 않은 경우에 적합한 방식.

- 최소 리스폰타임(Least Response Time Method)
가장 적은 연결 상태와 가장 짧은 응답시간을 보이는 서버에 우선적으로 로드를 배분하는 방식.

- ## 교차 영역 로드 밸런싱  
![ecs20](/public/JS/ecs20.png)    
가용 영역 A, B가 나누어져 있을 때 각각 개별적으로 트래픽을 받게 된다면 A에는 각각 25%의 트래픽을, B에는 각각 6.25%의 트래픽을 받게 되어 A에게 큰 부담을 주게 된다.


![ecs19](/public/JS/ecs19.png)    
따라서 교차 영역 로드밸런싱을 통해 각각에 동일한 수준의 트래픽을 분산하게 하여 부담을 줄일 수 있다.

---

## L4, L7
![L4](https://post-phinf.pstatic.net/MjAxOTEyMTBfNCAg/MDAxNTc1OTU1MzY3OTM2.nG91HOEOh6Sc1AuUgbN3O4pcnEI-rh24UKSrrrjkrcsg.VcG18MidW4az7Oh0RQfRPLDBHNRyGayE1BsQxDImL3Ig.JPEG/L4-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1.jpg?type=w1200)   

![L7](https://post-phinf.pstatic.net/MjAxOTEyMTBfMjA1/MDAxNTc1OTU1MzgxODY5.odnG4CRES0e5bH7sOKyWRP1c8uO_XC4VX9A3HPeI1JQg.lNL2eJYbMz6NX1e5YFzfHDMQHn4YrdOJR2VYHmq5e1Ig.JPEG/L7-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1.jpg?type=w1200)   

- 주로 L4는 TCP/UDP단 로드밸런싱, L7은 HTTP/HTTPS단 로드밸런싱을 한다. 주로 하는 역할이며 사실상 상위 계층은 하위 계층의 로드밸런싱 기능을 모두 수행 할 수 있다.
- 따라서 일반적으로 L7 로드밸런서가 L4 로드밸런서보다 비싸지만 조금 더 정교한 클라이언트별 로드밸런싱이 가능하며 DoS/DDoS와 같은 비정상적인 트래픽, 바이러스 필터링 등이 가능하다.
- 하지만 L7 로드밸런서가 L4로드밸런서보다 느리기 때문에 현명한 선택이 필요하다.   

ex) L4 예시: IP+Port > 213.12.32.123:80, 213.12.32.123:1024   
ex) L7 예시 : IP+Port+패킷 내용을 한번에 표현한다. 213.12.32.123:80, 213.12.32.123:1024 + GET/ img/aaa.jpg   

> 출처   
> https://m.post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903   
> https://vaert.tistory.com/189  
