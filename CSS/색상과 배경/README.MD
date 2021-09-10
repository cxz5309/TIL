# 색상과 배경

## &#60;color>  

### 값으로 들어갈 수 있는 내용
- 색상 키워드 사용   
`blue, transparent(투명)`  
- HEX(# + 16진수)  
`#ffffff(흰색)`
- rgb(), rgba()
  - 0~255 R:red, G:green, B:blue, A:alpha
  - 알파값은 투명을 뜻한다.
- hsl(), hsla()
  - %로 나타내어진다.

## opacity
- 요소의 불투명도를 설정한다.
- 기본값 1
- 0~1의 실수값이 들어간다.
- &#60;percentage>0~100% 로도 표현 가능
- **background와 달리 자식에 상속된다.**

## background-color(r,g,b,a)
- 배경색
- &#60;color>의 값이 들어간다.

## background-image
- 기본값 none (이미지 없음)
- &#60;image>
  - `url("https://upload.wikimedia.org/wikipedia/commons/0/0b/RGBA_comp.png")`
- background-color와 함께 사용할 수 있고 함께 사용하게 되면 이미지가 사용자에게 더 가깝게 보인다.



## background-repeat
- 배경 이미지를 반복시킨다.
- 컨테이너가 커지는 만큼 반복도 늘어난다
### 값
- repeat : 반복
- no-repeat : 반복 X
- repeat-x : x축만 repeat
- repeat-y : y축만 repeat

## background-position
- 배경의 좌표값
- **왼쪽 상단 꼭지점이 피벗이다**

### 값
- top, bottom, right, center 등의 키워드(중복 사용 가능, 순서 상관 없음)
- 픽셀

## background-origin
- 배경이 위치하는 박스 모델상의 기준점
- `content-box`, `padding-box`, `border-box`등 박스 모델 키워드

## background-clip
- 배경이 박스 모델상 어디까지 차지할 지 지정한다.
- **background-origin과의 차이점 : 무조건 중앙을 기준으로 하고 경계 바깥으로 나가면 잘라낸다. background-origin은 좌상단의 기준점이 바뀌므로 보통 우하단이 잘린다.**  

## background-size
- 배경크기
  
### 값
- auto : 이미지의 원래 크기, 기본값
- contain : 이미지가 잘리거나 찌그러지지 않는 한도 내에서 제일 크게 설정, **이미지의 비율이 유지됨**
- cover : contain과 같으나 이미지의 가로세로비가 요소와 다르다면 잘라내는 방식, **이미지의 비율이 유지됨**
- &#60;length> px : 
  - 한개만 입력했을 시 **이미지의 비율이 유지됨**
  - 가로, 세로를 모두 입력시 **이미지가 찌그러진다**
- &#60;percentage> % : **이미지가 찌그러진다**

## background (shorthand)
`background : green url("test.jpg") repeat-y border-box`
> 여러개의 배경을 한꺼번에 적용할 수 있다. 그 규칙은 단축속성 외(background-image 등)에서도 동일하다.
```
.myclass {
  background: background1, background 2, ..., backgroundN;
}
```

### 규칙
- **bg-size 값은 bg-position 바로 뒤에만 위치할 수 있으며 '/'문자로 구분해야 한다.**
- **box 값은 2개 까지 설정 가능하며 각각 background-origin, background-clip이다. (한개면 background-origin이 기본이다.)**
- **background-color는 마지막에만 쓸 수 있다.**
