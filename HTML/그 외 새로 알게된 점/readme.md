# 새로 알게된 점


## HTML5 스타일 가이드
> html5 에서 사용하는 스타일 가이드  
https://www.w3schools.com/html/html5_syntax.asp  
http://www.w3bai.com/ko/html/html5_syntax.html      

> 그 외에도 다양한 기업 등에서 각자의 스타일 가이드가 존재한다.  
> Google HTML/CSS 스타일 가이드 : https://google.github.io/styleguide/htmlcssguide.html#Background  

<details>
  <summary>HTML5 스타일 가이드</summary>

### 올바른 문서 형식을 사용하여
- 항상 문서 유형을 문서의 첫 번째 줄로 선언하십시오
true    
```html
<!DOCTYPE html>
```  

false    
```html
<!doctype html> 
``` 


### 소문자 요소 이름을 사용
- 소문자 요소 이름을 사용하는 것이 좋습니다.

bad  
```html
<SECTION> 
  <p>This is a paragraph.</p>
</SECTION>
```

very bad  
```html
<Section> 
  <p>This is a paragraph.</p>
</SECTION>
```

good  
```html
<section> 
  <p>This is a paragraph.</p>
</section>
```

### 모든 HTML 요소 닫기
- XML 소프트웨어가 페이지에 액세스 할 것으로 예상되는 경우(그냥 모든 상황에서) 닫기 슬래시를 유지하는 것이 좋습니다.  

bad  
```html
<meta charset="utf-8">
```

good  
```html
<meta charset="utf-8" />
```

### 소문자 속성 이름 사용

- 개발자는 일반적으로 소문자 이름을 사용합니다 (예 : XHTML).  
bad  
```html
<div CLASS="menu">
```

good  
```html
<div class="menu">
```


### 견적 속성 값
- HTML5는 따옴표없이 속성 값을 허용합니다.
- 값에 공백이 있으면 따옴표를 사용해야합니다.

very bad  
```html
<table class=table striped>
```
bad  
```html
<table class=striped>
```
good  
```html
<table class="striped">
```

### 이미지 속성
- 항상 alt이미지에 속성을 추가하십시오 . 
- 또한 항상 이미지 너비와 높이를 정의하십시오. 
> - 로드하기 전에 브라우저가 이미지 공간을 예약 할 수 있기 때문에 깜박임 현상이 줄어 듭니다.


bad   
```html
<img src="html5.gif">
```
good   
```html
<img src="html5.gif" alt="HTML5" style="width:128px;height:128px">
```

### 공백과 등호
- HTML5는 등호 주위에 공백을 허용합니다. 
- 그러나 공간이 적은 것은 읽기 쉽고 엔티티를 더 잘 그룹화합니다.

bad  
```html
<link rel = "stylesheet" href = "styles.css">
```
good   
```html
<link rel="stylesheet" href="styles.css">
```
> 이건 모르고 있었음  

### 긴 코드 라인 피하기

- 80 자보다 긴 코드 행을 피하십시오.

### 빈 줄과 들여 쓰기

- 이유없이 빈 줄을 추가하지 마십시오.
- 가독성을 위해 빈 줄을 추가하여 큰 코드 블록이나 논리 코드 블록을 분리하십시오.
- 가독성을 위해 두 개의 들여 쓰기 공백을 추가하십시오. 탭 키를 사용하지 마십시오.
- 불필요한 빈 줄과 들여 쓰기를 사용하지 마십시오. 모든 요소를 ​​들여 쓸 필요는 없습니다.

bad  
```html
<body>
 
  <h1>Famous Cities</h1>
 
  <h2>Tokyo</h2>
 
  <p>
    Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
    and the most populous metropolitan area in the world.
    It is the seat of the Japanese government and the Imperial Palace,
    and the home of the Japanese Imperial Family.
  </p>
 
</body>
``` 

<br>

good  
```html
<body>
 
<h1>Famous Cities</h1>
 
<h2>Tokyo</h2>
<p>Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
and the most populous metropolitan area in the world.
It is the seat of the Japanese government and the Imperial Palace,
and the home of the Japanese Imperial Family.</p>
 
</body>
```

### &#60;html>과 &#60;body>를 생략 하시겠습니까?

- 그러나 태그 &#60;html>와 &#60;body>태그 는 생략하지 않는 것이 좋습니다 .
- &#60;html>요소는 문서 루트입니다. 페이지 언어를 지정하는 데 권장되는 장소입니다.

good  
```html
<!DOCTYPE html>
<html lang="en-US">
```
- 접근성 응용 프로그램 (화면 판독기) 및 검색 엔진에 언어를 선언하는 것이 중요합니다.
- -> 검색엔진이나 스크린리더 사용할 수 있으니 언어를 선언해라
- DOM 및 XML 소프트웨어를 생략 &#60;html>하거나 &#60;body>충돌시킬 수 있습니다.
- 생략 &#60;body>하면 구형 브라우저 (IE9)에서 오류가 발생할 수 있습니다.

### &#60;head>를 생략 하시겠습니까?
- 그러나 &#60;head>태그를 생략하지 않는 것이 좋습니다 .
- 태그를 생략하면 웹 개발자에게는 익숙하지 않습니다. 

### 메타 데이터

- 이 &#60;title>요소는 HTML5에 필요합니다. 제목을 가능한 한 의미있게 만드십시오.
- 적절한 해석과 올바른 검색 엔진 색인화를 위해 언어와 문자 인코딩 모두를 문서에서 가능한 한 빨리 정의해야합니다.
  
good  
```html
<!DOCTYPE html>
<html lang="en-US">
<head>
  <meta charset="UTF-8">
  <title>HTML5 Syntax and Coding Style</title>
</head>
```


### 뷰포트 설정하기
- &#60;meta>모든 웹 페이지에 다음과 같은 뷰포트 요소를 포함해야 합니다.

good  
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
- 팁 : 휴대전화나 태블릿으로 이 페이지를 탐색하는 경우 아래 두 링크를 클릭하여 차이점을 확인할 수 있습니다.

[설정하지 않은 경우](https://www.w3schools.com/html/example_withoutviewport.htm)
[설정한 경우](https://www.w3schools.com/html/example_withviewport.htm)


### HTML 주석
- 짧은 주석은 다음과 같이 한 줄로 작성해야합니다.

good  
```html
<!-- This is a comment -->
```

- 두 줄 이상에 걸쳐있는 주석은 다음과 같이 작성해야합니다
good  
```html
<!-- 
  This is a long comment example. This is a long comment example.
  This is a long comment example. This is a long comment example.
-->
```

### 스타일 시트

- 스타일 시트에 연결하기 위해 간단한 구문을 사용합니다 (type 속성은 필요하지 않습니다).

good  
```html
<link rel="stylesheet" href="styles.css">
```

- 짧은 규칙은 다음과 같이 압축하여 작성할 수 있습니다.

good  
```css
p.intro {font-family: Verdana; font-size: 16em;}
```

- 긴 규칙은 여러 행에 작성해야합니다

good  
```css
body {
  background-color: lightgrey;
  font-family: "Arial Black", Helvetica, sans-serif;
  font-size: 16em;
  color: black;
}
```

### HTML로 자바 스크립트 로드하기

- 외부 스크립트를로드하는 데 간단한 구문을 사용하십시오 (type 속성은 필요하지 않습니다).
good  
```html
<script src="myscript.js"></script>
```

### 소문자 파일 이름 사용
- 일부 웹 서버 (Apache, Unix)는 파일 이름에 대소 문자를 구분합니다. "london.jpg"는 "London.jpg"로 액세스 할 수 없습니다.
- 다른 웹 서버 (Microsoft, IIS)는 대소 문자를 구분하지 않습니다. "london.jpg"는 "London.jpg"또는 "london.jpg"로 액세스 할 수 있습니다.
- 대문자와 소문자를 혼용하면 매우 일관성이 있어야합니다.
- 이러한. 제를 피하려면 항상 소문자 파일 이름을 사용하십시오.

</details>

## section 내부에는 h1-6이 먼저 들어가지 않으면 유효성 검사에서 Worning 이 발생한다.
- 각각의 section을 식별할 수단이 필요하기 때문. 

## 툴팁을 추가하는 속성
- <a href="../전역%20속성/README.MD#title">전역 속성 title</a>


## table 추가
- <a href="../목록과 표/README.MD#table">table</a>
- table th는 테이블의 tr 요소의 자식으로 어디든 작성 가능하다!
- td의 기본 속성 : 왼쪽 정렬

## hgroup
- HTML hgroup 요소는 다수의 h1~6 요소를 묶을 때 사용한다.
- html5에서 처음으로 등장하였으나 현재는 W3C HTML5 명세에서 제거되었고, WHATWG판 HTML에만 남아있다.
- 그러나 대부분의 브라우저에서 부분적으로 구현중이므로 사라지지는 않을 것
- W3C HTML5 명세에서는 다양한 방법으로 hgroup없이 hgroup으로 사용하던 기능을 구현하는 방법을 설명한다.
  1. header 요소를 사용하는 방법
  2. 같은 요소 내부에 :(콜론) 으로 구분
  3. span 과 br을 이용하는 방법
```
<h1>Ramones <br>
<span>Hey! Ho! Let’s Go</span>
</h1>
```
...  

## font-variant 속성
- 글꼴에 대한 모든 변형을 적용시킨다.
### font-variant-alternates
> - 파이어폭스밖에 사용 안함..
### font-variant-caps
- 대문자에 대한 대체 글리프의 사용을 제어한다.
  - normal : 사용하지 않는다.
  - small-caps : 소문자를 대문자로 변환하지만 소문자 크기로 축소한다.
  - all-smaill-caps : 대문자 및 소문자 모두에 대해 작은 대문자 표시를 활성화한다.
  - petite-caps : 작은 대문자 대체 글리프를 사용한다.
### font-variant-east-asian
- 일본어 및 중국어와 같은 동아시아 스크립트에 대한 대체 글리프 사용을 제어한다.
### font-variant-ligatures
- 적용되는 요소의 텍스트 콘텐츠에 사용되는 합자 및 컨텍스트 형식을 제어합니다. 
  - normal : 적용
  - none : 비적용
### font-variant-numeric
- 숫자, 분수 및 서수 마커에 대한 대체 글리프의 사용을 제어합니다.
  - normal : 이 키워드는 이러한 대체 글리프 사용을 비활성화합니다.
  - slashed-zero
  - tabular-nums
  - oldstyle-nums


## 메타데이터 - OpenGraph
<head>
    <meta property="og:type" content="website">
    <meta property="og:title" content="페이지 제목">
    <meta property="og:description" content="페이지 설명">
    <meta property="og:image" content="http://www.mysite.com/myimage.jpg">
    <meta property="og:url" content="http://www.mysite.com">
</head>


## `&nbsp;`
[특수문자 리스트](http://kor.pe.kr/util/4/charmap2.htm)












