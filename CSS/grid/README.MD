# grid
- flexbox와 매우 동일하다.
- 기본적으로 main axis에만 여러개의 아이템이 있는 flexbox와 달리 행과 열을 가진 상태를 기본으로 삼는다.
- columns(행), rows(열), gutters(행과 열 사이의 공백) 을 가진다.
- 열병합, 행병합 등을 쉽게 할 수 있다.
  
## Container - display: grid (내부 display 요소) <a id="in_display_grid">#</a>
- <a href="../레이아웃/README.MD#out_display">#외부 display 요소</a>
> - 외부 display 요소와 `-대쉬`를 이용하여 같이 사용 가능하다.
> display: inline-grid; 가로로 그리드 생성

## Container - grid-template-rows, grid-template-columns
- 몇개의 행, 열을 갖게 될 것인지를 결정한다.
- 기본적으로 아이템의 개수만큼 자동으로 결정한 행 수와 열 수에 맞추어지고 개수가 벗어나게 되면 설정한 크기 대신 본래의 크기의 아이템이 된다.

### grid-template-columns
- 각 열의 크기를 나열하여 각 열의 크기와 개수만큼 열을 세팅한다.
### grid-template-rows
- 각 햏의 크기를 나열하여 각 행의 크기와 개수만큼 행을 세팅한다.
#### 값
- `<length>`
- `<percentage>`
- `<flex>` : 각각 아이템의 비율을 나타낸다.
  - `grid-template-columns: 1fr 1fr 2.5fr 1.5fr;`
- max-content : 최대 크기
- auto
- minmax(min, max) : auto와 같지만 최소, 최대값을 지정한다.
- repeat(n, arg) : arg를 n번 반복하는 값과 같다.

## Container - grid-template-areas
- 만들어놓은 그리드를 일정 영역으로 나눈다.
> - [grid-template-areas mdn 예제](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-areas)  
- 비우고 싶은 영역은 . 을 넣는다.


```
.container{
  display: grid;
  grid-template-columns: repeat(5,1fr);
  grid-template-rows: repeat(3, 1fr);
  grid-template-areas:
  "hd hd hd hd hd"
  "ma ma ma . sb"
  "ft ft ft ft ft"
}
.item{
  border: 3px solid blue;
}
.header{
  grid-area: hd;
}
.main{
  grid-area: ma;
}
.sidebar{
  grid-area: sb;
}
.footer{
  grid-ared: ft;
}
```

## Container - row-gap, column-gap, gap
- 행이나 열 사이의 간격(gutter)를 설정한다.
- 기본 grid-row-gap이었으나 대부분의 브라우저에서는 row-gap도 같이 지원된다.

##  Container - grid-auto-rows, grid-auto-columns
- 템플릿에 명시적으로 작성을 하지 못했지만 넘쳐흐르는 아이템을 암시적으로 설정해준다.

## grid(단축 속성)
- 외재적(명시적)인 속성과 내재적(암시적)인 속성값을 한번에 설정한다.
- 내재적인 속성은 아이템의 위치가 확실치 않다.
앞쪽 속성과 뒤쪽 속성을 / 로 나누어 사용한다.
- 앞쪽 뒤쪽이 둘다 명시거나 row가 명시면 column이 암시,  column이 명시면 row가 암시가 된다.