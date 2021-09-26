# REST vs SOAP vs GraphQL

> 보통 무언가에 대해서 알아볼 때 다른 비슷한 것과 비교하는 방식을 좋아한다. 그 방법으로 구글에 '비교할것 vs' 라고 치면 비교적 명쾌한 비교 대상이 나온다 그런데 rest방식은 vs를 쳤을 때 soap와 따로 비교되고 graphql과 따로 비교되었다. graphql은 예전에 써봐서 차이점을 대충 아는데 왜 굳이 따로 비교되는지와 soap방식은 무엇인지, restful 방식과 다른 방식의 차이를 다시 정리해보자  

- SOAP, REST 및 GraphQL의 변화를 살펴보고 이들이 어떻게 다른지 알아본다. REST API는 차이점만 다룬 후 맨 마지막에 자세히 다시 다룰 예정이다.

## 배경
- 역시 예상대로 soap api가 가장 먼저 탄생했고(1998) rest가 soap를 개선하여 등장 후(2000) 한동안 웹 생태계를 지배하다가 Facebook이 GraphQL이라는 새로운 개념을 탄생시켰다(2015)
- 그러나 최신 기술이 기존 기술을 사용 생태계에 따라 보완하였지만 각각의 기술은 모두 본질적으로 다른 기술이며 기존의 기술보다 좋다고 말할 수 없다. 즉 **모두 장단점이 있다.**

## SOAP(Simple Object Access Protocol)
- SOAP는 그 자체로 프로토콜이며, 보안이나 메시지 전송 등에 있어서 REST보다 더 많은 표준들이 정해져있기 때문에 조금 더 복잡하다.
- 이러한 표준들로 인해서 오버헤드가 많기는 하지만, 보안, 트랜잭션, ACID(원자성, 일관성, 고립성, 지속성)을 준수해야 하는 보다 종합적인 기능이 필요한 조직에게는 적합한 방식이 될 수 있다. 
- SOAP는 보안 수준이 엄격하다. SOAP에서는 **SSL**도 지원하고 **WS-Security**라는 자체 표준의 보안 기능도 가지고 있다. 따라서 은행용 모바일 앱처럼 보안 수준이 높아야 하거나, 신뢰할 수 있는 메시징 앱, 또는 ACID를 준수해야 하는 경우라면 SOAP 방식이 더욱 선호된다.
- REST에서는 **표준화된 메시징 시스템**이 갖춰져 있지 않으며, 통신 장애가 있을 경우 재시도를 통해서만 조치할 수 있다. 반면 SOAP 표준에는 성공/반복 실행 로직이 규정되어 있기 때문에, SOAP API를 통해서 통신을 할 때 처음부터 끝까지 신뢰성을 제공한다.
- SOAP 표준에는 **ACID 준수**에 관한 사항이 있다. ACID를 준수하기 때문에 데이터의 변형을 줄여주고, 데이터베이스와의 상호작용에 대해서 사전에 정확하게 정하기 때문에 데이터의 무결성을 지켜준다. ACID는 데이터 일관성을 위한 다른 방식들보다도 더 보수적이기 때문에, 금융 정보 등의 민감한 데이터를 주고받을 때 일반적으로 많이 사용된다.

## SOAP vs REST
- API라는 것은 결국은 앱의 페이로드를 처리하기 위해서 만들어진 것인데, SOAP와 REST의 가장 큰 차이는 페이로드를 처리하는 방식에 있다. 
  - 페이로드: 인터넷을 통해서 전송되는 데이터
- 페이로드가 ‘무거운’경우에는 더 많은 리소스가 필요하다. **REST**는 **HTTP와 JSON**을 사용하기 때문에 페이로드의 무게를 가볍게 할 수 있다. 하지만 **SOAP**에서는 **XML**에만 의존한다.
- **SOAP 구조는 더 많은 신뢰성과 보안성을 가진 대신 SOAP 내에서 전송되는 데이터의 양은 엄청나서 더 많은 리소스가 필요하고 통신 속도가 느려졌다.**
- SOAP는 서버와 긴밀하게 연결하며, REST는 보다 느슨한 형태로 연결된다. 즉 REST가 더 확장성과 추상화의 장점을 가지고 있다.
- SOAP는 서버와 매우 긴밀하게 연결되기 때문에 그 통신 방식이 매우 엄격하며, 메시지 인코딩/디코딩 과정 등 웹 서비스 개발의 난이도가 높아 수정이나 업데이트를 하는 것이 보다 더 어렵다. REST 방식의 API에서는 클라이언트에서 해당 API가 필요하지 않지만, SOAP 방식의 API에서는 상호작용을 시작할 때조차도 클라이언트에서 API에 관한 모든 정보들을 필요로 한다.


### 결론
- **SOAP**
  - SOAP는 **프로토콜**이며, 엄격한 통신 규약 및 보안성으로 인해 데이터의 신뢰성과 보안성이 뛰어나다.
  -  그러나 그 정보를 포함하는 것과 데이터 형식으로 **XML**을 사용하는 것은 너무 무겁기 때문에 리소스와 대역폭을 더 많이 필요로 하고, 추상화 계층이 적기 때문에 업데이트도 쉽지 않다. 
  -  따라서 **기업용 애플리케이션**인 경우에는 **보다 많은 리소스와 아주 엄격한 보안 그리고 여러 다양한 요구 사항**들을 만족해야 하기 때문에 SOAP 방식을 택하는 경우가 많다!
- **REST**
  - REST는 실질적인 구현이 아닌 설계적 지침인 **아키텍쳐 스타일**이므로 REST 방식의 API라면 클라이언트-서버 모델로 구축되었다는 것을 의미하며, 정보의 페이로드가 두 지점 사이를 왕복하는 방식으로 이루어진다는 것을 뜻한다. 
  - SOAP와의 가장 큰 차이로 일반 텍스트, HTML, XML, JSON형식 등 **다양한 데이터 포맷**을 허용하기 때문에 SOAP에 비해 리소스가 적게 들고, 추상화와 엄격하지 않은 규약으로 인해 매우 빠르게 통신이 가능하다. 
  - 따라서 REST는 **웹과 모바일** 환경에서 SOAP를 압도하였으며, 오래도록 웹 API의 표준이 되어왔다!

## REST vs GraphQL
> Facebook 의 GraphQL blog 에는 REST 방법론이 있는데도 새로운 언어인 GraphQL 이 탄생해야했던 배경을 말해준다.  
> - RESTful API 로는 다양한 기종에서 필요한 정보들을 일일히 구현하는 것이 힘들었다.   
> - 예로, iOS 와 Android 에서 필요한 정보들이 조금씩 달랐고, 그 다른 부분마다 API 를 구현하는 것이 힘들었다.  
> - 즉 rest 방식으로는 Resource 마다 하나의 Endpoint 를 가지고, 그 Endpoint 에서 그 Resource 에 대한 (거의) 모든 것을 담당하게 되는데 그 방식이 구현에 오래 걸린다는 것이다  
```
글 관련 API = /posts
글 작성 = POST /posts
글 수정 = PATCH /posts/[postid]
글 삭제 = DELETE /posts/[postid]
댓글 관련 API = /posts/[postid]/comments
댓글 작성 = POST /posts/[postid]/comments
댓글 수정 = PATCH /posts/[postid]/comments/[commentid]
댓글 삭제 = DELETE /posts/[postid]/comments/[commentid]
```  
이렇게 작은 기능 구현에도 end point가 너무 많아지게 된다.  

- GraphQL은 이것을 표준화된 **Query language**를 만듦으로써 해결했다.
REST는 데이터를 보통 JSON형식의 리소스 자체를 보내게 된다.

```
{
	"title": "Romance of the Three Kingdoms",
	"author": {
		"firstName": "Luo",
		"lastName": "Guanzhong"
	}
}
```  
##### GET /books/1  
이 데이터를 GraphQL에서는 모델과 쿼리를 통해 전송한다.   
```
type Book {
	id: ID
	title: String
	author: Author
}
type Author {
	id: ID
	firstName: String
	lastName: String
	books: [Book]
}
```  
##### 모델  
```
type Query {
	book(id: ID!): Book
	author(id: ID!): Author
}
```  
##### 쿼리  
이제 이 데이터를 REST와 비슷한 방식으로 요청한다.
```
/graphql?query={ book(id: "1") { title, author { firstName } } }
```  
- 이렇게 쿼리를 사용하는 것은 다음과 같은 장점을 가진다.
1. HTTP 요청의 횟수를 줄일 수 있다.
  - **RESTful** 은 각 Resource 종류 별로 요청을 해야하고, 따라서 **요청 횟수가 필요한 Resource 의 종류에 비례한다**
  - 반면 **GraphQL** 은 원하는 정보를 하나의 Query 에 모두 담아 **한번에 요청할 수 있다.**
2. HTTP 응답의 Size 를 줄일 수 있다.
  - **RESTful** 은 응답의 형태가 정해져있고, 따라서 **필요한 정보만 부분적으로 요청하는 것이 힘들다.**
  - 반면 **GraphQL** 은 사용자에게 **필요하지 않은 속성을 제외하고** 요청하는 것이 가능해졌다.
![image](https://hwasurr.io/static/321080a2818c985b4f65f0eb0218b30f/d2a60/rest-graphql.png)  
> 출처: https://hwasurr.io/api/rest-graphql-differences/  

- 하지만 그럼으로써 GraphQL은 다음과 같은 단점도 가진다.
1. 고정된 요청과 응답만 필요할 경우에는 Query 로 인해 요청의 크기가 RESTful API 의 경우보다 더 커진다.
2. HTTP 캐싱 사용이 불가능하다. GraphQL 은 엔드 포인트가 1개 이므로 HTTP 에서 제공 되는 캐싱이 사용 불가능 하다.
  - 하지만 GraphQL 의 Apollo 사의 Apollo Engine 에서 자체 적으로 캐시를 제공 하기 떄문에 이점을 활용하면 된다.
3. 재귀적인 Query 가 불가능하다. (결과에 따라 응답의 깊이가 얼마든지 깊어질 수 있는 API 를 만들 수 없다.)
4. 실질적으로 Rest API 처럼 표준이 없기 때문에 코딩을 하는데 있어서 표준을 백엔드와 정하고 약속 하는 시간이 걸릴 수 있다.
> GraphQL이 Query 를 전송하고 Json 만 리턴 받았기 떄문에 File 전송 등이 불가능했던 문제는 GraphQL 버전이 올라감으로써 외부 라이브러리를 사용하다가 자체적으로 해결이 되었다.  

### 결론 
- **REST**
  - REST는 **아키텍처 스타일**이다. 엔드포인트가 많다는 점은 각각의 엔드 포인트에 HTTP 와 HTTPs 에 의한 **Caching**이 쉽다는 것을 뜻하며 response가 JSON으로 한정되는 GraphQL에 비해 **다양한 데이터 타입**을 지정할 수 있다. 또한 **재귀적인 쿼리**를 통해 응답의 길이가 깊은 복잡한 api를 만들때도 유리하며 무엇보다 **많이 사용된다**! 경우와 사용 방법에 따라 GraphQL보다 구현 시간이 빠르기 때문에 각각 장단점이 있다고 볼 수 있다.
- **GraphQL**
  - GraphQL은 이름의 "QL"에서 알 수 있듯이 **쿼리 언어**이다. 데이터 요청과 응답에 단 한줄의 쿼리로도 사용할 수 있기 때문에 REST방식에 비해 **요청 횟수가 적고** 모든 정보를 같이 보내야 하는 REST에 비해 필요한 속성만을 보낼 수 있기 때문에 **크기도 작아질 수 있다**. REST방식과 혼합해서 사용하는 것도 지원하며 필요한 상황에 맞게 쓰면 리소스를 절약할 수 있는 새로운 패러다임이다!


## 각각 언제 사용해야 하는가?
- SOAP
  - SOAP는 공식 계약 기반 교환 형식을 사용하는 엔터프라이즈 솔루션에서 사용할 수 있습니다. 또한 SOAP API는 양쪽에 가속 메커니즘이 구현되어 있을 때 가장 잘 작동합니다.
- REST
  - REST는 JavaScript에 매우 친숙하므로 JavaScript 기반 응용 프로그램에 완벽한 선택입니다. 또한 SOAP보다 더 높은 부하에 대처하고 데이터를 더 빠르게 처리할 수 있습니다. 따라서 애플리케이션이 로드 집약적이라면 REST가 API가 될 수 있습니다.
- GraphQL
  - GraphQL은 쿼리 수를 최소로 줄여야 할 때 최고의 성능을 보여줄 수 있습니다. 여러 리소스를 처리하는 단일 쿼리를 통해 GraphQL은 이 문제에 적합할 수 있습니다. 또한 GraphQL에서는 데이터가 클라이언트 측에서 정의된다는 점을 고려할 때 클라이언트 애플리케이션과 서버 간의 종속성이 없는 경우에 좋은 솔루션이 될 수 있습니다.


## REST(Representational State Transfer)
> REST는 특정한 툴이나 사용 방법이 따로 있는 것이 아닌 아키텍처의 스타일이다. 즉 그 구조를 제작하는 방법은 정해져있지만 실제 제작한 웹페이지가 REST의 특징을 그대로 따르고 있는지에 대해서는 알 수 없다. 마지막으로 REST의 구체적인 개념과 rest하다는 것이 무엇인지 알아보자  

### REST의 정의
- 자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미한다.
- **자원(resource)**의 **표현(representation)** 에 의한 **상태 전달**
  - 자원: 해당 소프트웨어가 관리하는 모든 것
  - 자원의 표현: 그 자원을 표현하기 위한 이름
  - 상태 전달: 데이터가 요청되어지는 시점에서 자원의 상태(정보)를 전달한다.
- 월드 와이드 웹(www)과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 개발 아키텍처의 한 형식
  - REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.
  - REST는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나이다.
### REST의 개념
- HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.
- 즉, REST는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.
- 웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여한다.
- CRUD를 위한 METHOD가 정해져 있다.
  
```
- Create : 생성(POST)
- Read : 조회(GET)
- Update : 수정(PUT)
- Delete : 삭제(DELETE)
- HEAD: header 정보 조회(HEAD)
```
### REST의 장단점
#### 장점
- HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구축할 필요가 없다.
- HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.
#### 단점
- 표준이 존재하지 않는다.
- 사용할 수 있는 메소드가 4가지 밖에 없다.
  - -> HTTP Method 형태가 제한적이다.
- 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 값이 왠지 더 어렵게 느껴진다.
- 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.

### REST 구성 요소
1. **자원(Resource): URI**
   - 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
   - 자원을 구별하는 ID는 ‘/groups/:group_id’와 같은 HTTP URI 다.
   - Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.
2. **행위(Verb): HTTP Method**
   - HTTP 프로토콜의 Method를 사용한다.
   - HTTP 프로토콜은 GET, POST, PUT, DELETE 와 같은 메서드를 제공한다.
3. **표현(Representation of Resource)**
   - Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
   - REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있다.
   - JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.
### REST의 특징
1. **Uniform (유니폼 인터페이스)**
   - Uniform Interface는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일
2. **Stateless (무상태성)**
   - 상태가 있다 없다는 의미는 사용자나 클라이언트의 컨택스트를 서버쪽에 유지 하지 않는다는 의미한다.
   - 세션이나 쿠키등을 별도로 관리하지 않기 때문에 API서버는 요청만을 들어오는 메시지로만 처리하기 때문에 구현이 단순하다. 
   > (무상태성인 REST에 상태를 주기 위해 세션이나 쿠키가 등장했다.)  
3. **Cacheable (캐시 처리 가능)**
   - REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용한다는 것이다.
   - HTTP가 가진 캐싱 기능이 적용 가능하다. HTTP 프로토콜 표준에서 사용하는 Last-Modified태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.
4. **Self-descriptiveness (자체 표현 구조)**
   - REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 것이다.
5. **Client - Server Architecture (클라이언트 - 서버 구조)**
   - REST 서버는 API를 제공하고, 제공된 API를 이용해서 비즈니스 로직 처리 및 저장을 책임진다.
   - 클라이언트의 경우 사용자 인증이나 컨택스트(세션,로그인 정보)등을 직접 관리하고 책임진다.
   - 서로간의 의존성이 줄어들게 된다.
6. **계층형 구조**
   - 클라이언트 입장에서는 REST ApI 서버만 호출한다.
   - REST 서버는 다중 계층으로 구성될 수 있다. 예를 들어 보안, 로드 밸런싱, 암호화, 사용자 인증등등 추가하여 구조상의 유연성을 줄 수 있다.

## RESTful 하다는 것
- RESTful은 누군가가 공식적으로 발표한 것이 아니며, 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.
- ‘REST API’를 제공하는 웹 서비스를 ‘RESTful’하다고 할 수 있다.
- 즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.
> ### RESTful 하지 못한 경우
> - CRUD 기능을 모두 POST로만 처리하는 API
> - route에 resource, id 외의 정보가 들어가는 경우(/students/update/name)

### REST API 디자인 가이드
> RESTful하게 api를 만드는 규칙이다.  
> URI는 Resource를 표현해야 한다.  
> Resource에 대한 행위는 HTTP Method (GET, PUT, POST, DELETE등등)로 표현한다.  
#### REST API 기본 규칙
1. URI는 정보의 자원을 표현해야 한다.
```
GET /course/insert/inform -- X
GET /course/inform -- O
```  
HTTP Method (GET, PUT, POST, DELETE등등)의 행위가 URI 표현으로 들어가서는 안된다.  
2. 자원에 대한 행위는 HTTP Method (GET, PUT, POST, DELETE등등)로 표현한다.
```
DELETE /members/1
```   
HTTP Method(GET, PUT, POST, DELETE등등)로 행위로 CRUD를 할 수 있다.  
#### REST API 규칙
1. **슬래시 구분자( / )**는 계층 관계를 나타내는데 사용한다.
2. URI 마지막 문자로 슬래시( / )를 포함하지 않는다.
3. **하이픈( - )**은 URI 가독성을 높이는데 사용한다.
   - 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높인다.
4. **밑줄( _ )**은 URI에 사용하지 않는다.~~(다 바꿔야되네;)~~   
   - 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 하므로 가독성을 위해 밑줄은 사용하지 않는다.
5. URI 경로에는 **소문자**가 적합하다.
6. **파일확장자**는 URI에 포함하지 않는다.  
   - REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다.
```
http://test.com/test.jpg -- X
http://test.com/test -- O
GET /test HTTP/1.1
Host: test.com
Accept: image/jpg
```

### HTTP 응답 코드
```
- 1xx : 전송 프로토콜 수준의 정보 교환
- 2xx : 클라어인트 요청이 성공적으로 수행됨
- 3xx : 클라이언트는 요청을 완료하기 위해 추가적인 행동을 취해야 함
- 4xx : 클라이언트의 잘못된 요청
- 5xx : 서버쪽 오류로 인한 상태코드
```
#### 성공 (200~)
```
- 200 :	정상적으로 수행
- 201 :	자원(Resource) 생성 요청. 성공적으로 수행됨
```
#### 클라이언트 에러(Client Error) (400~)
```
- 400 :	클라이언트 요청이 부적절할 경우 응답 코드
- 401 :	클라이언트가 권한이 없는 자원(Resource)를 요청하였을 때 응답 코드
- 403 :	보호되는 자원(Resource)를 요청하였을 때 응답 코드
- 405 :	클라이언트가 요청한 리소스에서는 사용 불가능한 Method를 이용했을 때 응답 코드
```
#### 기타
```
- 301 :	클라이언트가 요청한 리소스에 대한 URI가 변경 되었을 때 응답 코드
- 500 :	서버에 뭔가 문제가 있을때 사용하는 응답 코드
```

> 출처:  
> https://da-14.com/blog/ultimate-guide-api-architecture-rest-soap-or-graphql  
> https://hwasurr.io/api/rest-graphql-differences/
> http://blog.wishket.com/soap-api-vs-rest-api-%EB%91%90-%EB%B0%A9%EC%8B%9D%EC%9D%98-%EA%B0%80%EC%9E%A5-%ED%81%B0-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%80/
> https://www.howtographql.com/basics/1-graphql-is-the-better-rest/ 
> https://mygumi.tistory.com/55
> https://nesoy.github.io/articles/2017-02/REST
> https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html