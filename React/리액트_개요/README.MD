# 리액트 개요

## 리액트란?
> React는 웹 프레임워크로, 자바스크립트 라이브러리의 하나로서 사용자 인터페이스를 만들기 위해 사용된다.
- React는 facebook에서 만든 프론트엔드 라이브러리라고 볼 수 있다.
- 싱글 페이지 애플리케이션이나 모바일 애플리케이션의 개발 시 토대로 사용될 수 있다.

즉, 현재 많이 활용되고 있는, 웹/앱의 View를 개발할 수 있도록 하는 인기있는 라이브러리라고 볼 수 있다.

- 특정 값에 의존해 자동으로 반응하는 것을 리액티브(reactive) 하다라고 표현한다.
- 리액트를 비롯한 모던 UI 라이브러리는 이러한 리액티브한 특징을 가지고 있다. MVC 모델에서는 컨트롤러가 데이터와 뷰를 직접 관리한다. 어플리케이션을 동작시킬 때 모델도 변경하고 뷰도 빠짐없이 챙겨야하는 것이다.
- React는 뷰모델을 변경하는 것만으로 UI를 자동으로 갱신하기 때문에 어플리케이션의 움직이는 모습을 기술하는 것 보다 상태만 기술하는 방식이 더 선언적이고 읽기 쉬운 코드를 만들 수 있다.
-  
## 리액트의 특징
## 1. 가상 돔(Virtual DOM)
리액트는 가상 돔을 사용하여 웹 애플리케이션의 성능을 극대화 시켰다.  
가상 돔을 이해하기 위해서는 우선 HTML과 CSS가 렌더링(Rendering) 되는 과정을 이해해야 하는데  
### 브라우저의 UI 연산 과정
![브라우저의 UI 연산 과정](https://d2.naver.com/content/images/2015/06/helloworld-59361-1.png)  
브라우저(Chrome, Firefox, Safari, IE 등)에서 사용자 인터페이스 즉, UI를 구성하는데는 위와 같은 과정을 거친다.  
<br>

여기서 렌더링 엔진의 동작 과정을 자세히 살펴보면  
![웹킷 동작 과정](https://d2.naver.com/content/images/2015/06/helloworld-59361-3.png)  
**웹킷 동작 과정**  
![모질라의 게코 렌더링 엔진 동작 과정](https://d2.naver.com/content/images/2015/06/helloworld-59361-4.png)   
**모질라의 게코 렌더링 엔진 동작 과정**  

[참고] https://d2.naver.com/helloworld/59361

1. Parser - 각 파일들을 브라우저가 알아들을 수 있게 변환.
2. DOM Tree - 파일의 경우, 각 태그의 관계도 형성을 위해 DOM 트리 생성.
3. Attachment - HTML의 각 태그에 맞는 스타일(CSS. 정보를 객체 형태로 다음 단계로 넘겨줌.
4. Render Tree - 외부 CSS 파일이 선언되어있다면 이를 필요료 하는 각 HTML 엘리먼트에 결합 후, 이전 Attachment에서 전달받은 스타일 값 들을 계산, 그리고 레이아웃 정보 형성.
5. Layout - 렌더 트리 작업이 끝난 레이아웃에 대해서 좌표 부여.
6. Painting - 렌더링이 끝난 각 레이아웃들에게 실제 사용자에게 보여질 모양과 색 부여.  

- 주요렌더링경로(Critical Render Path)라고도 불리는 이 과정은 자바스크립트로 돔 구조를 변경하면 레이아웃다시 계산에 픽셀로 화면에 다시 그린다. 
- 돔을 수정한만큼 이 작업이 반복되기 때문에 페이지 렌더링 성능에 영향을 주는 요소이다.
<br>

이제 맨 위의 DOM의 역할을 알아보자  
> DOM(Document Object Model) 은 문서객체모델로써 HTML 파일에서 정의한 각 태그의 관계도(Tree 구조)를 정의해주고, 각 태그에 대한 저장 및 조작접을 제공해준다.
html파일을 해석하여 트리 구조로 관계를 정의하고, 조작할 수 있는 조작점을 만들어준다.  
하지만 이 DOM은 트리구조로 되어있어서 이해하기 쉽다는 장점이 있지만, 이러한 처리과정은 브라우저에 어떠한 작은 변화가 있을 때마다 위의 작업들을 계속적으로 반복하며 다시 레이아웃을 형성하게 된다.   
<br>

이러한 구조 덕분에 거대한 DOM 트리에서는 속도 이슈가 발생하였고 지속적인 DOM 업데이트는 잦은 오류와 사용자 인터페이스에 악영향을 끼쳤다.  
또한 DOM을 제대로 찾지 못한다면 코드를 분석하려고 다시 거대한 HTML을 들여다 봐야 하는 단점이 존재했다.  

### 가상 돔 연산 과정

[**react 가상 돔 문서**](https://ko.reactjs.org/docs/faq-internals.html#gatsby-focus-wrapper)

- 돔에서 일어나게 될 변화를 가상 돔에서 브라우저의 처리과정 중 렌더링 과정까지(Painting, Display 단계는 거치지 않음) 진행하면서 그 기록을 저장해두고, 실제 DOM에게 그 변화의 결과만을 전달해주어, 사용자에게 보여주게 된다.

규모가 큰, 특히나 SPA 방식의 웹 어플리케이션 같은 경우 사용자 인터랙션으로 일어나게 될 변화의 양은 적게는 수십번, 많게는 수천번까지 된다.  
그렇게되면 위와 같은 브라우저 처리과정을 수십번에서 수천번까지 실제 돔에서 계속적으로 렌더링과 페인팅, 디스플레이 과정을 거치면서 UI가 형성되어진다.  
<br>

하지만, 가상 돔 같은 경우 이러한 변화의 양을 한번에 묶어서 최종적으로 계산된 레이아웃의 정보만 실제 DOM에게 던져주게 된다. 이렇게 되면 브라우저의 연산 양이 기존보다 적어지게 되므로 자연스럽게 사용자에게 보다 쾌적한 UI 경험을 제공할 수 있게 된다.
![**가상 돔 렌더 방식**](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbsK2db%2FbtqCoR6Sefb%2FbWCCnmtGeZKkabCwwxBCn0%2Ftfile.svg)

React 뿐만아니라 Vue또한 이러한 Virtual DOM 방식을 채택하였다.

## 2. JSX
> - JSX(JavaScript XML)는 자바스크립트의 확장 문법이다. 
> - UI 다루는 코드의 가독성을 높이기 위해 고안된 문법이다. 
> - 기본 자바스크립트의 createElement() 함수를 직접 사용하는 방식은 읽기 어려운 UI 코드를 만들 수 밖에 없기 때문에 등장하였다.
> - 컴포넌트가 한가지 책임을 진다라는 점에서 표현력이 좋다.

- JSX는 마치 마크업 문법과 같다.  
```
<h1>Hello world</h1>
``` 
-> BABEL PARSER
```
React.createElement('h1', null, 'Hello world')
```

- React와 JSX를 사용해 렌더링까지 하면
```
// 1
const element = (
  <header>
    <h1>Hello world</h1>
  </header>
)

// 2
ReactDOM.render(element, document.querySelector("#app"))
```
이렇게 표현할 수 있다  
<br>

JSX는 자바스크립트 표현식이기 때문에 값으로 평가되고 반환된 리액트 앨리먼트를 element 상수에 할당했다.  
이 엘리먼트를 ReactDOM.render()에 전달하면 가상돔을 만들고 이걸 "#app" 엘리먼트에 붙여 렌더링되고 우리눈에 "hello world"란 텍스트를 볼 수 있는 것이다.  
  
[리액트 JSX 소개](https://reactjs-kr.firebaseapp.com/docs/introducing-jsx.html)
- JSX에 표현식 포함하기
  - JSX 안에 자바스크립트 표현식 을 중괄호로 묶어서 포함시킬 수 있다.
```
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);
```
- JSX 또한 표현식이다
  - 컴파일이 끝나면, JSX 표현식이 정규 자바스크립트 함수 호출이 되고 **자바스크립트 객체**로 인식된다.
  - 이 말은 if 문이나 for 반복 내에서 JSX를 사용할 수 있으며, 변수에 할당하거나 매개 변수로 전달하거나 함수에서 반환할 수 있음을 의미한다.
  - 
- JSX 속성 정의
  - 속성에 따옴표를 이용해 문자열 리터럴을 정의
  - 속성에 중괄호를 이용해 자바스크립트 표현식을 포함시킬 수 있다.
- JSX 인젝션 공격 예방
  - 유저 입력을 JSX 내에 포함시키는 것이 안전
```
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```
- JSX 객체 표현
  - Babel은 JSX를 React.createElement() 호출로 컴파일한다.

## 3. Component 기반 구조
- 엘리먼트가 리액트 앱을 구성하는 최소단위라면, 컴포넌트는 UI를 나타내는 엘리먼트와 어플리케이션 로직을 포함한 상위 개념이다.   
- 로직은 컴포넌트의 상태를 변경하면서 UI 엘리먼트를 제어한다.   
- 매개변수를 input으로 하고 UI가 어떻게 보여야 하는지 정의하는 React Element를 output으로 하는 함수.  
- 따라서 합성을 이용하여 “UI를 재사용할 수 있고 독립적인 단위로 쪼개어 생각”할 수 있게 한다.  

### 컴포넌트의 라이프사이클

- 컴포넌트는 각 프로세스가 진행될 때에 따라 Lifecycle 함수로 불리는 특별한 함수가 실행된다.  
- 개발자는 이를 재정의하여 컴포넌트를 제어하게 된다.  
   
![라이프사이클](https://kyun2da.dev/static/69e54fe57da139eabae168b5e8304af4/01645/lifecycle.png)
1. Mounting(생성)
   - 컴포넌트가 시작되면 우선 context, defaultProps와 state를 저장한다. 그 후에 componentWillMount 메소드를 호출한다. 그리고 render로 컴포넌트를 DOM에 부착한 후 Mount가 완료된 후 componentDidMount가 호출된다.  
   - Creating 중인 componentWillMount()에서 Ajax 요청을 날리면 응답 시간만큼 컴포넌트를 그리는 것이 늦어짐을 알 수 있다.  
   - 따라서 일반적으로 componentDidMount()에서 Ajax 요청을 하는 게 낫다는 것을 알 수 있다.
   - 내부 실행순서
     1. state, context, defaultProps 저장
     2. componentWillMount
     3. render
     4. componentDidMount
2. Updating(갱신)
   - Receiving State 중에 setState() API를 호출하면 프로세스가 끝난 후 또다시 Receiving State 할 것을 알 수 있다. 
   - 따라서 setState() API를 해당 Lifecycle 함수에서 호출하면 무한 루프에 빠질 수밖에 없다는 것을 알 수 있다.
   - props update
     1. componentWillReceiveProps
     2. shouldComponentUpdate
     3. componentWillUpdate
     4. render
     5. componentDidUpdate
   - state update
     1. shouldComponentUpdate
     2. componentWillUpdate
     3. render
     4. componentDidUpdate
3. Unmounting(제거)
  
주의하여 볼 것은 업데이트 부분인데, 업데이트는 다음과 같은 4가지 상황에서 발생한다.    

1. props가 바뀔 때
2. state가 바뀔 때
3. 부모 컴포넌트가 리렌더링 될 때
4. this.forceUpdate로 강제로 렌더링을 트리거할 때

### props와 state
- 컴포넌트는 두 가지 인스턴스 속성(property) props와 state를 가지고 있다.  
- props는 컴포넌트의 mounting, updating 프로세스 시점에 값이 할당될 뿐 컴포넌트 내부에서 값을 변경할 수 없다.   
- 상황에 따라 변경되어야 하는 값들은 state를 이용해야한다.  
- 이것은 개발자들에게 명확한 관념 모델(static mental model)을 제공한다.  
- 관념 모델은 무엇이 어떻게 동작하는지 이해할 때 진행되는 일련의 사고 프로세스를 의미한다. 즉, 논리적으로 이치에 맞는 사고 모델을 제공한다는 것  
- 컴포넌트 간에는 무조건 props를 통해서만 데이터를 주고받고 props는 컴포넌트 내부에서 변경되지 않는다.   
- 따라서 위/아래 양쪽에 대해 동시에 고민할 필요가 없고 아래 한쪽 방향(uni-directional) 그리고 자기 자신에 대해서만 고민하면 된다.  
- 퍼포먼스 측면의 이점도 있다. 만약 props와 state가 하나의 객체로 관리된다면, Updating을 할지 결정하는 shouldComponentUpdate() 함수에서 O(keys(props+state))만큼 값이 변경되었는지를 비교해야 하지만, 애초에 props와 state로 분리되어 있으므로 O(keys(state))만큼만 비교하면 Updating을 결정할 수 있다.  
- setState()는 비동기로 동작한다.  
    - 끊김 없는 원활한 UI/UX를 제공하기 위해 일정 수의 render를 꼭 수행시키기 위해서  
    - state 변경이 많으면 많을수록 render는 모든 변경이 적용될 때까지 늦어지기 때문에 render 시점과 별개로 동작하게 하기 위함  
<!-- TODO
## 4. 단방향 데이터 흐름
## 5. Props and State

### 나중에 추가할 내용
## Element
- 기본 js에서의 element와 react에서의 element의 로그를 찍어보면 각각 HTMLParagraphElementPrototype, Object 타입이다.
- 즉 react에서의 element는 일반 오브젝트로써 작동하므로 element만으로는 화면에 적용이 불가능하다. -->