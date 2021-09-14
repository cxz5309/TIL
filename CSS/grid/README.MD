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

## Container - grid-auto-rows, grid-auto-columns
- 템플릿에 명시적으로 작성을 하지 못했지만 넘쳐흐르는 아이템을 암시적으로 설정해준다.

## Container - grid-auto-flow
- 아이템이 자리잡는 방법의 흐름을 설정한다.
### 값
- row: 아이템의 흘러가는 방향이 행 축이다.
- column: 아이템이 흘러가는 방향이 열 축이다.
- dense: 두칸 혹은 세칸을 차지하는 아이템이 만드는 빈 영역이 없게 만든다.
- `row dense`, `column dense`등 함께 사용 가능하다.

## grid(단축 속성)
- 외재적(명시적)인 속성과 내재적(암시적)인 속성값을 한번에 설정한다.
- 암시적인 속성은 아이템의 위치가 확실치 않다.
- 앞쪽 속성과 뒤쪽 속성을 / 로 나누어 사용한다.
  - 앞쪽의 값은 row, 뒤쪽의 값은 column 영역이다.
- 앞쪽 뒤쪽이 둘다 명시거나 row가 명시면 column이 암시, column이 명시면 row가 암시가 된다.
> 명시적인 값일때의 grid 세부 속성 : grid-template-columns, rows
> 암시적인 값일때의 grid 세부 속성 : grid-auto-columns, rows

## Container - justify-content, align-content

### justify-content
- 기본 축을 기준으로 정렬을 설정한다.
- 바깥 컨테이너의 크기가 안 컨테이너보다 커야 적용 가능하다.

#### 값
- start: 기본 축의 가장 앞으로 정렬
- end: 기본 축의 마지막(보통 오른쪽 끝) 정렬
- center: 
- space-around: 기본축으로 동일한 여백 정렬(시작시 여백 발생)
- space-between: 기본축으로 각각 동일한 간격

### align-content
- column 축을 기준으로 정렬을 설정한다.
- justify-content와 사용법과 값이 동일하다.

## Container - justify-items, align-items

- 배치된 아이템의 영역에서 콘텐츠를 어떻게 정렬할 것인지 설정한다.
- 보통 아이템의 영역보다 콘텐츠가 작을 때에 적용된다.
- justify-items의 기본값이 stretch이므로 기본적으로 영역에 꽉 차 있지만 아이템의 크기가 영역보다 작다면 빈 공간이 생겨 적용된다.


```
.container{
  border 5px dashed;
  display: grid;
  drid-template-rows: repeat(3, 1fr);
  drid-template-columns: repeat(3, 1fr);

  justify-items: stretch;
}
.item{
  border 3px solid blue;
}
.item:nth-child(2){
  justify-self: end;
}
```
> - justify-self로 한 아이템에만 값을 정의할 수도 있다.  

### justify-items
- row 축을 기준으로 각각 아이템들의 정렬을 설정한다.

### align-items
- column 축을 기준으로 각각 아이템들의 정렬을 설정한다.
- justify-items와 사용법과 값이 동일하다.

## Item - grid-row, grid-column (단축 속성)
- grid-row-end와 grid-row-start의 단축 속성
- 아이템의 시작 위치와 종료 위치를 지정한다.
- 값은 각 영역의 시작점과 끝점으로 즉 columns의 개수가 3이면 값은 grid-row의 값은 1~4까지가 된다.
- 마이너스값을 붙일 수 있는데 -1은 양수의 최대값이 되는 형태이다.
  > - 마이너스 넘버링은 명시적으로 작성한 template-rows와 template-columns에만 붙여진다.  
### grid-row-end
- 시작 지점
### grid-row-start
- 종료 지점
### grid-row (단축 속성)
```
.container{
  border: 5px dashed;
  display: grid;
  grid-template-rows: repeat(5,100px);
  grid-template-columns: repeat(3, 1fr);
}
.item{
  border: 3px solid blue;
}
.item:first-child{
  grid-row: 4/ span 2;
  grid-column:2 / -1;
}
```
> - start와 end값을 / 로 나누어서 작성한다.

## grid-area(단축 속성)
- grid-areas의 컨테이너와 함께 각각 아이템의 이름을 지정할때 쓰인다.
- 그 외에도 단축 속성으로 쓰이는데 grid-row-start, grid-row-end, grid-column-start, grid-column-end값을 한번에 설정하는 단축 속성이다.
- 순서가 중요. 
  - row-start, column-start, row-end, column-end 의 순서이다.  
`grid-area: hd;`
`grid-area: 4 / 2 / span 2 / -1;`  


## Item - order
- 기본값은 0이다.(지정되지 않으면 마크업 순서에 맞추어서 흘러간다.)
- 정수(음수 포함) 사용 가능

```
.item:nth-child(3){
  order:-1;
}
```
> - 다른 아이템의 order가 지정되지 않았을 시에 가장 앞으로 간다.
> - 동일 order가 지정되었을 때에도 마크업 순서에 따른다.
## z-index
- display: flex 에서의 z-index 속성과 같지만 요소의 크기가 명시적으로 지정되었을 시에만 겹쳐지게 된다.

## Grid 단위

### fr
> - 다른 단위와 혼합해서 사용할 수 있다. 절대 길이와 함께 사용한 경우 절대 길이가 우선적으로 배정되고 남은 길이를 fr만큼 나누어 가진다.
### min-content
> - 내부 콘텐츠의 최소 길이만큼의 길이를 가진다.
### max-content
> - 내부 콘텐츠의 최대 길이만큼의 길이를 가진다.
### auto-fill
> - 화면이 늘어났을 때 column의 개수가 남는 공간에 자동으로 채워진다.
> - minmax를 조합하여 남는 공간을 꽉 채울 수 있게 해준다.
> - 모바일 등 반응형 페이지를 만드는 데 유용하다.
```
grid-tmplate-columns: repeat(auto-fill, 100px);
```
### auto-fit
- 아이템의 전체 개수 * 길이의 크기보다도 화면의 크기가 클 때 아이템의 길이를 화면을 꽉 채우도록 늘려준다.
> - 역시 모바일 등 반응형 페이지를 만드는 데 유용하다.
