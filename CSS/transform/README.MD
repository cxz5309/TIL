# transform
- 요소에 회전, 크기, 기울이기, 이동 효과 등을 부여
- 원본 파일 자체의 위치 중심점은 유지된다.
- 값으로 함수표기법을 사용한다.
  - [<transform-function>](https://developer.mozilla.org/ko/docs/Web/CSS/transform-function) 으로 명칭을 통일한다.
- 단축 속성으로써 여러 값이 들어갈 수 있다.  
> - **그러나 오른쪽부터 왼쪽 순서로 적용된다. 순서는 결과에 영향을 준다**  
> 변형 가능한 요소만 transform할 수 있다. 즉, CSS 박스 모델이 레이아웃을 결정하는 모든 요소 중 비대체 인라인 박스, 표를 제외한 요소에만 적용할 수 있다.  
## scale()
- 크기
### 매개변수 값
`scale(sx), scale(sx, sy)`    
`scaleX(sx), scaleY(sy)`  
- width를 변경하는 것과 다른 개념이다!
  - 컨테이너의 공간과 현재 중심점은 유지되고 크기만 바뀌기 때문
- **2개 사용시 비율이 찌그러진다**
- 3d시 scale3d()사용  

## rotate()
- 회전
### 사용할 수 있는 단위
> - 음수도 사용 가능하다.  
- deg : 흔히 통용되는 각도 `90deg = 90도`
- turn : `1turn = 1회 회전`, `0.5turn = 반바퀴 회전`


## translate()
- 이동
### 매개변수 값
> - 음수도 사용 가능하다.  
- 한가지 값 입력시 x축으로만 이동, 두가지 값 입력시 x, y값 이동
`translate(100px, 50%)`


## skew()
- 기울이기
### 매개변수 값
> - 음수도 사용 가능하다.  
- 한가지 값 입력시 x축만 기울이기, 두가지 값 입력시 x, y값 기울이기
- 사용 가능한 단위는 rotate()의 단위와 같다. 
`skew(90deg)`는 선이 될 정도로 기울어졌기 때문에 보이지 않는다

## transform-origin
- transform과 완전히 별도의 속성이다
- 기본값 `transform-origin:center;`
- 요소의 중심점을 설정한다.
- 
### 값
- `transform-origin:50px 100px;` : 좌상단 꼭지점을 기준으로 x, y축 이동한 값
- `transform-origin: top left;` : 기본값은 center이다. 좌상단 꼭지점으로 기준점을 옮긴다.
> animation, transition 에서 유용하게 사용하는 경우가 있다.