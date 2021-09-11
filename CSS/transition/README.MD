# transition(단축 속성)
- 요소에 런타임 변화를 주는 속성
- a -> b로 변환이 되는데 이때 **시간** 개념이 들어간다.
- 요소의 각 상태는(변환이 되는 이벤트) 가상 클래스 를 사용해 정의된 :hover 이나 :active 또는 자바스크립트를 사용해 만들어진 상태 속성이다.
  - 요소의 상태에만 transition을 주었을 경우 그 상태에만 변화를 준다 즉 `.box`에 주지 않고 `.box:hover`에 주었을 경우 transition은 마우스가 올라갔을때만 반응하고 없어졌을때에는 반응하지 않는다.
  > - <a href='../선택자/README.md#hover'>hover 문제점 추가</a>

- **대부분 단축 속성을 이용하여 한꺼번에 제작한다**
- 단축 속성 기본값
```
transition-delay: 0s
transition-duration: 0s
transition-property: all
transition-timing-function: ease
```
- duration이 중요하기 때문에 `<time>`속성이 하나 있다면 무조건 transition-duration으로 동작, 두개 있다면 뒤쪽의 시간이 transition-delay으로 적용된다. 그 외의 제한사항은 크게 없다.

## transition-property
- 요소의 변경할 css속성들을 정의한다.

### 값
- none : 변경x
- all : 가지고 있는 모든 css를 변경한다.
- 그 외의 속성(`transition-property: margin-right;`) : 그 속성만 변경한다.
> - 다중 값 입력 가능

## transition-duration
- 어느 정도의 시간 동안 변경할 것인가.
> - 다중 값 입력 가능하지만 transition-property의 각각의 시간을 정의하기 때문에 **transition-property의 속성 숫자와 같아야 한다**
>   - 다르다면 처리되는 방법 : 적다면 리스트의 앞 요소부터 반복, 많다면 무시
- `<time>` 값이 들어간다.


## `<time>`
- s : 세컨드
- ms : 밀리세컨드 
> 소수점, 마이너스 가능


## transition-delay
- transition시작시간 지연
- `<time>`만큼 transition의 시작이 지연된다.

## transition-timing-function
> - 유니티에서 ease사용하던것과 같다.
> - 그러나 바리에이션이 유니티만큼 많지는 않고 직접 설정해야 하는듯
변화율 그래프 : https://developer.mozilla.org/en-US/docs/Web/CSS/easing-function

### 값
- 대략적으로 나누어서 표현하면
1. linear : 직선
2. ease : 1변속
3. cubi-bezier : 2변속
4. step : 일정 변속이 계단식으로 급변한다.



## transition + transform 활용

```
.box{
  width: 100px;
  height: 100px;
  border: 10px solid seagreen;
  background-color: rgb(204, 253, 225);
  border-radius: 30px;

  transform-origin: bottom right;
  transition: all 1s ease-in-out;
}

.box:hover{
  transform: rotate(360deg);
}
```  
최종적으로 오른쪽으로 1초에 걸려서 오른쪽 모서리를 중심으로 360도 크게 돌아가게 된다.  