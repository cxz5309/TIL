# 19 프로토타입
- 자바스크립트는 명령형, 함수형, 프로토타입 기반, 객체지향 프로그래밍을 지원하는 **멀티 패러다임 프로그래밍 언어**이다.
- 자바스크립트는 객체지향 언어가 아니라고 오해를 받는 경우가 있으나 **자바스크립트는 클래스 기반 객체지향 프로그래밍 언어보다 효율적이며 더 강력한 객체지향 프로그래밍 능력을 지니고 있는 프로토타입 기반 객체지향 프로그래밍 언어이다.**
- 자바스크립트를 이루고 있는 **거의 모든것이 객체이다!** 원시 타입의 값을 제외한 나머지 값들은 모두 객체이다.


## 19.1 객체지향 프로그래밍
- 명령형 프로그래밍의 절차지향적 관점에서 벗어나 객체의 집합으로 프로그램을 표현한다!
### 추상화 
- 공통의 속성이나 기능을 묶어 이름을 붙이는 것
- 자바스크립트의 모든 객체는 속성을 가지고 있고 다양한 속성 중에서 프로그램에 필요한 속성만 간추려 내어 표현하는 것을 추상화라고 한다.
- 객체지향 프로그래밍은 객체의 상태를 나타내는 데이터와 상태 데이터를 조작할 수 있는 동작을 하나의 논리적인 단위로 묶어 생각한다. 객체의 상태를 프로퍼티, 동작을 메서드라 부른다.

## 19.2 상속과 프로토타입
### 상속
- 어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속받아 사용하는 것으로 불필요한 중복을 제거한다.
- **자바스크립트는 프로토타입을 기반으로 상속을 구현한다.**

## 19.3 프로토타입 객체
- 객체지향 프로그래밍의 근간을 이루는 상속을 구현하기 위해 사용한다.
- 프로토타입을 상속받은 하위 객체는 상위 객체의 프로퍼티를 자신의 프로퍼티처럼 자유롭게 사용한다.
- 모든 객체는 `[[Protorype]]` 이라는 내부 슬롯을 가지며, 이 내부 슬롯의 값은 프로토타입의 참조(또는 null)이다.
- `[[Protorype]]`이 저장되는 방식은 객체 생성 방식에 의해 결정된다. 객체가 생성될 때 객체 생성 방식에 따라 프로토타입이 결정되고 `[[Protorype]]`에 저장된다.
- 모든 객체는 하나(이하)의 프로토타입을 갖는다. 그리고 모든 프로토타입은 생성자 함수와 연결되어 있다.
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_1.PNG)
- `[[Protorype]]`내부 슬롯에는 직접 접근할 수 없지만 `__proto__` 접근자 프로퍼티를 통해 자신의 프로토타입에 간접적으로 접근할 수 있다.
- 프로토타입은 자신의 constructor 프로퍼티를 통해 생성자 함수에 접근할 수 있고, 생성자 함수는 자신의 prototype프로퍼티를 통해 프로토타입에 접근할 수 있다.
### 객체 생성 방식에 따라
- 객체 리터럴에 의해 생성된 객체 : Object.protorype
- 생성자 함수에 의해 생성된 객체 : 생성자 함수의 prototype 프로퍼티에 바인딩

### 19.3.1 `__proto__` 접근자 프로퍼티
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_2.PNG)
> 콘솔에 객체를 출력했을 경우 자주 등장하는 프로토타입
- person 객체의 프로토타입인 Object.prototype은 `__proto__`접근자 프로퍼티를 통해 person 객체의 `[[Protorype]]` 내부 슬롯이 가리기는 Object.prototype에 접근한 결과를 크롬 브라우저가 콘솔에 표시한 것이다.

- 내부 슬롯은 프로퍼티가 아니다. 따라서 자바스크립트는 원칙적으로 내부 슬롯과 내부 메서드에 직접적으로 접근하거나 호출할 수 있는 방법을 제공하지 않는다.
- 일부 내부 슬롯과 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공한다.(`__proto__`)
- `__proto__`는 getter/setter함수를 가지고 있어 `__proto__`를 통해 프로토타입에 접근하면 내부적으로 getter함수로 접근하게 된다.

<br/>

- `__proto__`접근자 프로퍼티는 Object.prototype의 프로퍼티이다.
- 모든 객체는 상속을 통해 Object.prototype__proto__ 접근자 프로퍼티를 사용할 수 있다.
 
### `__proto__` 접근자 프로퍼티를 통해 프로토타입에 접근하는 이유
- 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위해서 

```javascript
const parent = {};
const child = {};

child.__proto__ = parent;
parent.__parent__ = child;
```
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_3.PNG)  
- 위 그림과 같이 서로가 자신의 프로토타입이 되는 비정상적인 프로토타입 체인이 만들어지면 프로토타입 체인의 종점이 존재하지 않기에 무한루프에 빠지게 된다.
- 따라서 `__proto__` 접근자 프로퍼티를 통해 프로토타입에 접근하고 교체하도록 구현되어있다.

### 그러나 `__proto__` 접근자 프로퍼티를 코드 내에서 직접 사용하는 것은 권장하지 않는다.
- 모든 객체가 `__proto__` 접근자 프로퍼티를 사용할 수 있는 것은 아니기 때문
  - 직접 상속을 통해 Object.prototype을 상속받지 않는 객체를 생성할 수 있기 때문에
- 따라서 Object.getPrototypeOf 메서드(읽기)(es5 도입), 
- Object.setPrototypeOf 메서드(쓰기)(es6 도입)를 권장한다

### 19.3.2 함수 객체의 prototype 프로퍼티
- 함수 객체는 생성자 함수가 생성할 인스턴스의 프로토타입을 소유하고 있다.
- prototype 프로퍼티는 생성자 함수가 생성할 객체의 프로토타입을 가리킨다. 따라서 생성자 함수로써 호출할 수 없는 함수, non-constructor인 화살표 함수와 es6메서드 축약 표현으로 정의한 메서드는 prototype프로퍼티를 소유하지 않고 프로토타입도 생성하지 않는다.

```javascript
//함수 객체는 prototype 프로퍼티를 소유한다.
(function () {}).hasOwnProperty('prototype'); -> true
//일반 객체는 prototype 프로퍼티를 소유하지 않는다.
({}).hasOwnProperty('prototype'); -> false
//non-constructor는 prototype 프로퍼티를 소유하지 않는다.
const obj = {foo() {}};
obj.foo.hasOwnProperty('prototype') -> false
```
- 모든 객체가 가지고있는(Object.prototype으로부터 상속반은) `__proto__` 접근자 프로퍼티와 함수 객체만이 가지고 있는 prototype 프로퍼티는 동일한 프로토타입을 가리킨다.그러나 **사용 주체가 다르다**
- `__proto__` : 모든 객체가 사용하고 자신의 프로토타입에 접근 또는 교체하기 위해 사용
- prototype 프로퍼티 : 생성자 함수가 사용하고 자신이 생성할 객체의 프로토타입을 할당하기 위해 사용

### 19.3.3 프로토타입의 constructor 프로퍼티와 생성자 함수
- 모든 프로토타입은 constructor 프로퍼티를 갖는다. 
- 이 특성으로 인해 함수 객체는 생성자 함수를 사용할 수 있다.
```javascript
function Person(name) {
  this.name = name;
}
const me = new Person('Lee');

me.constructor === Person  //true
```
Person 생성자 함수는 me 객체를 생성했다.   me객체는 Persond의 기능을 사용하려고 한다.  
이때 me 객체에는 constructor프로퍼티가 없지만 me 객체의 프로토타입인 Perton.prototype에는 constructor 프로퍼티가 있다.  
따라서 me 객체는 프로토타입인 Person.prototype의 constructor프로퍼티를 상속받아 사용할 수 있다.

## 19.4 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입
- 리터럴 표기법에 의한 객체 생성 방식으로 명시적으로 new 연산자와 함께 생성자 함수를 호출하여 인스턴스를 생성하지 않는 객체 생성 방식도 있다.
```
//객체 리터럴
const obj = {};
//함수 리터럴
const add = function (a, b) {return a + b};
//배열 리터럴
const arr = [1,2,3];
//정규 표현식 리터럴
const regexp = /is/ig;

//obj.constructor === Object  //true
```
obj 객체는 Object생성자 함수로 생성한 객체가 아니라 객체 리터럴에 의해 생성된 객체인데도 Object 생성자 함수와 constructor 프로퍼티로 연결되어 있다. 왜 그럴까?  
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_4.PNG)  
생성자 함수로 객체를 생성하는 경우
- Object 생성자 함수에 인수를 전달하지 않거나 undefined 또는 null이 인수로 전달되면 내부적으로 추상 연산 OrdinaryObjectCreate를 호출하여 Object.prototyp을 프로토타입으로 갖는 빈 객체를 생성한다.  

![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_5.PNG)  
생성자 함수로 객체를 생성하는 경우

![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_6.PNG)
- 객체 리터럴도 평가될 때 추상 연산 OrdinaryObjectCreate를 호출하여 빈 객체를 생성하고 프로퍼티를 추가한다.
- 그러나 내부 로직이 다르다.

- 즉, Object 생성자 함수 호출과 객체 리터럴의 평가는 추상 연산 OrdinaryObjectCreate를 호출하여 빈 객체를 생성하는 점에서 동일하지만 new.target의 확인이나 프로퍼티를 추가하는 처리 등 세부 내용이 다르다.
- 따라서 객체 리터럴에의해 생성된 객체는 Object 생성자 함수가 생성한 객체가 아니다.
- 다만 리터럴 표기법에 의해 생성된 객체도 상속을 위해 프로토타입이 필요하다. 
- 따라서 리터럴 표기법에 의해 생성된 객체도 가상적인 생성자 함수를 갖고 프로토타입도 더불어 생성된다. 
- **즉, 프로토타입과 생성자 함수는 단독으로 존재하지 않고 언제나 쌍으로 존재한다.**

### 사실 내부 로직을 제외하고 보면 큰 틀에서 차이는 없다.
- 생성과정에 미묘한 차이는 있으나 결국 객체로서 동일한 특성을 갖는다. 
- 생성과정과 스코프, 클로저 등의 차이가 있으나 함수로서 동일한 특성을 갖는다.
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_7.PNG)  
리터럴 표기법에 의해 생성된 객체의 생성자 함수  

## 19.5 프로토타입의 생성 시점
- 객체는 리터럴 표기법 또는 생성자 함수, (Object.create 메서드와 클래스로 객체를 생성하는 방법도 있다.) 에 의해 생성되므로 결국 모든 객체는 생성자 함수와 연결되어 있다.
- 프로토타입은 쌍으로 존재하므로 생성자 함수가 생성되는 시점에 더불어 생성된다.
### 19.5.1. 사용자 정의 생성자 함수와 프로톹타입 생성 시점
- 내부 메서드 construct를 갖는 함수 객체는 new 연산자와 함께 생성자 함수로서 호출될 수 있다.
- **생성자 함수로서 호출할 수 있는 함수, 즉 constructor는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성된다.**
```javascript
console.log(Person.prototype); // {constructor: f}
function Person(name) {
  this.name = name;
}
```
- 그러나 생성자 함수로서 호출할 수 없는 함수, 즉 non-constructor는 프로토타입이 생성되지 않는다.
```javascript
const Person = name => {
  this.name = name;
};
console.log(Person.prototype); //undefined
```
- 함수 선언문은 런타임 이전에 자바스크립트 엔진에 의해 먼저 실행된다. **즉 함수 선언문으로 정의된 Person 생성자 함수는 어떤 코드보다 먼저 평가되어 함수 객체가 된다.** 이때 프로토타입도 더불어 생성된다. 
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_8.PNG)  
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_9.PNG)  

생성된 프로토타입은 오직 constructor 프로퍼티만을 갖는 객체이다. 생성된 프로토타입의 프로토타입은 Object.prototype이다.

- 이처럼 빌트인 생성자 함수가 아닌 사용자 정의 생성자 함수는 자신이 평가되어 함수 객체로 생성되는 시점에 프로토타입도 더불어 생성되며, 생성된 프로토타입의 프로토타입은 언제나 Object.prototype이다.

### 19.5.2 빌트인 생성자 함수와 프로토타입 생성 시점
- Object, String, Number, Function, Array, RegExp, Date, Promise 등 빌트인 생성자 함수도 일반 함수와 마찬가지로 빌트인 생성자가 생성되는 시점에 프로토타입이 생성된다. 
- 생성된 프로토타입은 빌트인 생성자 함수의 prototype 프로퍼티에 바인딩된다.
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_10.PNG)   
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_11.PNG)  

## 19.6 객체 생성 방식과 프로토타입의 결정
객체는 다양한 생성 방법이 있다.
1. 객체 리터럴 
2. Object 생성자 함수
3. 생성자 함수
4. Object.create 메서드
5. 클래스(es6)

- 모든 객체는 추상 연산 OrdinaryObjectCreate에 의해 생성된다는 공통점이 있다.
- 추상연산 OrdinaryObjectCreate는 필수적으로 자신이 생성할 객체의 프로토타입을 인수로 전달받는다. 
- 그 후 자신이 생성한 객체의 `[[Prototype]]` 내부 슬롯에 인수로 전달받은 프로토타입을 할당한 다음, 생성한 객체를 반환한다.
- 즉, 프로토타입은 추상 연산 OrdinaryObjectCreate에 전달되는 인수에 의해 결정된다.
- 또한 이 인수는 객체의 **생성 방식에 의해 결정된다.**
### 19.6.1 객체 리터럴에 의해 생성된 객체의 프로토타입
```
const obj = { x: 1 };
```
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_12.PNG)  
객체 리터럴에 의해 생성된 obj 객체는 Object.prototype을 프로토타입으로 갖게되며, 이로써 Object.prototype을 상속받는다.

### 19.6.2 Object 생성자 함수에 의해 생성된 객체의 프로토타입
```
const obj = new Object();
obj.x = 1;
```
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_13.PNG)  
- 내부 로직은 달랐으나 객체 리터럴에 의해 생성된 객체와 동일한 구조를 갖는다.
- 생성 방식에 차이가 있는데 객체 리터럴 방식은 객체 리터럴 내부에 프로퍼티를 추가하지만 생성자 방식은 일단 빈 객체를 생성한 후에 프로퍼티를 추가해야 한다.

## 19.6.3 생성자 함수에 의해 생성된 객체의 프로토타입
```
function Person(name) {
  this.name = name;
}
const me = new Person('Lee');
```
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_14.PNG)  
- OrdinaryObjectCreate에 의해 생성자함수와 생성자함수의 prototype프로퍼티에 바인딩되어있는 객체와 생성된 객체 사이에 연결이 생긴다.
- Object생성자 함수와 더불어 생성된 Object.prototype은 다양한 빌트인 메서드 를 갖고 있지만 사용자 정의 생성자 함수 Person과 더불어 생성된 프로토타입 Person.prototype의 프로퍼티는 constructor 뿐이다.

![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_15.PNG)
- 생성자 함수를 통해 생성된 모든 객체는 프로토타입에 추가된 메서드를 상속받아 자신의 메서드처럼 사용할 수 있다.
- 이렇게 추가/삭제된 프로퍼티는 프로토타입 체인에 즉각 반영된다.

## 19.7 프로토타입 체인
```
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function () {
  console.log(`hi my name is ${this.name}`);
};

const me = new Person('Lee');

console.log(me.hasOwnProperty('name'));  // true
```
- me 객체는 Person.prototype뿐만 아니라 Object.prototype도 상속받았다는 것을 의미한다.
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_16.PNG)  
- 자바스크립트는 객체의 프로퍼티에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 `[[Prototype]]`내부 슬롯의 참조를 따라 부모 프로토타입의 프로퍼티를 순차적으로 검색한다. 
- 이를 프로토타입 체인이라고 한다.
- 프로토타입 체인은 자바스크립트가 객체지향의 상속을 구현하게 해준다.

#### 모든 객체는 Object.prototype을 상속받는다
- Object.prototype을 프로토타입 체인의 종점이라고 한다.
- Object.prototype의 프로토타입, 즉 `[[Prototype]]`내부 슬롯의 값은 null이다.
- 프로토타입 체인의 종점인 Object.prototype에서도 프로퍼티를 검색할 수 없는 경우 undefined를 반환한다. `이때 에러가 발생하지 않는 것에 주의하자`
```
console.log(me.foo)  //undefined
```
자주 겪는 문제(에러x)
- 프로토타입 체인(객체간 상속관계)은 상속과 프로퍼티 검색을 위한 메커니즘이다.
- 그에 반해, 프로퍼티가 아닌 식별자는 스코프 체인(함수의 중첩관계)에서 검색한다. 따라서 스코프 체인은 식별자 검색을 휘한 메커니즘이다.
## 19.8 오버라이딩과 프로퍼티 섀도잉
- 객체지향 프로그래밍에서의 오버라이딩도 프로토타입으로 구현되어있다.
```
const Person = (function () {
  function Person(name) {
    this.name = name;
  }

  Person.prototype.sayHello = function () {
    console.log(`hi name is ${this.name}`);
  };
  return Persosn;
}());

const me = new Person('Lee');

me.sayHello = function () {
  console.log(`hey name is ${this.name}`);
};

me.sayHello();
```
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_17.PNG)  
- 프로토타입이 소유한 프로퍼티를 프로토타입 프로퍼티, 인스턴스가 소유한 프로퍼티를 인스턴스 프로퍼티라고 부른다.
- 프로토타입 프로퍼티와 같은 이름의 프로퍼티를 인스턴스에 추가하면 프로토타입 체인을 따라 프로토타입 프로퍼티를 덮어쓰는 것이 아니라 인스턴스 프로퍼티로 추가한다.
- 인스턴스 메서드 sayHello는 프로토타입 메서드 sayHello를 **오버라이딩**했고 프로토타입 메서드 sayHello는 가려진다. 
- 상속관계에 의해 프로퍼티가 가려지는 현상을 **프로퍼티 섀도잉**이라고 한다.

![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_18.PNG)  
- 하위 객체를 통해 프로토타입의 프로퍼티를 변경 또는 삭제하는 것은 불가능하다.
- 하위 객체를 통해 프로토타입에 get 액세스는 허용되지만 set 액세스는 허용되지 않는다.

## 19.9 프로토타입의 교체
- 프로토타입은 임의의 다른 객체로 변경될 수 있다.
- 2가지 방법이 존재한다

### 19.9.1 생성자 함수에 의한 프로토타입의 교체
```javascript
const Person = (function () { 
  function Person(name) {
    this.name = name;
  }
  Person.prototyp = {
    sayHello() {
      console.log(`Hi my name is ${this.name}`);
    }
  }
  return Person;
}());

const me = new Person('Lee');
```
Person 생성자 함수가 생성할 객체의 프로토타입을 리터럴로 교체했다.  
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_19.PNG)    
- 아까 언급했듯 리터럴 객체는 constructor 프로퍼티가 없다. 
- 따라서 me 객체의 생성자 함수를 검색하면 Person이 아닌 Object가 나온다.
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_20.PNG)  


### 19.9.2 인스턴스에 의한 프로토타입의 교체
프로토타입은 prototype프로퍼티 뿐만 아니라 `__proto__`접근자 프로퍼티(또는 Object.getPrototypeOf 메서드)를 통해서도 교체가 가능하다

- 생성자함수를 교체하는 것은 미래에 생성할 인스턴스의 프로토타입을 교체하지만
- `__proto__`접근자 프로퍼티를 통해 교체하는 것은 이미 생성된 객체의 프로토타입을 교체할 수 있다.

```
function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

const parent = {
  sayHello() {
    console.log(`hi my name is ${this.name}`);
  }
};

Object.setPrototypeOf(me, parent);

me.sayHello();
```
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_21.PNG)  

#### 차이점
- 그렇게 크지 않은 차이가 있다.
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_22.PNG)

- 프로토타입은 직접 교체하지 않는 것이 좋다. 상속 관계를 인위적으로 설정하려면 19.11절 **직접 상속** 또는 클래스를 사용하는 편이 좋다.

19.10 instanceof 연산자

```
function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

const parent = {};

Object.setPrototypeOf(me, parent);

console.log(me instanceof Person)  // false
console.log(me instanceof Object);  // true
```
instanceof 연산자 사용
- instanceof 연산자는 프로토타입의 constructor 프로퍼티가 가리키는 생성자 함수를 찾는 것이 아니라 **생성자 함수의 prototype에 바인딩된 객체가 프로토타입 체인 상에 존재하는지 확인한다.**
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_23.PNG)  

## 19.11 직접 상속

### 19.11.1 Object.fcreate에 의한 직접 상속
- Object.create 메서드는 명시적으로 프로토타입을 지정하여 새로운 객체를 생성한다. 
- 마찬가지로 추상 연산 OrdinaryObjectCreate를 호출한다.

```
obj = Object.create(Object.prototype, {
  x: {value: 1, writable: true, enumerable: true, configurable: true}
});

// 동일한 코드
// obj = Object.create(Object.prototype);
// obj.x = 1;
// 동일한 코드
// obj = { x: 1 }
```
- Object.create 메서드는 첫 번째 매개변수에 전달할 객체의 프로토타입 체인에 속하는 객체를 생성한다.
- 이 메서드의 장점은 다음과 같다
  1. new 연산자 없이도 객체를 생성
  2. 프로토타입을 지정하면서 객체를 생성
  3. 객체 리터럴에 의해 생성된 객체도 상속받는다.
- ESLint에서는 Object.prototype의 빌트인 메서드를 객체가 직접 호출하는 것을 권장하지 않는다.
- Object.create 메서드를 통해 프로토타입 체인의 종점에 위치하는 객체를 생성할 수 있기 때문이다.
- 프로토타입 체인의 종점에 위치하는 객체는 Object.prototype의 빌트인 메서드를 사용할 수 없다.
```
const obj = Object.create(null);
obj.a = 1;

console.log(Object.getPrototypeOf(obj) === null);

//obj는 빌트인 메서드를 사용할 수 없다.
console.log(obj.hasOwnProperty('a'));  // TypeError: obj.hasOwnProperty is not a function
```

```
const obj = Object.create(null);
obj.a = 1;


console.log(Object.prototype.hasOwnProperty.call(obj, 'a'))
```
권장하는 방법(22.2.4절 간접 호출)
### 19.11.2 객체 리터럴 내부에서 __proto__에 의한 직접 상속
```
const myProto = { x: 10 };

const obj = {
  y: 20,
  __proto__: myProto
};

console.log(obj.x, obj.y);  //10 20
console.log(Object.getPrototypeOf(obj) === myProto);  // true
```

## 19.12 정적 프로퍼티/ 메서드
- 정적 프로퍼티/메서드: 생성자 함수로 인스턴스를 생성하지 않아도 참조/호출할 수 있는 프로퍼티/메서드
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_24.PNG)  
- 정적 프로퍼티/메서드는 생성자 함수가 생성한 인스턴스로 참조/호출할 수 없다.
- 자바에서 생성자함수같은 역할인듯
![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_25.PNG)
- 동일한 프로토타입 체인에 속해있지 않으므로 생성자 함수가 생성한 인스턴스가 호출할 수 없다.

![image](/public/Book_Review/ModernJS_DeepDive/19_프로토타입_26.PNG)

## 19.13 프로퍼티 존재 확인
### 19.13.1 in 연산자
```
const person = {
  name: 'lee',
}
console.log('name' in person);  // true
console.log('toString' in person);  // true
```
### 19.13.2 Object.prototype.hasOwnProperty 메서드
```
console.log(person.hasOwnProperty('name'));  // true

//중요
console.log(person.hawOwnProperty('toString'));
```
- own이 중요했다.

## 19.14 프로퍼티 열거

### 19.14.1 for ... in 문
```
for (const key in person) {
  console.log(key + ': ' + person[key]);
}
```
- for ... in문은 상속받은 프로토타입의 프로퍼티까지 열거한다!
- 하지만 toString과 같은 Object.prototype의 프로퍼티가 열거되지는 않는다.
- toString 메서드는 열거할 수 없는 프로퍼티로, 프로퍼티 어트리뷰트 `[[Enumerable]]`의 값이 false이다.
- 프로퍼티 키가 심벌이면 열거하지 않는다.
- 열거할 때 순서를 보장하지 않는다.( 하지만 대부분의 모던 브라우저에서 순서를 보장하고 숫자키에 대해서는 정렬도 해준다. )
- 배열은 for ... of 문을 권장하지만 배열도 객체이므로 for ... in 문 사용이 가능하다.

### 19.14.2 Object.keys/values/entries 메서드
- for ... in문은 상속받은 프로퍼티도 열거한다.
- 상속받은 프로퍼티를 열거하고 싶지 않다면 Object.keys/values/entries메서드를 권장한다.(Object.prototype.hasOwnProperty메서드로 추가 처리하는 것을 피함)
- Object.keys/values/entries는 열거가능한 프로퍼티를 배열로 반환한다.
```
console.log(Object.keys(person));
```
- es8에서는 Object.entries가 도입되었다.
- 키와 값의 쌍을 배열에 담아 반환한다.
```
console.log(Object.entries(person));
Object.entries(person).forEach(([key, value]) => console.log(key, value));
```





