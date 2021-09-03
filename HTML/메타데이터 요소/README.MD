# 메타데이터

- 데이터를 위한 데이터
- 책의 저자, 발행일시 등과 같이 데이터의 설명을 해 주는 데이터이다.
- head태그에 내부에 들어가는 경우가 많다

---
## title
- 웹 페이지의 이름
- head내부에는 title이 하나만 들어갈 수 있다
- 이름은 실제 웹사이트 내에서 여러 효과를 준다(웹 태그에 보여지는 등)
- 'SEO : 검색 엔진 최적화' 에 도움을 준다

---
## meta
- 빈 요소이므로 속성에 정보를 나열한다

### name 속성
- contents 속성과 같이 사용하여 이름-값 쌍으로 문서의 메타데이터를 제공한다.
- 지향하는 표준 메타데이터 이름이 있다.
> [표준 메타데이터 이름](https://developer.mozilla.org/ko/docs/Web/HTML/Element/meta/name)
> - **표준 메타데이터 정보**
> application-name : title요소와 비슷하게 앱의 이름을 나타내지만 문서 이름이나 상태 등 다른 정보 삽입도 가능하다.
> description : 문서 설명
> generator : 페이지를 생성한 소프트웨어
> keywords : 검색 결과, 해시태그 느낌, 실제 동작은 하지 않는다
> referrer : http Referer 헤더를 content 값에 따라 통제한다.
> *refferrer content 값 일부 예시*
> - no-referrer : HTTP Referer 헤더를 전송하지 않는다.
> - origin : 문서의 출처를 전송
> - no-referrer-when-downgrade : 목적지가 현재 문서와 동일하거나 더 높은(HTTP(S)→HTTPS) 보안 수준을 가진 경우 전체 URL을 전송하고, 더 취약(HTTPS→HTTP)한 경우 전송하지 않습니다. 기본 동작 방식입니다.
> - strict-origin : 목적지가 현재 문서와 동일하거나 더 높은(HTTP(S)→HTTPS) 보안 수준을 가진 경우 출처를 전송하고, 더 취약(HTTPS→HTTP)한 경우 전송하지 않습니다.
> [HTTP 와 HTTPS의 차이점 을 알아보자](../HTTP%20와%20HTTPS의%20차이점/README.MD)
> theme-color : 다크모드 css를 적용할 때 추천되는 이름
> - *사용되는 값* : normal / [light|dark]+ /only light
> [다크모드 대응 방법을 알아보자](../../JS/다크모드/README.MD)
> viewport : 모바일에서 뷰포트의 초기 사이즈를 지정하기 위한 힌트
> *content 값 일부 예시*
> - 'width=device-width, initial-scale=1.0' : 뷰포트의 너비는 화면 너비만큼, 장치 너비와 뷰포트 너비는 1:1 비율로 한다
> - 'user-scalable=no' : 사용자가 웹 페이지를 확대할 수 없다. 
> - 'maximum-scale=10.0' : 웹 페이지를 확대했을때 최대 비율 1:10
> robots : 크롤러 또는 '로봇'의 동작을 지정(크롤링 또는 검색 엔진에 제약을 준다)
> 크롤링 하는 법..?<!--TODO>

### charset 속성
- 페이지의 문자 인코딩을 선언한다.
- 보통 UTF-8을 사용하는데 대부분 호환되나 특정 상황에서 깨진다

---
## link 
- 기본적으로는 css 연결할때 주로 쓴다.(자주 쓰인다는 뜻)
- 현재 문서와 외부 리소스와의 관계
### href 속성
- 하이퍼레퍼런스, 외부 리소스 링크
- 절대, 상대 url 모두 가능
### rel 속성
- 연결할 리소스와 현재 문서의 관계. 링크 유형의 값을 공백으로 구분하여 넣으라고 했는데 stylesheet나 icon, preload 말고는 잘 몰랐다.
> [링크 타입](https://developer.mozilla.org/ko/docs/Web/HTML/Link_types)
### type 속성
- 링크된 콘텐츠의 타입, css는 text/css(MIME타입)
- 동영상 같은 것을 불러올 때도 중요하다(video/mp4)
### 자주 사용되는 유형
```
<link href="main.css" rel="stylesheet">
<link rel="icon" href="favicon.ico">
<link rel="apple-touch-icon-precomposed" sizes="114x114"
      href="apple-icon-114.png" type="image/png">
<link href="print.css" rel="stylesheet" media="print">
```

---
## MIME타입
- 링크된 파일을 불러올 때 파일 경로를 해석하기 위해서 사용한다.
> [MIME타입](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types)
> [MIME타입의 전체 목록](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types)
> - 일반적인 구조 : type/subtype
> - 개별 타입 : text/html, image/jpeg, audio/mpeg, video/mp4
> text/plain은 txt파일

---
## style
- html내부에 style요소를 사용하여 스타일을 지정하는 방법
- 토이프로젝트에서 손이 많이 귀찮을때 사용할 듯
- 권장하지 않는다.

---
## script
- js 연결할 때 거의 쓰인다.
- html 내부에 직접 스크립트를 작성하기도 한다.
-  WebGL의 GLSL 셰이더 프로그래밍 언어, JSON 등 다른 언어와도 사용할 수 있다고 한다.
### src 속성
- 파일의 경로
### type 속성
- 스크립트의 유형
- 생략시 :  js
- js MIME 유형 : js
- module : 스크립트를 js모듈로 간주한다. 웹팩, babel등이 모듈 기반 시스템이다.
- 다른 모든 값 : 내장 콘텐츠를 브라우저가 처리하지 않을 데이터 블록으로 간주한다. (안쓴다)
### nomodule 속성
- 모듈을 사용하지 않는다는 뜻
- 모듈화 JavaScript를 지원하지 않는 오래된 브라우저(라고 말하면 거의 IE이다)
### defer 속성
- 브라우저가 스크립트를 문서 분석 이후에, 그러나 DOMContentLoaded 발생 이전에 실행해야 한다
- html분석 이전에 스크립트를 받아오는 지연을 막는데 효과적이다.async도 비슷한 효과를 가진다.
> **모듈 스크립트는 기본적으로 지연 평가하므로, defer를 지정해도 변화가 없다.**

