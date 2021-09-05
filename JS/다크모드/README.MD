# 다크모드

> 다크모드를 만드는 다양한 방법에 대해 알아보자
- 다크모드: 배경색을 어두운 색으로 변경하고 전경색을 밝은 색으로 변경하여 나같이 밤에 활동하는 사람한테 친숙한 ui를 만들어준다.
- 현재 Youtube, Instagram, Discord, Netflix 등 다양한 웹 서비스에서 지원한다.

## CSS

**기본적으로 전경색과 배경색은 CSS를 활용해 변경한다.**  
```CSS
.dark {
  background: white;
  color: black;
}

.white {
  background: black;
  color: white;
}
```

## 사용자 선호 테마를 감지하는 방법

### prefers-color-scheme
css 미디어 쿼리 규격 수준 5부터 미디어 쿼리에 prefers-color-scheme 가 추가되었다.  
미디어 쿼리는 브라우저 및 장치 환경이 지정한 규칙과 일치할 경우에만 CSS를 적용하는 CSS 문법이다.  
prefers-color-scheme는 공식적으로 사용자의 선호하는 칼라 테마를 지정하기 위해 만들어졌기 때문에 이것을 활용하는 편이 좋다.

- prefers-color-scheme: light 는 라이트 모드를 의미한다.
- prefers-color-scheme: dark 는 다크 모드를 의미한다.
- prefers-color-scheme: no-preference 는 사용자가 선호하는 테마를 알리지 않았음을 의미한다.

**이 방법을 활용하여 CSS를 적용한다.**
```CSS
<div class="themed">Theme</div>
.themed {
  background: black;
  color: white;
}

@media (prefers-color-scheme: light) {
  .themed {
    background: white;
    color: black;
  }
}
```

---

### Attribute 활용

조금 더 쉽고 일반적인 방법으로 속성값을 인식하여 테마를 변경하는 방법이 있다.  
root 요소에 속성값을 넣어 하위 테마를 모두 변경 가능하다.  


**root의 속성으로 color-theme를 주고 값을 light/dark로 변경한다.**  
```CSS
:root[color-theme='light'] {
  --background: #fff;
  --boxColor: #000;
}

:root[color-theme='dark'] {
  --background: #000;
  --boxColor: #fff;
}

html {
  background: var(--background);
}

.themed {
  background: var(--boxColor);
  color: var(--background);
}
```


---

### 메타 태그 활용
테마 토글 기능 없이 시스템의 테마를 따르면서 웹사이트를 제작하고 싶은 경우 메타 태그를 활용한다.
```html
<meta name="color-scheme" content="dark light" />
```
CSS를 관리하지 않아도 브라우저에서 추가하는 CSS(User Agent Stylesheet)가 시스템의 테마에 맞게 조정된다.


---

### localStorage, IndexedDB 등 활용

지금까지 방법은 설정이 브라우저에 저장되지 않는다.
따라서 localStorage를 활용하여 브라우저에 선호하는 테마를 저장하고, 웹 렌더링시 저장한 테마를 받아오는 형식으로 웹을 재접속하더라도 테마가 유지된다.
localStorage는 문자열만 저장할 수 있고, 메인 쓰레드를 차단할 여지도 있기 때문에 큰 데이터를 활용 시에는 indexedDB를 이용하도록 한다.  

```javascript
localStorage.setItem('color-theme', 'dark);
localStorage.setItem('color-theme', 'light);
```
하지만 다른 웹에서 prefers-color-scheme 를 이용하여 테마를 변경하였던가 테마가 지정되지 않은 순수한 상태일 경우도 있다.
따라서 3가지의 경우의 수를 모두 고려하여 상태를 입력한다.

```js
const isUserColorTheme = localStorage.getItem('color-theme');
const isOsColorTheme = window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';

const getUserTheme = () => (isUserColorTheme ? isUserColorTheme : isOsColorTheme);
```


---

## 테마를 추가하는 방법


### dataset
HTML의 dataset을 활용한다.  
dataset은 HTML 요소에 정보를 추가해주는 효과를 가진다.   
body에 data-theme를 추가하여 한꺼번에 테마 전체를 변경한다.  

```js
export const updateTheme = () => {
  const currentTheme = document.body.dataset.theme;
  const nextTheme = currentTheme === 'dark' ? 'light' : 'dark';
  localStorage.setItem('theme', nextTheme);
  document.body.dataset.theme = nextTheme;
};
```


---

### main stylesheet 전체를 변경

현재 사용중인 CSS stylesheet를 바꿔버린다.
쉽게 비교가 가능하고 여러가지 테마를 추가하기 쉽지만 network round trip을 한번 더 돌아야 하기 때문에 딜레이가 생길 수 있다.

```js
export const updateTheme = () => {
  const stylesheet = document.getElementById('theme');
  const currentTheme = stylesheet.getAttribute('href');
  const nextTheme =
    currentTheme === 'src/light.css' ? 'src/dark.css' : 'src/light.css';
  localStorage.setItem(
    'theme',
    nextTheme === 'src/dark.css' ? 'dark' : 'light',
  );
  stylesheet.href = nextTheme;
};
```
