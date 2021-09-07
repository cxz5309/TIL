# 폰트 관련 속성

## 폰트 크기
- 글자 크기
```
.text{
  font-size: 16px;
}
```
### font-size 값에 들어갈 수 있는 항목
- 사용자의 기본 폰트 크기에 따라 결정  
`xx-small, x-small, small, medium, large, x-large, xx-large`  
- 부모 요소의 폰트 크기에 따라 결정(정해진 비율)  
`larger, smaller`
- 부모 요소의 폰트 크기에 따라 결정(비율 설정)  
`%`
- 단위값([단위와 값](../단위와%20값/README.MD)에서 추가 설명)
`px, em`
- 전역 값([선택자](../선택자/README.md)에서 추가 설명)  
`inherit, initial, unset`

## 폰트 스타일
- 거의 이탤릭체를 위해 사용
```
.text{
  font-size: 16px;
  font-style: italic;
}
```
`oblique` : 이탤릭체와 비슷하나 브라우저 스타일에 따라 이탤릭체가 더 필기체같은 경우가 많다.


## 폰트 굵기
- 거의 볼트체를 위해 사용
```
.text{
  font-weight: bold;
}
```
- 단위로 볼드를 더 다양하게 지원한다.
- lighter, bolder로 더 얇고 굵은 체를 지원한다.


## 글꼴

- 여러 개의 폰트 중 먼저 있는 폰트를 적용하고, 만약 사용자의 컴퓨터에 다운되지 않았거나, 지원되지 않는 언어일 경우 차례대로 뒤에 있는 폰트를 사용한다.
- 보통 많은 사람들이 사용하지 않는 경우는 쓰지 않는 편이 좋고 웹폰트를 사이트에서 다운받을 수 있게 하여 폰트를 적용한다.
```
.text{
font-family: Times, Georgia
}
```

## 줄간격

```
.text{
  line-height: 
}
```

### line-height 값에 들어갈 수 있는 항목
- 기본
`nomal`
- 폰트사이즈의 배수  
<숫자>
- 폰트사이즈의 따라 결정(비율 설정)  
`%`
- 단위값([단위와 값](../단위와%20값/README.MD)에서 추가 설명)
`px, em`
- 전역 값([선택자](../선택자/README.md)에서 추가 설명)  
`inherit, initial, unset`

## font(CSS단축 속성)
-여러 가지 속성을 한줄로 묶어서 표현
- 필수 요소  
`font-size, font-family`   
- 옵션 요소  
`font-style, font-variant, font-weight, line-height`   
```
.text{
  font: 20px, 'Times New Roman', Times, serif;
}
```
- **작성하지 않으면 '기본값을 적용한다'라는 의미가 되므로 추가로 작성시 font보다 아래쪽에 넣어야 한다.**  
- 순서  
`font-style font-weight font-size/ line-height 무조건 맨 뒤에 font-family`

## 여백 크기
```
.text{
  letter-spacing: normal;
  word-spacing: normal;
}
```
### 값에 들어갈 수 있는 항목
- 기본  
`normal`  
- 단위값  
`&#60;	length>`  
- 전역 값  
`inherit, initial, unset`  
> - word-spacing에서만 퍼센트를 사용 가능하다  
> %  


## 정렬
```
.text{
  text-align: center;
}
```
- 인라인 요소에서는 텍스트가 부모 요소에 꽉 차게 적용되기 때문에 적용이 되지 않는다.
- 
### 값에 들어갈 수 있는 항목
`start, end, center, right, left, justify, justify-all, match-parent`
> justify : 왼쪽과 오른쪽 열에 맞추어 화면을 늘어뜨림

## 들여쓰기
```
.text{
  text-indent: 20px;
}
```
- inherited(상속된다)
- block contents(블럭 요소에만 적용된다)

### text-indent 값에 들어갈 수 있는 항목
- 단위값  
&#60;length>  
- 컨텐츠 요소 가로 길이에 따라 결정(비율 설정)  
%  
- 전역 값  
`inherit, initial, unset`  
- 옵션 값  
`each-line` : 들여쓰기는 블록 컨테이너의 첫 번째 줄과 강제 줄 바꿈 후의 각 줄에 영향을 준다  
`hanging` : 들여쓴 줄을 반전시킨다. 첫 번째 줄을 제외한 모든 줄이 들여쓰기된다.  


## text-decoration(CSS단축 속성)
- font속성과 달리 거의 대부분 단축 속성으로써 사용한다.
- 텍스트에 선을 그어 텍스트를 꾸며 준다.

```
span{
  text-decoration: line-through, underline
}
```
### 필수 속성
### text-decoration-line 
- 텍스트에 선을 긋는 필수 속성
#### 값에 들어갈 수 있는 항목
`none` : 없음
`underline` : 밑줄
`overline` : 상단선
`line-through` : 취소선
- 여러 개 동시에 사용 가능하다

### 옵션 속성
### text-decoration-style
- 선의 스타일
#### 값에 들어갈 수 있는 항목
`solid` : 한 줄  
`double` : 두 줄  
`dotted` : 점선  
`dashed` : 긴 점선  
`wavy` : 물결표  

### text-decoration-color
- 선의 색상
[&#60;color>](../색상과%20배경/README.MD)

### text-decoration-thickness
- 선의 굵기
#### 값에 들어갈 수 있는 항목
`auto` : 기본  
`from-font` : 글꼴 파일에 기본 두께에 대한 정보가 포함되어 있으면 해당 값을 사용한다.  
`&#60;length>` : 단위값  
`%` : 1em의 백분율로 비율 설정    

## word-break
- 텍스트가 자신의 콘텐츠 박스 밖으로 오버플로 할 때 줄을 바꿀지 지정한다.  
`normal` : 기본값  
`break-all` : 보통 영어에만 사용, 줄을 바꿀때 단어를 끊는다.  
`keep-all` : 보통 한중일 텍스트에 사용(lang='en'의 default값) , 줄을 바꿀때 단어를 끊지 않는다.  


## text–transform
대문자, 소문자
```
.container p:last-of-type{
  text-transform: uppercase;
}
```

`uppercase` : 대문자
`lowercase` : 소문자
`capitailize` : 맨 앞의 문자만 대문자로 변경
