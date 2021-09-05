# MVC패턴의 진화와 파생 패턴

> MVC패턴에 대해서 다시 한번 정리해보기로 했다.  
> 장고를 하게 되면서 MTV모델을 학습하게 되었고 결과적으로 이름과 역할만 다르고 크게 다른 건 아니란 것을 알게 되었으나 와중에 거의 접해보지 못한 MVP, MVVM 모델에 대해서도 확실히 이해할 겸 작성하게 되었다.

## MVC 패턴

![image](https://media.prod.mdn.mozit.cloud/attachments/2018/06/08/16042/090bb2d2be010d2d547684a2d9ee41aa/model-view-controller-light-blue.png)
[출처](https://developer.mozilla.org/ko/docs/Glossary/MVC)

- MODEL-VIEW-CONTROLLER로 각각 역할을 나누어 코드의 역할을 분담시킨다.
- 얼마 전에 리액트에서 **단일 책임 원칙** 이라는 키워드를 발견했는데 거의 대체로 대형 웹앱들에서는 당연히 적용되는 작업이다.
- 코드의 역할을 분담함으로써 대형 프로젝트에서 맡은 부분의 개발에만 집중할 수 있게 된다.
- 유지보수, 확장성, 개발의 유연성이 늘어난다

### MODEL
- 모델은 앱이 포함해야 할 데이터를 정의한다.
- 비즈니스 로직을 처리하고 VIEW나 CONTROLLER 로 데이터를 보낸다.
- 같은 종류의 데이터는 같은 모델 클래스를 공유한다.
> - 보통 DB의 테이블의 형태를 띄고 있는 경우가 많으며 ORM 사용시 ORM에 맞게 쓰여진다.

### VIEW 
- 앱의 데이터를 보여주는 방식을 정의한다.
> - 주로 렌더링되는 상황에서의 작업 알고리즘이 존재, 렌더링되는 데이터를 모델로부터 받아오거나 생성하여 보여지는 View를 정의한다.
> - 컨트롤러 하위에 종속되어 컨트롤러가 보여주려고 하는 View를 모두 가지고 있다.

### CONTROLLER
- 앱의 사용자로부터 입력에 대한 응답을 한다.
> - 이때 입력은 다양한 경우를 포함하는데, GET/ POST등의 페이지 입력이나 DOM 이벤트까지도 다양한 상황에서의 입력을 처리한다.
> - 동적으로 모델/ 뷰를 업데이트하며 다양한 처리 동작을 한다.
> - 보통 Model을 1차 처리하여 View로 전송한다.(Model과 View의 중개인 역할)

### 간단한 앱을 통한 MVC 패턴 예시
```
const main = () =>{
    const model = new Model(storage);
    const views = {
        keywordListView: new KeywordListView(),
    }
    new Controller(model, views);
}
```
Model과 View를 Controller가 받아와서 사용한다.  

```
### - Controller
export default class Controller {
  constructor(
    model,
    {
      keywordListView,
    }
  ) {
    console.log(tag, "constructor");

    this.model = model;

    this.keywordListView = keywordListView;

    this.subscribeViewEvents()
    this.render();
  }
...
```
보통 Controller의 constructor(생성자)에는 render 함수가 있어 Model을 View로 바로 연결하고, View를 화면에 송출해준다.  
> - Model 내용이 변경되더라도 별다른 수정 없이 View를 바꾸어 줄 수 있다(코드의 재사용성, 생산성)

### - Model
```
export default class Model {
  constructor() {
    console.log(tag, "constructor");

    if (!storage) throw "no storage";

    this.storage = {
      keywordData: [
        { id: 1, keyword: "샐러드" },
        { id: 2, keyword: "커리" },
        { id: 3, keyword: "햄버거" },
      ],
      ...
    }

    this.searchKeyword = '';
    this.searchResult = [];
    this.selectedTab = TabType.KEYWORD;
  }
}
```
주로 데이터의 형태를 정의한다. 데이터는 직접 가지고 있지 ~~않을 수도 있다~~.(대부분 DB에 넣고 가지고 있지 않음)  

### - View

```
export default class View {
  constructor(element) {
    console.log(tag, "constructor");

    if (!element) throw "no element";

    this.element = element;
    this.originalDisplay = this.element.style.display || "";

    return this;
  }

```

```
export default class KeywordListView extends View{
    constructor(element = qs('#keyword-list-view'), template = new Template()){
        console.log(tag, "constructor");
        super(element);

        this.template = template;
    }
}

class Template{
    getEmptyMessage(){
        return `
          <div class='empty-box'>추천 검색어가 없습니다</div>
        `
    }

    getList(data = []){
        return `
        <ul class='list'>
            ${data.map(this._getItem).join('')}
        </ul>`
    }

    _getItem({id, keyword}){
        return `
        <li data-keyword=${keyword}>
            <span class='number'>${id}</span>
            ${keyword}
        </li>`
    }
}
```
렌더링되는 상황에서의 동작을 정의하거나 View를 가지고 있다  

---


## MVC 패턴2
> 한참 MVC패턴을 조사하고 있으니까 아무리 생각해도 이상했다.  
> Model, View, Controller를 이어주는 화살표가 설명하는 글마다 다르고 제멋대로인 것이다..  
> 이유를 알아보기로 하였다.  

![MVC 패턴 검색결과](../../public/JS/mvc패턴검색결과.png)
(MVC 패턴 검색 결과)  
조금 조사해보면 알겠지만 화살표가 진짜 다 제멋대로이다.  

https://imcts.github.io/MVC-PATTERN/  
https://maverick2k.tistory.com/201  
이 블로그 등에서 힌트를 얻었다.

![MVC1](https://imcts.github.io/images/2019-02-05-MVC-PATTERN/mvc1.png)  
아마도 초기의 MVC 패턴에서 각자의 역할은 자세하지 않았던 것 같다.  

- 디자인 패턴이 결국 개발 과정에서 자주 발생하는 문제를 해결하는 방법을 패턴화한 것이므로 디자인 패턴은 시대에 따라 변화하고, 발전할 수 있다.
> 그 예라고 할 수 있을진 모르겠으나 자바 spring의 탄생 배경을 알아보면 프로그래밍 기술의 패러다임 변경과 발전을 느낄 수 있다.  
- 또한 패턴이란 것이 정해진 기술이 아니므로 구현에 따라, 사람의 관점에 따라 말해지는 것이 달라지기도 한다.
> [페이스북조차 MVC 패턴에 대한 관점이 다르다](https://blog.coderifleman.com/2015/06/19/mvc-does-not-scale-use-flux-instead/)
> 아무튼 이래서 Flux 패턴을 보완한 React의 Redux가 탄생하였다.

![MVC2](https://media.prod.mdn.mozit.cloud/attachments/2018/06/08/16042/090bb2d2be010d2d547684a2d9ee41aa/model-view-controller-light-blue.png)  
출처: https://developer.mozilla.org/ko/docs/Glossary/MVC  
이후에는 이런 느낌이 된 것 같다.  
<br>
하지만 역시 ~~우리가 알고있는~~(내가 알고있는) MVC패턴과 화살표가 조금 다르다.(MODEL -> VIEW)  

- 이때까지의 MVC 패턴에서 Controller의 역할은 Model을 업데이트하고, Model을 나타내줄 View를 선택하기만 할 뿐이었다.  
- 따라서 View는 Model을 이용하여 화면을 나타내게 된다.
- 이 패턴은 오히려 View와 Model사이의 의존성이 높아지게 된다.

이때 이런 개념이 들어왔었나 보다.  

--- 

## [PAC 패턴](https://maverick2k.tistory.com/201)  
- 거의 알려지지 않은 패턴이지만 이후의 MVC패턴의 기본 개념이 PAC 패턴이라고 부르는 패턴의 개념과 동일해졌다.  

![MVC3](https://imcts.github.io/images/2019-02-05-MVC-PATTERN/mvc2.png)  
**그리고 현재 ~~대부분의 웹 개발자들이 인식하고 있는~~ MVC패턴이 완성되었다.**  
- 현재의 MVC 패턴은 제왕적 컨트롤러 방식의 MVC패턴이다.
- Controller가 Model과 View의 데이터를 다루고 Model과 View는 서로에 대해 거의 간섭하지 않으며 스스로 동작하지 않는다. 
  - 설계 이유는 Model과 View의 변화율이 다르기 때문인데, 즉 Model의 데이터가 변화되는 숫자만큼 View의 변화가 없을 수도 있게 되는 것이다(없다).  
  - 이것이 직접적으로 영향을 주게 된다면 경우에 따라 성능에 영향을 줄 것이다.  
  - View와 Model사이의 의존성 문제를 없앴다.

---

## 이후의 패턴들
이후 기술할 몇가지 문제점들로 인해 MVC패턴은 다양한 파생 패턴들이 생겨났다.  
<a href="#mvp">MVP패턴</a>   
<a href="#mvvm">MVVM패턴</a>   
<a href="#flux">Flux패턴</a>   
(조사하고 보니 파생 패턴이 생겨난 이후 MVC패턴이 현재 상태로 진화하였다.)  

---

## MTV 패턴
> 이 글을 쓰게 된 이유이자 요즘 django를 배우고 있기 때문에 MVC패턴과 뭐가 다른가 알아보게 된 패턴이다.  
> 결론부터 말하자면 이름만 다르지 하는 일은 비슷하다.  

![MTV](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCHnnn%2FbtqFBYBTv99%2FxU7eTE2nOcJazmjINginUk%2Fimg.png)  
출처: https://dw3232.tistory.com/14  
Django의 MTV 패턴  
  
### Model
- MVC 패턴의 Model과 같다. 
- db 데이터의 형태를 정의하거나 사전처리를 한다.

### Template
- MVC 패턴의 View와 같다. 
- HTML과 비슷하지만 엄연히 다른 [장고 템플릿 시스템 문법](https://runebook.dev/ko/docs/django/ref/templates/language)을 사용한다.
- HTML 작업에 익숙한 사용자에게 편안한 느낌을 주도록 설계되었기 때문에 퍼블리셔에게 친화적으로 그 부분만 집중할 수 있게 하여 생산성에 도움을 준다.

### View
- MVC 패턴의 Controller와 같다.
- 사용자에게 이벤트를 받고, 데이터를 템플릿에서 활용하여 다시 사용자에게 보내준다.

### URLconf - URL 설계
- django MTV패턴만의 특별한 과정이다. 
- 파이썬의 직관적인 URL 지정 방식을 이용하여 URLconf 모듈이 URL을 분석한 후 처리를 담당할 View와 연결해준다.
#### URLconf의 URL 분석 순서
  1. setting&#46;py 파일의 ROOT_URLCONF 항목을 읽어 URLconf(urls&#46;py)의 위치를 알아낸다.
  2. URLconf 모듈을 로딩하여 urlpatterns 변수에 지정되어 있는 URL 목록을 검사한다.
  3. 위에서부터 순서대로 URL 목록의 내용을 검사하면서 매치가 되면 검사를 종료한다.
  4. 매치가 된 URL의 뷰를 호출한다. 여기서 뷰는 함수 또는 클래스의 메소드 이다. 호출 시 HttpRequest 객체와 매칭할 때 추출된 단어들을 뷰에 인자로 넘겨 준다.
  5. 목록 끝까지 검사했는데도 매칭에 실패하면 에러를 처리하는 뷰를 호출한다. 


---

## MVP 패턴, MVVM 패턴

[자바 코드를 통한 차이점 예시](https://wellohorld.tistory.com/152)


---

## <a name="mvp">MVP 패턴</a>
- MVC 패턴과 비슷하지만 Controller가 Presenter로 바뀌었다. 
- MVC패턴의 문제점을 보완하였다.

### MVC패턴의 문제점
- MVC패턴에서는 뷰에 역할이 정해지지 않았기 때문에 Controller의 코드가 너무 비대해지고 View와 Model 사이의 의존성이 너무 높아지게 된다.(가장 최신의 MVC패턴 이전의 패턴)

### Presenter
- 뷰에 연결되는 것이 아니라 단순한 인터페이스로써 쓰인다.
- Controller와 View가 1:N 대응인 것과 다르게 Presenter와 View는 1:1 대응이 된다.
- 이로써 View와 Model간의 의존성을 해결하였다.

---
## <a name="mvvm">MVVM 패턴</a>
- MVP 패턴과 비슷하지만 Presenter가 ViewModel로 바뀌었다. 
- MVP패턴의 문제점을 보완하였다.

### MVP패턴의 문제점
- MVP패턴은 MVC패턴의 Model과 View간의 의존성을 없앴으나 View와 Presenter간의 의존성이 강해졌다.

### MVVM패턴의 동작
- MVVM패턴은 Command 패턴을 사용하여 ViewModel에 View의 Action을 전달한다.
- ViewModel은 Model에게 결과에 따른 데이터를 요청한 후 가공한다.
- View는 ViewModel과 Data Binding을 통해 화면을 나타낸다.

### 장점
- Command 패턴과 Data Binding을 이용하여 View와 View Model 사이의 의존성을 없앴다.
- 의존성을 최소화한 결과 변화 대응의 용이성이 가장 좋아진 패턴이다.

---

## <a name="flux">FLUX 패턴</a>

### MVC패턴의 문제점
- 데이터의 흐름이 양방향이며, 의존적이고, 연쇄적이다.
- 이렇게 뒤얽힌 데이터 흐름은 대형 어플리케이션에서 예측할 수 없는 결과를 만들어낸다.

![MVC단점](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FALrHe%2FbtqBTMSuHfN%2FZlW9i9ET34e90APgCRChk1%2Fimg.png)  
출처: https://beomy.tistory.com/44  
페이스북에서 말하는 MVC패턴의 단점  

### FLUX패턴

- Flux 패턴은 데이터를 단방향으로 흐르게 만들었다.
- 이것은 데이터의 변화를 예측하기 쉽도록 만들었다.
- redux의 아이디어로써의 의의가 있다..?

![FLUX](https://facebook.github.io/flux/img/overview/flux-simple-f8-diagram-with-client-action-1300w.png)   
출처: https://beomy.tistory.com/44  

### Dispatcher
- 앱의 모든 데이터 흐름을 관리한다.
- Action이 발생되면 Action을 받아와서 등록된 콜백 함수를 통해 Store에 전달한다.

### Store
- 앱의 모든 상태 변경을 담당한다.
- Dispatcher로부터 콜백 함수를 통해 수신받는다.
- Store의 변경은 View에 전달된다.
- 싱글톤으로 관리된다.(앱 전체에서 상태를 알 수 있다.)

### View
- 화면에 나타내는 것 뿐 아니라, 자식View로 데이터를 흘려보내는 뷰 컨트롤러의 역할도 함께 한다.

##### redux는 react 폴더에 기술할 예정

---

## 결론
생각치도 못했던 일인데 개발자들이 말하는 MVC 패턴에 대한 정의와 구조는 정말 다양하다.  
그 이유는 MVC패턴이 시간이 지날수록 형태를 바꾸어 진화해왔기 때문이고, 개발자들끼리도 구현과 각자의 정의가 다르기 때문이다.  
게다가 그 변화가 인터넷 세계에서는 항상 최신화되지 않기 때문에 옛날 자료를 지금도 새것처럼 쓰기도 하는 등 혼동이 올 수밖에 없다.  
심지어 프론트엔드, 백엔드, 언어에 따라 가능한 일과 불가능한 일, 사용 의의 등이 다 달라서 더 제멋대로이다..  

<br>

어떤게 뛰어나다거나 한 것은 없다. 각자 모두 장단점을 가지고 있다. 패턴의 설계 의의와 용도를 잘 파악해야 한다.  
빠르게 변화하는 프로그래밍 기술과 패러다임에 따라갈 필요가 있겠다;  