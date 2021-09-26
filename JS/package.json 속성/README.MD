# package.json 속성
## name 속성
- name 속성은 package.json 구조의 기본 구성 요소 중 하나이며 name은 package.json이 설명하는 모듈의 이름과 정확히 일치하는 string이다.
```
"name" : "metaverse"
```
## version 속성
- version 속성은 package.json의 핵심 부분으로 package.json 파일이 설명하는 모듈의 현재 버전을 나타낸다.
```
"version": "5.12.4"
```
## license 속성
- license 속성은 package.json 파일이 설명하는 모듈의 라이센스를 기록하는 데 사용된다. 
- license 속성을 사용하여 이중 라이센스 또는 자체 라이센스를 정의하는 등 복잡한 방법이 있지만 가장 일반적인 용도는 SPDX 라이센스 식별자를 사용하는 것이다. (ex:MIT, ISC, GPL-3.0)
```
"license": "MIT"
```
## description 속성
- description 속성은 모듈에 대한 사람이 읽을 수 있는 설명이 포함 된 string이다. 기본적으로 모듈 개발자는 모듈이 정확히 무엇인지 정확하게 알려 줄 수 있다.
- description 속성은 npm 검색과 npm CLI 검색 도구가 자주 인덱싱되어 검색 쿼리를 기반으로 관련 패키지를 찾을 수 있다.
```
"description": "The Metaverse virtual reality. The final outcome of all virtual worlds, augmented reality, and the Internet."
```
## keywords 속성
- keywords 속성은 모듈에 대한 키워드 모음이다. 
- 키워드는 패키지, 관련 모듈 및 소프트웨어 및 개념을 식별하는데 도움이 된다. 
- keywords 속성은 항상 하나 이상의 string을 배열의 값으로 가지는 배열이 된다. 이러한 문자열 각각은 프로젝트의 키워드 중 하나가 된다.
```
"keywords": [
"metaverse",
"virtual reality",
"augmented reality",
"snow crash"
]
```
## main 속성
- main 속성은 package.json 이 설명하는 모듈에 대한 진입 방향이다. 
- Node.js 응용 프로그램에서 require 문을 통해 모듈을 호출하면 main 속성에 지정된 파일의 모듈 내보내기가 Node.js 응용 프로그램에 반환된다.
```
"main": "app.js"
```
## repository 속성
- repository 속성은 모듈의 소스 코드가 어디에 존재하는지 정의하는 배열이다. 
- 일반적으로 오픈 소스 프로젝트의 경우 공개 컨트롤 GitHub의 저장소이며 저장소 배열은 버전 제어 유형이 git이고 repo 자체의 URL 임을 나타낸다.
- 한 가지 유의할 점은 repo에 접근할 수 있는 URL이 아니라 버전 컨트롤에 접근 할 수 있는 전체 URL 이다.
```
"repository": {
"type": "git",
"url": "https://github.com/bnb/metaverse.git"
}
```
## script 속성
- scripts 속성은 개념적으로 단순하지만 기능적으로 복잡하여 여러 사람이 작성 도구로 사용한다. 
- 원하는만큼의 key / value 를 가진 객체를 사용한다. 이 key / value 의 각 key는 실행할 수있는 명령의 이름이다. 
- 각 key의 해당 값은 실행되는 실제 명령이다. 스크립트는 모듈 작업에 필요한 명령을 테스트, 빌드 및 간소화하는 데 자주 사용된다.
```
"scripts": {
"build": "node app.js",
"test": "standard"
}
```
## dependencies 속성
- module의 package.json의 dependencies 속성은 dependencies (**이 모듈이 사용하는 다른 모듈**)가 정의되는 곳이다. 
- dependencies 속성은 각 종속성을 사용해야하는 이름과 버전을 가진 객체를 사용한다. 앞에서 정의한 version 속성으로 물건을 연결하면 모듈에 필요한 버전이 정의된다.
- 패키지 버전에 포함 된 캐럿 (^) 및 물결표 (~)는 자주 찾을 수 있다. 이 특수문자들은 버전 범위 표기법이다.
```
"dependencies": {
  "axios": "^0.21.4",
  "bcrypt": "^5.0.1",
  "cheerio": "^1.0.0-rc.10",
  "dotenv": "^10.0.0",
  "express": "^4.17.1",
  "iconv-lite": "^0.6.3",
  "mongoose": "^6.0.7",
  "morgan": "^1.10.0",
  "pug": "^3.0.2"
},
```
## devDependencies 속성
- dependencies 속성과 거의 동일하며지만 주요 차이점이 있다. 
- dependencies 속성은 module이 production 환경에서 실행해야하는 dependencies을 정의하는 데 사용된다. 하지만 devDependencies 속성은 일반적으로 module이 개발에서 실행해야하는 종속성을 정의하는 데 사용된다.
```
"devDependencies": {
  "eslint": "^7.32.0",
  "eslint-config-airbnb-base": "^14.2.1",
  "eslint-plugin-import": "^2.24.2",
  "nodemon": "^2.0.12"
}
```

## homepage
- 프로젝트 홈페이지 주소이다.
- url 항목과는 다르며, url을 설정하면 예상치 못한 움직임을 하게 되므로 주의해야 한다.

## author
- 프로젝트 작성자 정보로, 한 사람만을 지정한다. 
- JSON 형식으로 name, email, url 옵션을 포함한다.

## contributors
- 프로젝트에 참여한 공헌자 정보로, 여러 사람을 배열로 지정할 수 있다.

## config
- 소스 코드에서 config 필드에 있는 값을 환경 변수처럼 사용할 수 있다.

## private
- 이 값을 true로 작성하면 중앙 저장소로 저장하지 않는다.

## engine
- 실행 가능한 노드 버전의 범위를 결정한다.

## bugs
- 프로젝트의 이슈와 버그 트래킹을 볼 수 있는 url과 이슈를 알릴 email 주소를 입력한다. 
```
"bugs": {
  "url": "http://github.com/owner/project/issues",
  "email": "project@hostname.com"
}
```
