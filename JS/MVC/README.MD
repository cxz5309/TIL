# MVC 패턴, 

> MVC패턴에 대해서 다시 한번 정리해보기로 했다.  
> 장고를 하게 되면서 MTV모델을 학습하게 되었고 결과적으로 이름과 역할만 다르고 크게 다른 건 아니란 것을 알게 되었으나 와중에 거의 접해보지 못한 MVP, MVVM 모델에 대해서도 확실히 이해할 겸 작성하게 되었다.

## MVC 패턴

![image](https://media.prod.mdn.mozit.cloud/attachments/2018/06/08/16042/090bb2d2be010d2d547684a2d9ee41aa/model-view-controller-light-blue.png)
[출처](https://developer.mozilla.org/ko/docs/Glossary/MVC)

- MODEL-VIEW-CONTROLLER로 각각 역할을 나누어 코드의 역할을 분담시킨다.
- 얼마 전에 리액트에서 **단일 책임 원칙** 이라는 키워드를 발견했는데 거의 대체로 대형 웹앱들에서는 당연히 적용되는 작업이다.

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

### 간단한 앱을 통한 mvc 패턴 예시
```
const main = () =>{
    const model = new Model(storage);
    const views = {
        keywordListView: new KeywordListView(),
    }
    new Controller(store, views);
}
```
Model과 View를 Controller가 받아와서 사용한다.  

```
### - Controller
export default class Controller {
  constructor(
    store,
    {
      keywordListView,
    }
  ) {
    console.log(tag, "constructor");

    this.store = store;

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
export default class Store {
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
주로 데이터의 형태를 정의한다. 데이터는 직접 가지고 있지 않을 수도 있다.(보통 가지고 있지 않음)  

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
        this.bindEvents();
    }
}

class Template{
    getEmptyMessage(){
        return `<div class='empty-box'>추천 검색어가 없습니다</div>`
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

##
<!-- TODO
- 비슷한 장고 MTV 모델과의 비교
- MVP, MVVM 모델과의 비교 -->