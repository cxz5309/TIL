# 레이아웃

## display (외부 디스플레이 요소, 박스 요소) <a id="out_display">#</a>
- <a href="../flexbox/README.MD#in_display_flex">#내부 display 요소-flex</a>  
- <a href="../grid/README.MD#in_display_grid">#내부 display 요소-grid</a>  
- 외부 디스플레이 요소(inline, block)와 내부 디스플레이 요소, 박스 요소 등을 설정한다.
> - 내부 디스플레이 요소는 이후 등장할 flex에서 사용한다.

### inline, block(외부 디스플레이 요소)
### inline
- 영역의 크기가 내부 콘텐츠 크기로 정해진다.
  - width, height를 해도 안먹힌다.
- margin, padding의 top/bottom
- 여러 요소가 가로 배치가 된다.  
ex) `span`

### block
- 영역의 크기를 width, height로 지정할 수 있다.
- width를 지정하지 않으면 가로 전체를 차지한다.
- 여러 요소가 세로 배치가 된다.  
ex) `div`

### inline-block
- inline과 block요소의 특징을 같이 가지고 있다.
- 영역의 크기를 width, height로 지정할 수 있다.
- 여러 요소가 가로 배치가 된다.  
ex) `input`

### 요소를 없애는 방법(박스 요소)

### <a id="none">none</a>
- 박스 요소를 없앤다
- <a href="hidden">visibility: hidden</a>과 달리 레이아웃에서도 제외된다.

---

## visibility
### visible
- 보임
### <a id="hidden">hidden</a>
- <a href="none">display: none</a>과 달리 레이아웃에는 존재하지만 보이지는 않는다.  
### collapse
- table 요소에서 사용하면 적용한 요소만 숨기고 공간까지 제거한다.

---


## float
- 요소가 보통 흐름(normal flow)에서 빠져 텍스트 및 인라인 요소가 그 주위를 감싸는 자기 컨테이너의 좌우측을 따라 배치한다.
> - 현재는 flexbox로 인해 사용 빈도가 줄었다.  
> - 레거시 코드에서 많이 사용했으므로 알아둘 필요는 있다.  
![floats Example](https://media.prod.mdn.mozit.cloud/attachments/2012/07/09/3220/f1f6c7ad89656e9e1545bbab898239b9/floats.png)    
float를 적용한 예시   

### none
- 없음
### left
- 요소를 왼쪽에 배치한다.(인라인 요소는 오른쪽으로 배치된다.)
### right
- 요소를 오른쪽에 배치한다.(인라인 요소는 오른쪽으로 배치된다.)

---


## position
- top, left, right, bottom의 속성을 따로 주어서 요소의 위치를 결정한다.
- 위치를 결정할 때 기준점을 잡아준다.


### nomal flow(일반 대열)
- 요소에 레이아웃을 변경하지 않았을 경우의 배치되는 방법
- 블록요소는 너비100%, 인라인 요소는 자기 자신의 크기

### static
- default 값
- 일반적인 문서 흐름(nomal flow)
- top, right, bottom, 등이 영향을 주지 않는다.
### relative
- 자기 자신을 기준으로 오프셋이 적용된다.
### absolute
- 부모를 기준으로 오프셋이 적용된다. 
- **부모 중 static이 아닌 것**만을 기준
### fixed
- 뷰포트를 기준으로 삼는다. 
- 일반적인 문서 흐름에서 제거하고, 공간도 배정하지 않는다.
### sticky
- 특정 위치에서 지나갔을 때 스크롤을 따라간다.
- 스크롤하는 대상의 바로 자식이어야만 한다.(아니면 동작x)

---


## overflow
- 컨테이너가 지정된 상태에서 내부 콘텐츠 영역이 많아 컨테이너 밖으로 넘쳐 흐를 경우의 처리
### visible
- 넘쳐흐르게 놔둠
### hidden
- 블록 밖으로 나갈 수 없다.
### scroll
- 스크롤바가 생겨난다.
### auto
- visible / scroll 에서 상황에 따라 자동으로 선택된다.
> - 일반적으로 나쁘지 않은 선택인듯  

---


## z-index
- 요소가 다른 요소보다 앞에 보이는 것을 조절한다.
- 정수값 사용 가능
- 3차원 z축을 생각하면 된다.
- 숫자가 클 수록 사용자에 가깝게 보인다.
- 없으면 static이 아닌 애들이 static보다 앞에 쌓인다.
- 둘다 static이 아니면 코드 순서대로(뒤에있는 코드가) 앞에 쌓인다.
![z-index적용](https://media.prod.mdn.mozit.cloud/attachments/2012/07/09/789/3f63768682968cb88d0e5270731bdfbb/understanding_zindex_03.png)   
z-index의 적용 예

