# 04 변수

## 4.1 변수란 무엇인가? 왜 필요한가?

- 자바스크립트엔진의 계산방식
  
10 + 20을 계산하기 위해 + 연산자의 좌변과 우변의 숫자값, 즉 피연산자를 기억한다. 이때 기억은 메모리를 사용, 연산은 cpu를 사용한다.  
메모리는 메모리 셀의 집합체로 셀 하나의 크기는 1 바이트(8비트)이며 컴퓨터는 메모리 단위로 데이터를 저장하거나(write) 읽는다(read)  
셀은 고유의 메모리 주소를 가지며 0부터 메모리 크기만큼 정수로 표현된다.  
10과 20은 메모리상 임의의 위치에 기억되고 cpu는 이 값을 읽어 연산을 수행한다. 연산 결과로 생성된 30도 메모리상 임의의 위치에 저장된다. 
30에 접근하기 위한 방법으로 메모리 주소를 통하는 방법은(c언어 포인트 등) 치명적 오류를 발생시킬 가능성이 높은 매우 위험한 일이므로 자바스크립트는 직접적인 메모리 제어를 허용하지 않는다.  
또한 동일한 코드를 실행해도 코드 실행마다 값이 저장될 메모리 주소는 변경된다.  
이 때문에 js는 기억하고 싶은 값을 메모리에 저장하고, 저장된 값을 읽어 재사용하기 위해 변수를 제공한다. 
### 변수
- 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름  
  
즉 변수는 메모리가 아닌 값의 위치를 가리키는 상징적인 이름이다. 변수는 컴파일러 또는 인터프리터에 의해 값이 저장된 메모리 공간의 주소로 치환되어 실행된다.  
따라서 개발자는 직접 메모리 주소를 통해 값을 저장하고 참조할 필요 없이 변수를 통해 안전하게 값에 접근이 가능하다.  
### 변수의 고유한 이름
- 변수 이름
### 변수에 저장된 값
- 변수 값
### 변수에 값을 저장하는것 
- 할당
### 변수에 저장된 값을 읽어 들이는 것
- 참조

## 4.2 식별자

- 어떤 값을 구별해서 식별할 수 있는 고유한 이름  
  
식별자는 어떤 값이 저장되어 있는 메모리 주소를 기억해야 한다.  
즉 식별자는 값이 저장되어 있는 메모리 주소와 매핑관계를 맺으며, 이 매핑 정보도 메모리에 저장되어야 한다.  
따라서 식별자는 값이 아니라 메모리 주소를 기억하고 있다. 
식별자라는 용어는 변수 이름에만 국한해서 사용하지 않으며 변수, 함수, 클래스 등의 이름은 모두 식별자이다.  
식별자는 네이밍 규칙을 준수해야 하며 **선언**에 의해 식별자의 존재를 알린다.

## 4.3 변수 선언

- 변수를 생성하는 것. 즉 값을 저장하기 위한 메모리 공간을 확보하고 변수 이름과 확보된 메모리 공간의 주소를 연결하여 값을 저장할 수 있도록 준비한다.  

변수를 사용하기 위해서는 반드시 선언이 필요하다.  
ES6에서 let, const 키워드가 도입되었다.  
-> var키워드의 단점으로 인해 거의 대체되었다.  
> ## 15.1 var 키워드로 선언한 변수의 문제점
> 1. 변수 중복 선언 허용
> 2. 함수 레벨 스코프
> 3. 변수 호이스팅

변수 선언으로 인해 메모리 공간이 확보되면 자바스크립트 엔진에 의해 undefined라는 값이 암묵적으로 할당되어 초기화된다. 이건은 자바스크립트의 독특한 특징이다.  
### 선언단계
변수 이름을 등록해서 자바스크립트 엔진에 변수의 존재를 알린다.
### 초기화 단계 
값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 undefined를 할당해 초기화한다.  
  
만약 초기화 단게를 거치지 않으면 확보된 메모리 공간에는 이전에 사용했던 값이 남아 있을 수 있다. 이러한 값을 **쓰레기값**이라고 한다. js는 let, var등 키워드에서 암묵적으로 초기화를 수행하므로 이러한 위험이 발생되지는 않는다.  
만약 선언되지 않은 식별자에 접근하면 ReferenceError(참조 에러)가 발생한다.

## 4.4 변수 선언의 실행 시점과 변수 호이스팅

- 런타임
소스코드가 한 줄씩 순차적으로 실행되는 시점  
변수 선언은 런타임이 아니라 그 이전 단계에서 먼저 실행되기 때문에 다음과 같은 상황에서 에러가 발생되지 않는다  
```
console.log(scroe);
var score;
```
이는 변수 선언이 소스코드가 순차적으로 실행되는 런타임 이전 단계에서 먼저 실행된다는 증거이다. 이처럼 변수 선언이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 **변수 호이스팅**이라고 한다.  
> ## 15.2.3 let 키워드
> 변수 호이스팅은 var로 선언된 변수에서만 발생하고 ES6에서 사용하는 let, const 는 변수 호이스팅의 문제점으로 인해 변수 호이스팅이 발생하지 않는 것처럼 동작한다!

## 4.5 값의 할당

변수 선언은 호이스팅으로 런타임 이전에 먼저 실행되지만 값의 할당은 소스코드가 순차적으로 실행되는 시점이 런타임에 실행된다.
선언과 동시에 할당하더라도 js엔진은 선언과 할당을 2개의 문으로 나누어 각각 실행한다. 
```
var score = 80;
```

## 4.6 값의 재할당

- 이미 값이 할당되어 있는 변수에 새로운 값을 또다시 할당하는 것을 말한다.
  
var 키워드로 선언한 변수는 선언과 동시에 undefined로 초기화되기 때문에 엄밀히 말하자면 처음으로 값을 할당하는 것도 사실은 재할당이다.  
만약 값을 재할당할 수 없어 변수에 저장된 값을 변경할 수 없다면 변수가 아니라 **상수**라고 한다. 즉 상수는 단 한번만 할당할 수 있는 변수다.  
-> const 키워드  
변수에 값을 할당할 때는 이전 값 undefined가 저장되어 있던 메모리공간을 지우고 그곳에 할당 값을 새롭게 저장하는 것이 아니라 새로운 메모리 공간을 확보하고 그곳에 할당 값 80을 저장한다.  
이때 생기는 쓰레기값(가비지)들은 **가비지콜렉터**에 의해 메모리에서 자동 해제된다. 
가비지콜렉터의 해제 시기는 예측할 수 없다.  
가비지 콜렉터를 통해 메모리 누수(memory leak)를 방지한다.  
가비지 콜렉터를 내장하고 있는 언어를 보통 **매니지드 언어**라고 한다.  
js는 직접적인 메모리 제어를 전혀 허용하지 않으므로 생산성을 확보할 수 있지만 성능 면에서 어느정도 손실을 감수하여야 한다.  

## 4.7 식별자 네이밍 규칙

- 식별자는 특수문자를 제외한 문자, 언더스코어, 달러 기호를 포함할 수 있다.
- 단 식별자는 특수문자를 제외한 문자, 언더스코어, 달러 기호로 시작가능하나 숫자로 시작하는것은 허용하지 않는다.
- 예약어는 식별자로 사용할 수 없다.(사용은 가능하나 지양, strict mode에서는 불가)

변수 이름도 식별자이므로 네이밍 규칙을 따른다. 

### 네이밍 컨벤션
- 카멜 케이스 firstName
- 스네이크 케이스 first_name
- 파스칼 케이스 FirstName
- 헝가리언 케이스 strFirstName

자바스크립트에서는 일반적으로 변수나 함수에서 카멜케이스, 생성자 함수, 클래스의 이름 등에는 파스칼 케이스를 사용한다.  