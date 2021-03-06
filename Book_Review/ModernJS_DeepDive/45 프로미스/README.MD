# 45 프로미스
- ES6에서는 비동기 처리를 위한 또 다른 패턴으로 프로미스를 도입했다. 
- 프로미스는 전통적인 **콜백 패턴**이 가진 단점을 보완하며 **비동기 처리 시점을 명확하게 표현**할 수 있다는 장점이 있다.
## 45.1 비동기 처리를 위한 콜백 패턴의 단점

- 비동기 함수를 호출하면 함수 내부의 비동기로 동작하는 코드가 완료되지 않았다 해도 기다리지 않고 즉시 종료된다.
- 즉, 비동기 함수 내부의 비동기로 동작하는 코드는 비동기 함수가 종료된 이후에 완료된다.
- 따라서 비동기 함수 내부의 비동기로 동작하는 코드에서 처리 결과를 외부로 반환하거나 상위 스코프의 변수에 할당하면 기대한 대로 동작하지 않는다(진심)

### 이유
- 비동기 함수의 이벤트 핸들러는 이벤트가 발생하면 일단 태스크 큐에 저장되어 대기하다가, 콜 스택이 비면 이벤트 루프에 의해 콜 스택으로 푸시되어 실행된다.
- **즉, 동기함수가 먼저 실행된다**
- 이처럼 비동기 함수는 비동기 처리 결과를 외부에 반환할 수 없고, 상위 스코프의 변수에 할당할 수도 없다. 
- 따라서 비동기 함수의 처리 결과에 대한 후속 처리는 비동기 함수 내부에서 수행해야 한다. 이때 비동기 함수를 범용적으로 사용하기 위해 비동기 함수에 비동기 처리 결과에 대한 후속 처리를 수행하는 콜백 함수를 전달하는 것이 일반적이다.

### 콜백 헬
- 이처럼 콜백 함수를 통해 비동기 처리 결과에 대한 후속 처리를 수행하는 비동기 함수가 비동기 처리 결과를 가지고 또다시 비동기 함수를 호출해야 한다면 콜백 함수 호출이 중첩되어 복잡도가 높아지는 현상이 발생하는데, 이를 콜백 헬이라 한다.
```
get('/step1', a=>{
  get('/step2/${a}', b=>{
    get('/step3/${b}, c=>{
      get('step4/${c}, d=>{
        consolo.log(d);
      })
    })
  })
})
```
### 에러 처리의 한계
- 비동기 처리를 위한 콜백 패턴의 문제점 중 가장 심각한 것은 에러 처리가 곤란하다는 것이다.
```
try {
  setTimeout(() => {
    throw new Error('Error!');
  }, 1000);
}
catch (error) {
  console.error('캐치한 에러', error);
}
```
이 에러는 catch코드 블록에서 캐치되지 않는다.  
1. setTimeout이 호출되면 setTimeout함수의 실행 컨텍스트가 생성되어 콜 스택에 푸시되어 실행된다. 
2. setTimeout은 비동기 함수이므로 콜백 함수가 호출되는 것을 기다리지 않고 즉시 종료되어 콜 스택에서 제거된다.
3. 타이머가 만료되면 settimeout함수의 콜백 함수는 태스크 큐로 푸시되고 콜 스택이 비어졌을 때 이벤트 루프에 의해 콜 스택으로 푸시되어 실행된다.
4. 콜백 함수가 콜 스택에서 실행될 때 setTimeout함수는 이미 콜 스택에서 제거된 상태이다. 이것은 **setTimeout 함수의 콜백 함수의 호출자가 setTimeout함수가 아니라는 것을 의미한다.**
5. 에러는 호출자 방향으로 전파되기 때문에,  setTimeout함수의 콜백 함수 호출자는 setTimeout함수가 아니기 때문에 setTimeout함수의 콜백 함수가 발생시킨 에러는 catch 블록에서 캐치되지 않는다!

## 45.2 프로미스의 생성
- Promise는 호스트 객체가 아닌 ECMAScript사양에 정의된 표준 빌트인 객체이다
- Promise 생성자 함수는 비동기 처리를 수행할 콜백 함수를 인수로 전달받는데 이 콜백 함수는 resolve와 reject함수를 인수로 전달받는다.
- 만약 비동기 처리가 성공하면 비동기 처리 결과를 resolve 함수의 인수로 전달하면서 호출하고, 실패하면 에러를 reject함수에 인수로 전달하면서 호출한다.
- 프로미스는 상태 정보를 갖는다.
  - pending : 비동기 처리가 아직 수행되지 않은 상태
  - fulfilled : 비동기 처리가 수행된 상태(성공)
  - rejected : 비동기 처리가 수행된 상태(실패)
  - settled : fulfilled 또는 reject 상태

- 즉, 프로미스는 비동기 처리 상태와 처리 결과를 관리하는 객체이다.

## 45.3 프로미스의 후속 처리 메서드
- 프로미스의 처리 결과의 후속 처리를 위해 프로미스는 then, catch, finally를 제공한다.
- 모든 후속 처리 메서드는 프로미스를 반환하며, 비동기로 동작한다.

### 45.3.1 Promise.prototype.then
- then 메서드는 두 개의 콜백 함수를 인수로 전달받는다.
  1. fulfilled 상태의 콜백 함수
  2. rejected 상태의 콜백 함수
```
new Promise(resolve => resolve('fulfilled'))
  .then(v => console.log(v), e => console.error(e));
```
- then 메서드는 언제나 프로미스를 반환한다. 만약 then 메서드의 콜백 함수가 프로미스를 반환하면 그 프로미스를 그대로 반환하고, 콜백 함수가 프로미스가 아닌 값을 반환하면 그 값을 암묵적으로 resolve 또는 reject 하여 프로미스를 생성해 반환한다.

### 45.3.2 Promise.prototype.catch
- 프로미스가 rejected 상태인 경우만 호출된다.
- then 메서드와 마찬가지로 언제나 프로미스를 반환한다.

### 45.3.3. Promise.prototype.finally
- 프로미스의 성공 또는 실패와 상관없이 무조건 한 번 호출된다.
- 언제나 프로미스를 반환한다.


## 45.4 프로미스의 에러 처리
- then 메서드의 두번째 콜백 함수는 첫 번째 콜백 함수에서 발생한 에러를 캐치하지 못하고 코드가 복잡해져서 가독성이 좋지 않다.
- catch 메서드를 모든 then 메서드를 호출한 이후에 호출하면 비동기 처리에서 발생한 에러(rejected 상태) 뿐만 아니라 **then 메서드 내부에서 발생한 에러까지 모두 캐치할 수 있다.** (then 메서드도 프로미스를 반환하기 때문)

```
try {
    await mongoose.connect(mongoURI);
    console.log('몽고디비 연결!');
  } catch (error) {
    console.error('몽고디비 연결 에러', error);
  }
```
```
await mongoose.connect(mongoURI)
    .then(() => console.log('몽고디비 연결!'))
    .catch((error) => console.error('몽고디비 연결 에러', error));
```
이게 더 깔끔한듯  


## 45.5 프로미스 체이닝
- 프로미스는 then, catch, finally 후속 처리 메서드를 통해 콜백 헬을 해결한다.
- then, catch, finally 후속 처리 메서드는 언제나 프로미스를 반환하므로 연속적으로 호출할 수 있다.
- 이를 **프로미스 체이닝** 이라고 한다.

- 후속 처리 메서드는 콜백 함수가 반환한 프로미스를 반환한다. **만약 후속 처리 메서드의 콜백 함수가 프로미스가 아닌 값을 반환하더라고 그 값을 암묵적으로 resolve 또는 reject하여 프로미스를 생성해 반환한다!!**
> 하씨 미리 좀 제대로 공부할걸

## 45.6 프로미스의 정적 메서드
- 프로미스는 주로 생성자 함수로 사용되지만 함수도 객체이므로 메서드를 가질 수 있다. 
- 프로미스는 5가지 정적 메서드를 제공한다.

1. Promise.resolve : 인수로 전달받은 값을 resolve하는 프로미스를 생성한다.
2. Promise.reject : 인수로 전달받은 값을 reject하는 프로미스를 생성한다.
3. **Promise.all : 여러 개의 비동기 처리를 모두 병렬 처리할 때 사용한다.** 각각의 비동기 처리는 서로 의존하지 않고 개별적으로 수행된다. 비동기 처리를 순차적으로 처리할 필요가 없다.
   - Promise.all 메서드는 인수로 전달받은 배열의 프로미스가 **하나라도** rejected 상태가 되면 나머지 프로미스가 fulfilled 상태가 되는 것을 기다리지 않고 **즉시 종료한다.**
   - 모든 프로미스가 fulfilled 상태가 되면 **처리 결과를 배열에 저장**해 **새로운 프로미스를 반환**한다.
4. Promise.race : Promise.all과 달리 동시에 비동기되지만 **가장 먼저 fulfilled 상태가 된 프로미스**의 처리 결과를 resolve하는 새로운 프로미스를 반환한다. reject 상태는 동일하다.
5. Promise.allSettled : Promise.all과 달리 fullfilled 뿐만이 아닌 rejected상태(settled)까지 처리 결과를 배열로 반환한다.
   - 프로미스가 fulfilled 상태인 경우 비동기 처리 상태를 나타내는 status 프로퍼티와 처리 결과를 나타내는 value 프로퍼티를 갖는다.
   - 프로미스가 rejected 상태인 경우 비동기 처리 상태를 나타내는 status 프로퍼티와 에러를 나타내는 reason 프로퍼티를 갖는다.

## 45.7 마이크로태크스 큐
```
setTimeout(()=>console.log(1), 0);

Promise.resolve()
  .then(() => console.log(2))
  .then(() => console.log(3));
```
- 프로미스의 후속 처리 메서드의 콜백 함수는 태스크 큐가 아니라 마이크로태스크 큐에 저장된다.
- **마이크로태스크 큐는 태크크 큐보다 우선순위가 높다.**  
- 따라서 1 2 3 이 아니라 2 3 1 이 출력된다.

## 45.8 fetch
- Web API로서 역시 IE에선 제공 안한다.
