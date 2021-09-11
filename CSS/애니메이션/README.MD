# animation (단축 속성)
- 다수의 스타일을 전환하는 애니메이션을 적용
- **transition과 달리** 유저의 action이 없어도 자동적으로(또는 트리거에 의해서) 전환된다.
- **transition과 달리** 중간값 설정이나 중간 시간 설정도 가능하다.
- a to b가 아니라 다양한 상태값들이 있기 때문에 키프레임이라는 개념을 활용한다.
- 키 프레임은 `animation-name`에 키값 {상태값}으로 저장된다.

## @keyframes
- 애니메이션 중간중간의 특정 지점들을 거칠 수 있는 키프레임들을 설정한다.

- from-to 사용 예제
```
@keyframes slidein{
  from{
    margin-feft:100%
  }
  to{
    margin-left:0%;
  }
}
```  


- % 사용 예제
```
@keyframes 이름{
  n% {상태}  
  n% {상태}
}
```  
> - 동일한 % 적용시 **코드상 뒤쪽의** 스타일이 적용된다.

<br>

- 단축 속성을 사용할 수 있다.
> - 단축 속성을 선호한다.
- 기본값
```
animation-name (en-US): none
animation-duration: 0s
animation-timing-function (en-US): ease
animation-delay: 0s
animation-iteration-count (en-US): 1
animation-direction: normal
animation-fill-mode: none
animation-play-state (en-US): running
```
> animation-play-state는 잘 안쓴다
- transition과 같이 duration이 delay보다 우선된다.
- keyframes와 duration이 없으면 정상적으로 작동하지 않기 때문에 최소 이것을 포함한 둘 이상으로 사용한다.


## animation-name
- 키 프레임의 이름을 설정한다.
`
animation-name : 설정한-키프레임-이름
@keyframes : 설정한-키프레임-이름{}
`

## animation-duration
- transition-duration과 동일
- 그러나 animation은 반복이 가능하기 때문에 고려할 필요가 있고 음수도 작용하지 않는다.
- 1반복을 1사이클이라고 한다.

## animation-delay
- **음수값을 지정할 수 있다.** 
- 음수값 지정시 애니메이션 주기의 음수값만큼 뒤쪽 애니메이션이 잘려서 종료된다.

## animation-timing-function
- transition-timing-function과 동일하게 사용한다.

## animation–iteration–count
- 애니메이션의 재생 횟수
- ### 값으로 infinite를 설정 가능하다

## animation-direction
- 애니메이션의 재생방향을 설정한다(역재생이 가능하다.)
### 값
- normal
- reverse : 역재생
- alternate : 사이클마다 방향 변경

## animation-paly-state
### 값
- running : 기본값, 기본 상태
- paused : 정지상태(애니메이션이 정지된다, 중단이 아닌 정지)

## animation-fill-mode
- 애니메이션이 실행 전과 후에 대상의 스타일을 적용하는 방식을 지정한다.

### 값
- none : 애니메이션이 실행되지 않을 때 스타일을 적용하지 않는다. 즉 애니메이션이 재생될때만 `@keyframes`의 값을 사용한다.
- forwards : 끝난 상태의 `@keyframes`를 적용한다.
- backwards : 첫 상태(`0% or from`)의 `@keyframes`를 적용한다.
- both : 둘 다 적용한다.