# passport.js

- http://www.passportjs.org/

## 배경
- 웹에서 정보를 보안에 부적절하다고 여기고 자사의 정보를 숨기던 시절 트위터는 외부에서 자사의 서비스 데이터를 읽어갈 수 있는 api를 제공하였다. 이로 인해 트위터를 이용한 많은 웹앱들이 등장하였고 페이스북, 구글, 아마존 등 글로벌 기업들의 트렌드가 자사의 데이터를 공개하는 방향으로 바뀌게 되었다. 
- 문제는 인증인데 인증을 타 앱에서 이용하기 위해서는 비밀번호를 공개해야만 하는데 심각한 보안적 문제를 초래하게 된다. 이를 위해 OAuth, OpenID와 같은 표준화된 보안 인증 기법이 등장하게 된다. 또한 외부 서비스에 주는 권한도 제한할 수 있게 되었다.
- 이후로 다양한 인증 기법들이 쏟아져 나오게 되었는데 express 프레임워크에서 제공하는 passport.js 도 그 중 하나이다. 

## 특징
- passport는 전략(strategy)이라는 방법으로 다양한 인증 방법을 구현할 수 있도록 해 주는 Node.js용 미들웨어이다.
- strategy란 말 그대로, passport 미들웨어에서 사용하는 인증 전략인데, 약 300가지가 넘는 방법의 전략을 지원하고 있다고 한다.
> - http://www.passportjs.org/packages/
> - 척 보기만 해도 아주 많은 전략을 사용할 수 있다.
- passport의 strategy라는 인증 방법은 모듈식이기 때문에 Express 기반 웹 응용 프로그램에서 사이드이펙트를 발생시키지 않을 수 있다. 심지어 페이스북이나 구글, 카카오, 깃허브 등의 다양한 글로벌 웹 서비스의 인증 시스템의 인증 방식을 개별로 적용시키지 않고 passport만으로 해결이 가능하다! 
- 게다가 기본 로컬 스토리지나 jwt 등의 간편한 로그인 방법까지도 지원하고 있으며 문법이 통일되어있기 때문에 사용하기도 간단하다.

passport.js 메인 화면에선 이렇게 광고하고 있다.
```
passport.authenticate('github');
passport.authenticate('twitter');
passport.authenticate('facebook');
passport.authenticate('google');
```
> 정말 간편해 보인다

## 사용 방법
TODO (실 사용때 배우면서 스크립팅할 예정)