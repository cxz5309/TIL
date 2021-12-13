# Forward Proxy vs Reverse Proxy
## 프록시 서버
- 서버와 클라이언트 사이의 중계 역할을 해주는 서버

## Forward Proxy
[proxy1](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPbhvn%2FbtqBzj4CWaB%2FLVl1kFgdRPYq3DLbEeGn10%2Fimg.jpg)  
- 일반적인 프록시 서버는 포워드 프록시이다.
- 클라이언트가 서버에 요청을 보낼 때 직접 요청하지 않고 프록시 서버를 거쳐 프록시 서버에서 요청을 한다.
- 클라이언트의 ip를 감출 수 있어 보안에 도움이 된다.

## Reverse Proxy
[proxy2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsoZxz%2FbtqBvsBdrub%2F3lKN2HHrkzEnxZecoArlFK%2Fimg.jpg)  
- 포워드 프록시의 반대로 서버가 클라이언트로 응답을 줄 때 프록시 서버를 거쳐 보낸다. 
- 서버의 ip를 감출 수 있다.

## 프록시 서버의 장점
- 보안
  - 프록시 서버를 사용하면 클라이언트나 서버 모두 IP를 숨길 수 있는 방법이 생긴다. 
  - 실제 서버 또는 클라이언트의 IP를 숨기고 프록시 서버의 IP만 공개함으로써 해킹을 대비한다.
- 성능 
  - 프록시 서버를 사용하여 캐싱 기능과 트래픽 분산으로 성능 향상을 가져올 수 있다.
  - 캐싱 기능은 자주 사용되는 동일한 요청을 캐싱하여 재활용하는 방식이다. 실제 서버로 다시 호출하지 않고 프록시 서버가 대신 응답을 주어 서버의 자원 사용을 줄여준다.
- 트래픽 분산
  - 일부 프록시 서버(nginx)는 로드 밸런싱도 제공하여 여러 대의 분산된 서버가 있다면 서버의 트래픽을 분산시켜 준다.
  - 그리고 앤드 포인트(URL)마다 호출하는 서버를 설정할 수 있어 역할에 따라 서버의 트래픽을 분산한다.

> 출처  
> https://firework-ham.tistory.com/23  