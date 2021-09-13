# flexbox
> 이해하기 힘들고 규칙도 외우기 힘든 float나 다른 레이아웃 요소들을 안 써도 되게 하는 갓 시스템  
> 그래서 개발자들이 매우 많이 사용하고 중요하다  
> css3부터 추가되었다.  
>> 매우 도움되는 사이트 : https://flexboxfroggy.com/#ko  
>> 사실 사용할 때마다 여기 보고 했는데 이번 기회에 제대로 외워두어야겠다.  

```
.container{
  border: 5px dashed;
  display: flex;
}

.item{
  width: 50px;
  height: 50px;
  background-color: black;
  border: 3px solid blue;
}
```
>이것만 해도 엄청 유용한 기능임에 틀림없다.  

## flex container, flex item, main axis, cross axis
- flex container, flex item이 부모 자식 형태가 되어야만 flex가 제대로 동작한다.
- container에서만 사용하는 속성, item에서만 사용하는 속성이 따로 있기 때문에 알맞게 넣어주어야 잘 동작한다.
- 일반 flexbox는 1차원 공간이기 때문에 main axis는 가로축 기본값이고 cross axis가 세로축 역할을 해준다.

## Container - display: flex (내부 display 요소) <a id="in_display_flex">#</a>
- <a href="../레이아웃/README.MD#out_display">#외부 display 요소</a>
- `block`, `inline`, `inline-block`는 `<display-outside>`의 display값 요소이고 `<display-inside>` 의 값 요소는 flex와 관련이 있다.  
- `-(대쉬)`를 사용하여 바깥쪽 요소와의 관계와 안쪽의 관계를 동시에 정의할 수 있다.

## Container - flex–direction
- flex-direction은 flex컨테이너 내의 아이템의 주축 및 배치 방향을 지정한다.(main=가로, cross=세로)
- 변경 가능한 값
1. 주축의 위치(세로, 가로)
2. 주축의 방향(정, 역)

### 값
- row : 기본값, 주축이 가로로 되어 있으며, 왼쪽부터 오른쪽의 정 방향으로 진행한다.
- row-reverse : 가로, 오른쪽에서 왼쪽방향
- column : 주축이 세로, 위에서 아래방향
- column-reversse : 주축이 세로, 아래에서 위 방향

```
#pond {
  display: flex;
flex-direction: row-reverse
}
```
출처 : https://flexboxfroggy.com/#ko 8단계   
```
#pond {
  display: flex;
flex-direction: column
}
```
출처 : https://flexboxfroggy.com/#ko 9단계    

## Container - flex–wrap
- 요소들이 강제로 한줄에 배치되게 할 것인지, 또는 가능한 영역 내에서 벗어나지 않고 여러행으로 나누어 표현 할 것인지 결정하는 속성

### 값
- nowrap : 기본값, 한줄 배치
- wrap : 여러 행으로 나눈다, 일반적인 순서(왼->오, 위->아래)로 쌓인다
- wrap-reverse : wrap처럼 행이 나뉘지만 라인 순서가 반대이다(왼->오, 아래에서 위로 쌓인다.)
```
#pond {
  display: flex;
flex-wrap: wrap
}
```  
출처 : https://flexboxfroggy.com/#ko 18단계    

## Container - flex-flow(단축 속성)
- flex-direction과 flex-wrap의 단축 속성이다.
- flex-direction과 flex-wrap이 자주 같이 사용되기 때문에 만들어졌다.
- flex-direction과 flex-wrap의 값 단위가 다르므로 아무렇게나 써도 상관 없다.

```
#pond {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
}
```
출처 : https://flexboxfroggy.com/#ko 19단계    


```
#pond {
  display: flex;
  flex-flow: column wrap
}
```  
출처 : https://flexboxfroggy.com/#ko 20단계    

## item - order
- flex 컨테이너 내부에서 현재 요소의 순서를 지정한다.
- 순서는 오름차순, 같은 값이 있다면 소스코드의 순서를 따른다.
- 기본값은 0이므로 하나만 적용시 -1이면 맨 앞, 1이면 맨 뒤가 된다.
> - order속성은 논리적인 순서나 탭 순서와는 상관 없이 화면에 보이는 순서에만 영향을 준다. 따라서 비시각적 매체에 적용하면 안된다.

```
#pond {
  display: flex;
}

.yellow {
  order: 1
}
```
출처 : https://flexboxfroggy.com/#ko 14단계  

## item - flex-grow
- flex-item요소가 컨테이너 요소 내부에서 할당 가능한 공간의 정도(적용시 남은 공간만큼 늘어난다.)
- 음수는 사용할 수 없다.
- 숫자만큼 남은 공간을 나누어 가진다.

## item - flex-shrink
- **item의 요소가 container요소의 크기보다 클 때** 사용한다
- grow와 반대로 줄어든다.
### 값
- 기본값 1 :  즉 flex에는 기본으로 1배율로 줄어드는 기능을 가지고 있다.
- 0 : 적용하지 않아 줄어들지 않는다.
- 숫자 적용시 총 줄어든 공간을 숫자만큼 할당한다.

## flex-basis
- flex item의 초기 크기를 지정한다.
- grow, shrink 등이 초기 크기 + 늘어나는 비율이기 때문에 초기 크기가 다르더라도 초기 크기를 지정해서 크기를 동일하게 맞추는데 유용하다.

```
.container{
  height: 200px;
  display: flex;
}

.item{
  height: 50px;
  margin: 5px;
  font-size: 30px;
  flex-grow: 1;
  flex-basis: 0;
}
```

## flex (단축 속성)
- 초기값
```
flex-grow: 0;
flex-shrink: 1;
flex-basis: auto;
```
> - **주의할 점**: flex-grow, flex-shrink만 사용시 flex-basis는 auto가 되지 않고 0이 된다.  
>   - 사실 flex-basis가 0인 편이 오히려 사용하기 쉽다.

- 값이 한 개일 때 `<number>`이면 flex-grow이다.
- 값이 한 개일 때 `<length>`또는 `<percentage>`이면 flex-basis이다.
- 순서가 중요하다. 값이 두 개일 때 첫번째 값은 무조건 `<number>` 여야 하고 flex-grow가 된다. 두번째 값은 사용 값에 따라 flex-shrink, flex-basis로 나뉜다.
- 마찬가지로 값이 3개일 때도 순서가 중요하다. flex-grow flex-shrink flex-basis 순으로 된다.
### 값 
- initial : flex 0 1 auto와 같다
- auto : flex 1 1 auto와 같다.
- none : flex 0 0 auto와 같다.

> ###### 이렇게 하면 꽉 채워지나보다..^^

## Container - justify-content
- 주축을 기준으로 아이템을 어떻게 정렬할 것인가를 결정
### 값
- flex-start: 주축이 시작되는 위치부터(기본값)
- flex-end: 주축이 끝나는 위치부터
> flex-direction은 주축의 방향을 바꿔버리기 때문에 flex-direction이 reverse이면 앞부터 정렬한다   
> 따라서 왼쪽정렬, 오른쪽 정렬이 아닌 주축의 시작, 끝 정렬로 이해하는 것이 편하다.  
- flex-center: 중앙정렬
- space-between: 요소 사이 동일 간격 정렬
- space-around: 요소 앞뒤로 동일한 여백 정렬(시작시 여백 발생)
- space-evenly: 요소만큼의 여백 설정



```
#pond {
  display: flex;
justify-content:flex-end;
}
```
```
#pond {
  display: flex;
justify-content: center;
}
```
```
#pond {
  display: flex;
justify-content: space-around;
}
```
출처 : https://flexboxfroggy.com/#ko 1~4  

## Container - align-items
- 컨테이너 내부의 main축의 모든 요소들을 각 라인별로 한 요소로 잡은 요소를 정렬 가능한 속성(세로축 정렬이 아님)

### 값
- stretch: 기본값, 세로축 전체로 늘인다.
- flex-start: 시작 위치부터 정렬
- flex-end: 마지막 위치부터 정렬
- center: 중앙 정렬
> - space-between같은 요소는 각각의 요소를 정렬하는 것이 아니라 모든 요소를 하나로 생각하고 정렬하기 때문에 존재하지 않는다.

```
#pond {
  display: flex;
align-items: flex-end;
}
```
```
#pond {
  display: flex;
justify-content: center;
align-items: center;
}
```

```
#pond {
  display: flex;
justify-content: space-around;
align-items: end;
}
```
```
#pond {
  display: flex;
flex-direction: row-reverse;
justify-content: flex-end;
}
```
```
#pond {
  display: flex;
flex-direction: column;
justify-content: flex-end;
}
```
```
#pond {
  display: flex;
flex-direction: column-reverse;
justify-content: space-between;
}
```
```
#pond {
  display: flex;
flex-direction: row-reverse;
justify-content: center;
align-items: flex-end;
}
```

출처 : https://flexboxfroggy.com/#ko  
## Container - align-content
- 컨테이너 내부의 cross축의 요소를 정렬 가능한 속성

### 값
- flex-start: cross축이 시작되는 위치부터(기본값)
- flex-end: cross축이 끝나는 위치부터
- flex-center: 중앙정렬
- space-between: 요소 사이 동일 간격 정렬
- space-around: 요소 앞뒤로 동일한 여백 정렬(시작시 여백 발생)

```
#pond {
  display: flex;
  flex-wrap: wrap;
align-content: flex-start;
}
```
```
#pond {
  display: flex;
  flex-wrap: wrap;
align-content: flex-end;
}
```
```
#pond {
  display: flex;
  flex-wrap: wrap;
flex-direction: column-reverse;
align-content: center;
}
```

출처 : https://flexboxfroggy.com/#ko 21~23단계  

## Item - align-self
- 아이템 단 하나만 정렬하는 속성
### 값
- auto: align-items의 값을 따라간다.
- normal: 레이아웃의 상태에 따라 start 또는 stretch로 작동한다.
- self-start: 가장 왼쪽 상단 모서리를 시작지점으로 정렬한다.
- flex-start: 주축의 시작지점을 기준으로 정렬한다.
- stretch: 남은 공간만큼 늘린다.

```
#pond {
  display: flex;
  align-items: flex-start;
}

.yellow {
align-self: flex-end;
}
```
```
#pond {
  display: flex;
  align-items: flex-start;
}

.yellow {
order: 1;
align-self: flex-end;
}
```
출처 : https://flexboxfroggy.com/#ko 16, 17단계  


```
#pond {
  display: flex;
flex-direction: column-reverse;
justify-content: center;
flex-flow: column-reverse wrap-reverse;
align-content: space-between;
}
```
출처 : https://flexboxfroggy.com/#ko 24단계