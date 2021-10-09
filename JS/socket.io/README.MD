# socket.io

  > 기본적으로 뭔가 비교할 대상이 있을 때 관심이 생기는데 socket.io 강의를 듣던 중 웹소켓이 공식적으로 나온 표준 기술인데 아직 지원하지 않는 곳이 있어서 socket.io라는 웹소켓 기술과 흡사하게 만든 기술을 쓴다고 하여 '왜 웹소켓을 쓰지 않는지, 소켓의 동작 과정을 알아보기로 하였다.  

## 웹소켓의 배경
- 전형적인 브라우저 렌더링 방식은 request에 대한 response를 받은 후 브라우저의 화면을 깨끗하게 지우고 받은 내용을 새로 표시하는 방식이다. 이 방식은 브라우저의 깜빡임이 생기고 어느정도 지연이 생기게 된다.
- 이것에 대한 해결 방법 중 하나로 요즘 나오는 <a href='../CSR과 SSR/README.MD#csr'>CSR</a>이 있지만 다른 방식으로 푸는 방법도 많이 연구되었다.
- 상호작용하는 웹 서비스를 위해 Long Polling, Stream 등 다양한 방법이 연구되었는데 이러한 방식은 브라우저가 HTTP 요청를 보내고 웹 서버가 이 요청에 대한 HTTP 응답를 보내는 **단방향** 메세지 교환 '규칙'을 변경하지 않고 구현한 방식이다. 그렇기 때문에 상호작용하는 웹 페이지를 복잡하고 어려운 코드로 구현해야 했다.

![long polling](http://www.secmem.org/assets/images/websocket-socketio/polling.png)  
**long polling**  
- 클라이언트에서 일정 주기마다 요청을 보내고 서버는 현재 상태를 바로 응답하는 방식
- 실시간 반응이 가능하고 polling에 비해서 불필요한 트래픽은 유발하지는 않지만 오히려 이벤트가 잦다면 순간적으로 과부하가 걸리게 된다.

![Streaming](http://www.secmem.org/assets/images/websocket-socketio/streaming.png)  
**Streaming**  
- 이벤트가 발생했을때 응답을 내려주는데 응답을 완료시키지 않고 계속 연결을 유지하는 방식.
- Long Polling에 비해 응답마다 다시 요청을 하지 않아도 되므로 효율적이지만, 연결 시간이 길어질수록 연결의 유효성 관리의 부담이 발생한다.
> 출처: http://www.secmem.org/blog/2019/08/17/websocket-socketio/  

- 보다 쉽게 상호작용하는 웹 페이지를 만들려면 브라우저와 웹 서버 사이에 더 자유로운 양방향 메시지 송수신(bi-directional full-duplex communication)이 필요하다. 그래서 HTML5 표준안의 일부로 WebSocket API(이후 WebSocket)가 등장했다.

## 웹소켓의 특징
- websocket이란 웹 서버와 웹 브라우저간 **실시간 양방향** 통신환경을 제공해주는 실시간 통신 기술이다. 위의 Polling 방식(요청-응답방식)과 다르게 양방향으로 원할때 요청을 보낼 수 있으며 stateless한 HTTP에 비해 오버헤드가 적으므로 유용하게 사용할 수 있다.
![웹소켓](http://www.secmem.org/assets/images/websocket-socketio/websocket.png)
> 출처: http://www.secmem.org/blog/2019/08/17/websocket-socketio/  

## WebSocket 프로토콜
- 표준 WebSocket의 API는 W3C에서 관장하고, 프로토콜은 IETF(Internet Engineering Task Force)에서 관장한다. 그리고 WebSocket은 **다른 HTTP 요청과 마찬가지로 80번 포트를 통해 웹 서버에 연결한다**. HTTP 프로토콜의 버전은 1.1이지만 다음 헤더의 예에서 볼 수 있듯이, Upgrade 헤더를 사용하여 웹 서버에 요청한다. 당연한 이야기겠지만 클라이언트인 브라우저와 마찬가지로 웹 서버도 WebSocket 기능을 지원해야한다.
```
GET /... HTTP/1.1  
Upgrade: WebSocket  
Connection: Upgrade  
```
- 브라우저는 "Upgrade: WebSocket" 헤더 등과 함께 **랜덤하게 생성한 키**를 서버에 보낸다. 웹 서버는 이 키를 바탕으로 **토큰**을 생성한 후 클라이언트에 돌려준다. 이런 과정으로 WebSocket 핸드쉐이킹이 이루어진다.
- 그 뒤 Protocol Overhead 방식으로 웹 서버와 브라우저가 데이터를 주고 받는다. Protocol Overhead 방식은 여러 TCP 커넥션을 생성하지 않고 **하나의 80번 포트 TCP 커넥션**을 이용하고, 별도의 헤더 등으로 논리적인 데이터 흐름 단위를 이용하여 여러 개의 커넥션을 맺는 효과를 내는 방식이다.
- 이런 방식을 사용하기 때문에 방화벽이 있는 환경에서도 무리 없이 WebSocket을 사용할 수 있다.
> 방화벽은 80번 포트를 허용한다고 한다.  
> https://it.donga.com/8810/  

## socket.io의 배경
- 놀랍게도 웹소켓을 지원하지 않는 환경이 ie말고도 꽤 많이 있었다!

![image](https://d2.naver.com/content/images/2015/06/helloworld-1336-2-1.png)  
> Mozilla 계열 브라우저와 Opera에서는 프록시와 관련된 보안 이슈 때문에 WebSocket의 기본 설정을 'disable'로 설정했다. about:config 페이지에서 설정을 변경할 수 있지만 많은 사용자들이 이 조치에 불만을 제기했다. 프록시와 관련된 문제는 Flash나 Java에서도 동일하게 발생하는데 WebSocket만 기본 설정에서 제외했다는 것에 대한 불만이었다. 이러한 의견을 반영한 것인지 Mozilla 재단에서는 Firefox 6.0부터 네임 스페이스를 붙여 MozWebSocket으로 다시 WebSocket을 지원하기 시작했다. 이 사례는 사용자들이 WebSocket에 거는 기대감이 굉장히 크다는 것을 엿볼 수 있는 사례다.  
> 출처: https://d2.naver.com/helloworld/1336  
- 즉 못쓰니까 socket.io가 탄생했다

## socket.io의 특징
- WebSocket이 미래의 기술이라면 Socket.io는 현재 바로 사용할 수 있는 기술이다. Socket.io는 JavaScript를 이용하여 브라우저 종류에 상관없이 실시간 웹을 구현할 수 있도록 한 기술이다.
- Guillermo Rauch가 만든 Socket.io는 **WebSocket**, **FlashSocket**, **AJAX Long** **Polling**, **AJAX Multi part Streaming**, **IFrame**, **JSONP Polling**을 하나의 API로 추상화한 것이다. 
- ### 즉 브라우저와 웹 서버의 종류와 버전을 파악하여 가장 적합한 기술을 선택하여 사용하는 방식이다. 
- ### 그 덕분에 socket.io를 통해 개발을 하면 websocket이 지원이 되지 않는 브라우저에서도 메시지를 양방향으로 주고 받을 수 있다.
> - 가령 브라우저에 Flash Plugin v10.0.0 이상(FlashSocket 지원 버전)이 설치되어 있으면 FlashSocket을 사용하고, Flash Plugin이 없으면 AJAX Long Polling 방식을 사용한다.  
- Web Socket과 달리 Socket.io는 표준 기술이 아니고 Node.js 모듈로서 Guillermo Rauch가 CTO로 있는 LearnBoost(https://www.learnboost.com) 라는 회사의 저작물이며 MIT 라이센스를 가진 **오픈소스**이다. 
- Socket.io는 WebSocket과 마찬가지로 브라우저에서는 JavaScript를 사용한다. WebSocket 프로토콜은 IETF에서 관장하는 표준 프로토콜이라서 WebSocket을 지원하는 여러 서버 구현체(Jetty, GlassFish, Node.js, Netty, Grizzly 등)가 있지만 **Socket.io는 Node.js 하나 밖에 없다.** (오)

## 결론
- 웹소켓은 기존의 req, res를 통한 요청 응답 방식이 아닌 **실시간, 양방향** 통신에 적합한 기술이다.
- **tcp통신**이며 **80번 포트**를 사용하므로 방화벽에도 걸리지 않는다.
- 그러나 socket.io는 웹소켓의 발달에 비해 인터넷 환경이 따라오지 않아 만들어진 인터넷 환경에 따라 실시간 양방향 통신을 지원하는데 가장 적합한 기술을 찾아주는 **추상화된 API이다.**
- 한 천재가 개발한 오픈소스이며 아직 node.js에서밖에 지원되지 않는다

> 출처 :   
> https://d2.naver.com/helloworld/1336  
> http://www.secmem.org/blog/2019/08/17/websocket-socketio/   
