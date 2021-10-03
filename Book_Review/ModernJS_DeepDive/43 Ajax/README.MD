# 43 Ajax (Asynchronous JavaScript and XML)

## 43.1 Ajax란?
- 자바스크립트로 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, 서버가 응답한 데이터를 수신하여 웹페이지를 동적으로 갱신
- js는 Web api인 XMLHttpRequest를 통해 비동기 통신을 한다.

- Ajax의 등장은 서버로부터 웹 페이지의 변경에 필요한 데이터만 비동기 방식으로 받아 웹페이지를 변경할 필요가 없는 부분은 다시 렌더링하지 않고, 변경할 필요가 있는 부분만 한정적으로 렌더링하는 방식으로 화면을 표시할 수 있게 하였다. (SPA)
> 근데 지금 배우는거는 왜 맨날 새로고침하고있지..  

## 43.2 JSON
- 클라이언트와 서버 간의 HTTP통신을 위한 텍스트 데이터 포맷, XML에서 거의 대체되었다.

### 43.2.2. JSON.stringify
- 객체를 json포맷으로 직렬화한다.
### 43.2.3 JSON.parse
- json 포맷의 문자열을 객체로 변환한다.
- 이를 역직렬화라고 한다.

## 43.3 XMLHttpRequest
- XMLHttpRequest 객체는 **브라우저**에서 제공하는 **Web API**이므로 **브라우저 환경에서만 정상적으로 실행된다.**

### 43.3.3 HTTP 요청 전송
- HTTP요청을 전송하는 경우 다음 순서를 따른다.
1. XMLHttpRequest.prototype.open 메서드로 HTTP 요청을 초기화한다.
2. 필요에 따라 XMLHttpRequest.prototype.setRequestHeader 메서드로 특정 HTTP 요청의 헤더 값을 설정한다.
3. XMLHttpRequest.prototype.send 메서드로 HTTP요청을 전송한다.

#### XMLHttpRequest.prototype.open
- method: HTTP 요청 메서드
- url: HTTP 요청을 전송할 URL
- async: 비동기 요청 여부, 기본값 true

##### method 종류
GET : index/retrieve 용도, 페이로드 x
POST : create 용도
PUT : replace 용도
PATCH : modify 용도
DELETE : delete 용도, 페이로드 x

#### XMLHttpRequest.prototype.send
- 서버로 전송하는 데이터는 GET, POST 요청 메서드에 따라 전송 방식에 차이가 있다.
![요청방식](../../../public/Book_ReView/ModernJS_DeepDive/요청방식.png)


#### XMLHttpRequest.prototype.setRequestHeader
- setRequestHeader메서드는 반드시 open메서드를 호출한 이후에 호출해야 한다.

#### 자주 사용되는 MIME 타입 종류
| MIMI 타입   | 서브타입                                           |
| ----------- | -------------------------------------------------- |
| text        | text/plain, text/html, text/css, text/javascript   |
| application | application/json, application/x-www-form-urlencode |
| multipart   | multipart/formed-data                              |

