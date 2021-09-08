# 박스 모델

![박스 모델](https://media.prod.mdn.mozit.cloud/attachments/2014/09/29/8685/0930aa361239ef7b22a8da798410a855/boxmodel-(3).png)  
박스 모델  

```
.box{
  width: 60% - 30px;
  height: 60% - 30px;
  padding: 10%;
  margin: 10%;
  border: 10px solid blue;
}
```
css 사용 예  

--- 


## width, height

### 사용가능한 값

- 단위가 있는 숫자  
`<length>`  
- 백분율  
`<percentage>`   
- 요소의 너비를 브라우저가 계산(default 값)  
`auto`  
> - 당연히 block요소에서는 가로 길이 전체로 적용된다.
> - inline요소에서는 컨텐츠 크기만큼 적용된다.

#### inline요소에서는 다른 종류의 값도 적용되지 않으며 특별한 조정 없이는 컨텐츠 크기만큼만 적용된다.
- 특별한 조정 : display="block"

## max-width, min-width, max-height, min-height
- %, auto 등으로 크기가 자동 변경되는 경우 최대값과 최소값을 조정할 수 있다.
- 부모 요소에 영향을 받는 경우에도 최대값, 최소값 조정이 가능하다.
> - IE에서 min(), max() 보다 적용이 잘 되기 때문에 지향한다.


--- 


## margin

- 가장 바깥 쪽 레이어, 해당 박스와 다른 요소 사이의 공백

### 사용법
- margin : 0(없음) 이 기본값
- %를 사용하면 **부모의** 값의 백분율을 따라간다.

### margin 순서 <a id="margin_order">#</a>
- 4면 모두 적용
`margin : -3px;` 
- 세로, 가로 순서
`margin: 5% auto;`
- 위, 가로, 아래 순서 (**햄버거**)
`margin: lem auto 2em;`
- 위, 오른쪽, 아래, 왼쪽 (**시계방향**)
`margin: 2px lem 0 auto;
> 순서 나름 중요

[전역 값](../선택자/README.md#inheritance)

--- 


## 마진 상쇄
- 여러 블록 요소들의 위/아래 margin이 경우에 따라 가장 큰 크기를 가진 margin으로 결합(상쇄)되는 현상

1. 인접 형제
  - 두 형제 요소의 위/아래 여백이 만나 상쇄된다.
```
body{
  margin: 0;
}
.box{
  width: 50px;
  height: 50px;
  margin-top: 10px;
  margin-bottom: 20px;
}
```
> 이 경우 2번째 박스와 첫번째 박스 사이의 margin은 20px, 첫번째 박스와 바깥 테두리 사이의 margin은 10px이다.  

2. 부모-자식요소간
  - 부모 블록에 border, padding, inline content가 없어서 부모와 자식의 margin-top이 만나는 경우
  - 부모 블록에 border, padding, inline content가 없고, 부모-자식을 분리할 height값이 지정되지 않아 부모와 자식의 margin-bottom이 만나는 경우
```
#parent{
  width: 100px;
  height: 100px;
  margin-top: 30px;
}
#child{
  width: 30px;
  height:30px;
  margin-top: 40px;
}
```
> 이 경우 부모 요소의 margin-top도 40px로 통일된다.  
> 그러나 부모 요소에 padding 또는 border이 1px라도 주게 되면 둘 사이의 결합이 깨진다.  

3. 빈 블록
  - border, padding, content가 없고, height 또한 존재하지 않으면, 해당 블록의 margin-top과 margin-bottom이 상쇄된다.
> 쉽게 볼 수 없는 경우  
> height가 0인 등의 이유로 자기 자신의 margin-top과 자기 자신의 margin-bottom이 만나게 되면 상쇄된다.  

--- 


## padding
-  콘텐츠와 테두리 사이의 여백

### 사용법
- 순서는 <a href="#margin_order">margin의 순서</a>와 같다
- 그러나 margin과 달리 음수값은 유효하지 않다
- margin과 달리 상쇄가 일어나지 않는다.
- margin과 같이 %를 사용하면 **부모의** 값의 백분율을 따라간다.

--- 

## border
- padding과 margin 사이의 테두리, 외각선(있을 수도 있고 없을 수도 있음, 기본값은 0이므로 기본값은 없는 상태)

### 사용법
- 단축 속성이므로 border-style, border-width, border-color를 한 줄로 사용한다(주로 사용되는 방법)
- 순서는 상관없다.
- border-style은 none 이 기본값(border가 보이지 않는 상태)이므로 보이길 원한다면 필수

### border-style
- 테두리 모양
- none 이 기본값(border가 보이지 않는 상태)
- [스타일 키워드](https://developer.mozilla.org/ko/docs/Web/CSS/border-style)
- 순서는 <a href="#margin_order">margin의 순서</a>와 같다

### border-width
- 테두리 굵기
- 0 이상의 `<length>` 또는 키워드로 사용
- 스타일 키워드 thin, medium, thick
  - 키워드로 사용시 굵기가 브라우저마다 달라지기 때문에 디자인적으로 정확하지 않다(권장하지 않음)

### border-color
- 테두리의 색

--- 

### border-radius
- 요소 테두리 경계의 꼭짓점을 둥글게 만든다. 
- 모서리에 생기는 원의 반지름 크기를 값으로 둔다.
- 순서는 <a href="#margin_order">margin의 순서</a>와 같다

#### 사용가능한 값
`<length>`   
- %를 사용하게 되면 가로와 세로에 각각 계산이 들어가기 때문에 가로와 세로와 다를 수 있다.
`<percentage>`
```
.box{
  width: 300px;
  height: 300px;
  
  border: 5px, solid red;
  border-radius: 150px;
}
```
> 이대로 사용했을 경우 원이 만들어진다.

--- 

## outline
- border와 달리 영역을 차지하고 있지 않아 box model에 속해있지 않다.
- 탭으로 포커싱할 경우(강조할 경우) 외각선을 나타낸다.


--- 
## box-sizing
- 요소의 너비와 높이를 계산하는 방법을 지정한다.


### content-box 값
- 내부의 컨텐츠 사이즈**만** width, height로 잡는다.

### border-box 값
- 전체 길이(content, padding, border) 의 값의 합을 다 합한 값을 width, height로 잡는다.
> 개발자가 인지하기 쉬운 방법  
```
*{
  box-sizing: border-box;
}
```
> 전체 적용을 시켜 사용하는 편이다.  