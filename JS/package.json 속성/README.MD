# package.json 

> 프로젝트 도중 확인할 수 있는 사전용으로 있는거 없는거 일단 다 넣기로 하였다. 안쓰는 속성이 굉장히 많다. 

## name 
- name 속성은 package.json 구조의 기본 구성 요소 중 하나이며 name은 package.json이 설명하는 모듈의 이름과 정확히 일치하는 string이다.
```
"name" : "metaverse"
```
## version 
- version 속성은 package.json의 핵심 부분으로 package.json 파일이 설명하는 모듈의 현재 버전을 나타낸다.
```
"version": "5.12.4"
```
## license 
- license 속성은 package.json 파일이 설명하는 모듈의 라이센스를 기록하는 데 사용된다. 
- license 속성을 사용하여 이중 라이센스 또는 자체 라이센스를 정의하는 등 복잡한 방법이 있지만 가장 일반적인 용도는 SPDX 라이센스 식별자를 사용하는 것이다. (ex:MIT, ISC, GPL-3.0)
```
"license": "MIT"
```
## description 
- description 속성은 모듈에 대한 사람이 읽을 수 있는 설명이 포함 된 string이다. 기본적으로 모듈 개발자는 모듈이 정확히 무엇인지 정확하게 알려 줄 수 있다.
- description 속성은 npm 검색과 npm CLI 검색 도구가 자주 인덱싱되어 검색 쿼리를 기반으로 관련 패키지를 찾을 수 있다.
```
"description": "The Metaverse virtual reality. The final outcome of all virtual worlds, augmented reality, and the Internet."
```
## keywords 
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
## main 
- main 속성은 package.json 이 설명하는 모듈에 대한 진입 방향이다. 
- Node.js 응용 프로그램에서 require 문을 통해 모듈을 호출하면 main 속성에 지정된 파일의 모듈 내보내기가 Node.js 응용 프로그램에 반환된다.
```
"main": "app.js"
```

## bin
- 많은 패키지는 PATH에 설치되는 하나 이상의 실행 파일을 가지고 있다. npm에서는 이를 매우 쉽게 구현할 수 있다. (실제로 이 기능은 "npm"을 설치하는 데에도 사용되고 있다.)
- 실행할 수 있는 패키지를 만들기 위해선 package.json 파일에 bin 항목을 제공해야 한다. 패키지 설치 시에, npm 은 bin 항목에 기술된 파일의 심볼릭 링크를 global install인 경우 prefix/bin 에, local install인 경우 ./node_modules/.bin/ 에 생성하게 된다.
- 예를 들어, myapp은 아래와 같이 bin 항목이 지정되어 있다.
```
"bin": { "myapp": "./cli.js" }
```

## directories
- CommonJS Packages 스펙에는 directories 개체를 사용해서 패키지 구성을 나타낼 수 있다. 
- npm의 package.json 을 보면 doc, lib와 man 으로 이루어진 디렉토리 구성을 확인 할 수 있다.

## repository 
- repository 속성은 모듈의 소스 코드가 어디에 존재하는지 정의하는 배열이다. 
- 일반적으로 오픈 소스 프로젝트의 경우 공개 컨트롤 GitHub의 저장소이며 저장소 배열은 버전 제어 유형이 git이고 repo 자체의 URL 임을 나타낸다.
- 한 가지 유의할 점은 repo에 접근할 수 있는 URL이 아니라 버전 컨트롤에 접근 할 수 있는 전체 URL 이다.
```
"repository": {
"type": "git",
"url": "https://github.com/bnb/metaverse.git"
}
```
## scripts 
- scripts 속성은 개념적으로 단순하지만 기능적으로 복잡하여 여러 사람이 작성 도구로 사용한다. 
- 원하는만큼의 key / value 를 가진 객체를 사용한다. 이 key / value 의 각 key는 실행할 수있는 명령의 이름이다. 
- 각 key의 해당 값은 실행되는 실제 명령이다. 스크립트는 모듈 작업에 필요한 명령을 테스트, 빌드 및 간소화하는 데 자주 사용된다.
```
"scripts": {
"build": "node app.js",
"test": "standard"
}
```
### scripts의 예약 key
> npm은 다음의 scripts를 package.json 파일의 “scripts” 속성에서 지원한다.

- prepublish: 패키지가 압축되어 배포되기 전에 실행합니다(뿐만 아니라 인자 없이 npm install 을 실행할 때에도 적용됩니다).
- prepare: 인자 없이 npm install 할 때와 git dependencies 를 설치할 때, 이 둘을 패키지가 압축되어 배포되기 전에 실행합니다. 이 명령은 republish 다음 prepublishOnly 전에 실행됩니다.
- prepublishOnly: 패키지가 압축되어 배포되기 전에 실행하지만, npm publish 일 때만 실행합니다.
- prepack: tarball(tar 압축 파일)이 압축되기 전에 실행합니다(npm pack, npm publish, 그리고 git dependencies 설치시에 적용됩니다).
- postpack: tarball(tar 압축 파일)이 생성된 후 최종 목적지로 이동한 후에 실행합니다.
- publish, postpublish: 패키지가 배포된 후 실행합니다.
- preinstall: 패키지를 설치하기 전에 실행합니다.
- install, postinstall: 패키지를 설치한 후에 실행합니다.
- preuninstall, uninstall: 패키지를 삭제하기 전에 실행합니다.
- postuninstall: 패키지를 삭제한 후에 실행합니다.
- preversion: 패키지 버전을 충돌시키기 전에 실행합니다.
- version: 패키지 버전이 충돌된 후, commit 전에 실행합니다.
- postversion: 패키지 버전이 충돌된 후, 그리고 commit 후에 실행합니다.
- pretest, test, posttest: npm test 명령어로 실행합니다.
- prestop, stop, poststop: npm stop 명령어로 실행합니다.
- prestart, start, poststart: npm start 명령어로 실행합니다.
- prerestart, restart, postrestart: npm restart 명령어로 실행합니다(주의: 만약 restart 스크립트가 제공되지 않은 경우 npm restart 는 stop 과 start 스크립트를 실행합니다).
- preshrinkwrap, shrinkwrap, postshrinkwrap: npm shrinkwrap 명령어로 실행합니다.



## dependencies 
- module의 package.json의 dependencies 속성은 dependencies (**이 모듈이 사용하는 다른 모듈**)가 정의되는 곳이다. 
- dependencies 속성은 각 종속성을 사용해야하는 이름과 버전을 가진 객체를 사용한다. 앞에서 정의한 version 속성으로 물건을 연결하면 모듈에 필요한 버전이 정의된다.
- 패키지 버전에 포함 된 캐럿 (^) 및 물결표 (~)는 자주 찾을 수 있다. 이 특수문자들은 버전 범위 표기법이다.


> - 버전 범위 표기법(semver)   
> version : 명시한 version 과 일치해야 한다.    
> &#62;version : 명시한 version 보다 높아야 한다.   
> &#62;=version  
> &#60;version  
> &#60;=version  
> ~version : 명시한 version 과 근사한 버전. 자세한 내용은 semver 참조.  
> ^version : 명시한 version 과 호환되는 것. 자세한 내용은 semver 참조.  
> 1.2.x : 1.2.0, 1.2.1, 등등. 1.3.0은 제외  
> http://... : 지정된 url로 패키지 설치시에 다운로드되고 설치된다.  
> &#42; : 모든 버전  
> "" : &#42; 와 같음  
> version1 - version2 : &#62;= version1 <= version2 과 같음.  
> range1 || range2 : range1 또는 range2  
> git... : Git url을 지정할 수도 있다.  
> user/repo : npm 버전 1.1.65 부터 GitHub url을 "foo": "user/foo-project" 와 같이 사용할 수 있다.  
> tag : tag가 지정되어 publish 된 특정 버전.   
> path/path/path : npm 버전 2.0.0부터 로컬 경로를 패키지에 포함시킬 수 있다. 로컬 경로는 npm install -S 나 npm install --save 로 설치할 수 있다.  

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

## devDependencies 
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

## peerDependencies
- 일반적으로 dependency는 내가 만든 모듈에서 사용하는 패키지들을 지정하는 반면, peerDependencies는 반대로 내가 만든 모듈이 다른 모듈과 함께 동작할 수 있다는 호환성을 표시한다. 
- 내가 만든 모듈이 다른 모듈의 모든 버전이 아니라 1.3 버전과만 동작한다면 그런 정보를 명시한다.
> 요구사항이 충돌하는 서로 다른 플러그인을 설치하려고 하면 오류가 발생한다. 이런 이유로, 당신의 플러그인 요구사항은 가능한 넓어야하고 특정 패치 버전들과 묶여선 안된다.
```
"name": "my_package",
"version": "1.3.5",
"peerDependencies": {
    "necessary": "2.x"
}
```

## bundledDependencies
- 패키지를 퍼블리싱할 때 번들되는 패키지 이름들의 목록

## optionalDependencies
- 사용을 원하는 모듈이지만, 없거나 설치가 실패해도 npm의 패키지 설치 과정이 중단되지 않도록 하려면, optionalDependencies 를 사용한다. 
- 여기에는 버전을 포함한 패키지 이름 혹은 url을 dependencies 와 같은 방식으로 기재한다. 
- 차이가 있다면, 빌드가 실패해도 설치가 중단되지 않고 이어서 다른 모듈을 설치하는 것이다.
-optionalDependencies 에 있는 패키지들은 dependencies 에 같은 이름이 있으면 덮어쓰게 되므로 가장 좋은 방법은 한쪽에만 기재하는 것이다.(dependencies를 쓰자..)

## homepage
- 프로젝트 홈페이지 주소이다.
- url 항목과는 다르며, url을 설정하면 예상치 못한 움직임을 하게 되므로 주의해야 한다.

## author
- 프로젝트 작성자 정보로, 한 사람만을 지정한다. 
- JSON 형식으로 name, email, url 옵션을 포함한다.
```
"author": {
  "name": "young",
  "email": "c@xz.com",
  "url": "http://github.com/owner/project/issues"
}
```

## files
- 프로젝트에 포함된 파일의 배열이다. 폴더 이름을 지정하면 폴더 안의 파일도 포함된다.
- 다음의 파일들은 설정에 관계없이 항상 포함된다.
```
package.json
README
CHANGELOG 
LICENSE 또는 LICENCE
```

## contributors
- 프로젝트에 참여한 공헌자 정보로, 여러 사람을 배열로 지정할 수 있다.

## config
- 소스 코드에서 config 필드에 있는 값을 환경 변수처럼 사용할 수 있다.

## private
- 이 값을 true로 작성하면 중앙 저장소로 저장하지 않는다.

## engine
- 실행 가능한 노드 버전의 범위를 결정한다.
- 주의할 점은, 사용자가 engine-strict config flag 를 설정하지 않으면 이 필드는 단지 조언용으로만 사용된다.

## os
- 모듈이 어떤 운영체제에서 작동하는지 지정할 수 있다. 
```
"os": ["darwin", "linux"]
```

## cpu
- 특정한 CPU 아키텍쳐에서만 동작한다면 그것역시 명시해줄 수 있다.

## preferGlobal
- 패키지가 글로벌 설치(-g 옵션을 붙여 설치)를 수행해야만 한다면, 이 값을 true로 해서 local 설치시에 경고 메시지를 제공할 수 있다.

## private
- 만약 "private": true 로 package.json 에 설정 해두면, publish 명령을 거부하게 된다.

## publishConfig
- publish 할때 사용되는 설정이다. tag 와 registry, access 를 다룰 때 편리한데, 이것들을 설정해서 패키지가 "lastest"로 태그되거나,  public registry 에 publish 되지 않도록 또 scoped module을 기본값으로 private 로 해주는 것 등을 쉽게 설정해줄 수 있다. 


## bugs
- 프로젝트의 이슈와 버그 트래킹을 볼 수 있는 url과 이슈를 알릴 email 주소를 입력한다. 
```
"bugs": {
  "url": "http://github.com/owner/project/issues",
  "email": "project@hostname.com"
}
```

> 출처:  
> https://medium.com/@yeon22/node-js-package-json%EC%9D%98-scripts-54e290adb5fb  
> https://medium.com/@hwanseogchoi/npm-package-json-2ceed25965b7  
> https://programmingsummaries.tistory.com/385  