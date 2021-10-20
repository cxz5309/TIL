# 링크 모음

> 북마크가 너무 더러워서 싹 비우려고 만듦  
> 북마크 비우기 + 주제 없음 + 옛날 자료  
> 최소한의 분류정도만 할 예정.  

### 리소스
#### 눈누 상업용 무료한글폰트 사이트
https://noonnu.cc/
#### Font Awesome
https://fontawesome.com/
#### http://pngimg.com/ License Attribution-NonCommercial 4.0 International
http://pngimg.com/
#### 무료 사진  
https://unsplash.com/
#### 홈페이지 제작 툴
https://www.squarespace.com/
#### 게임 에셋 상업용 kenney
https://www.kenney.nl/
#### 구글 폰트
https://fonts.google.com/?selected=Material+Icons
#### 구글 아이콘
https://fonts.google.com/icons?selected=Material+Icons
#### 고대 게임 비상업용
https://www.spriters-resource.com/
#### mp3 커터
https://mp3cut.net/ko/
#### 유료 음악
https://www.pond5.com/
#### 게임 3d 에셋
https://www.mixamo.com/
https://www.cgtrader.com/
#### 무료 효과음 다운로드 사이트 35곳 소개!(상업적 이용 가능) : 네이버 블로그
https://blog.naver.com/PostView.nhn?blogId=ansthddns&logNo=221343778770&categoryNo=27&parentCategoryNo=27&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView

### html css 참고용
https://www.mysecretwoods.com/  
https://www.hazelight.se/about/  

### api
#### 라이브 스트리밍(돈듬)
https://www.brightcove.com/en/customers/
#### hammer.js
https://hammerjs.github.io/
#### nhn
https://www.toast.com/kr
#### 네이버
https://developers.naver.com/main/
https://www.ncloud.com/
#### public apis
https://github.com/public-apis/public-apis
https://public-apis.xyz/page/1
#### 웹성능
https://web.dev/vitals/#evolving-web-vitals

### 파서
#### html to markdown
https://www.browserling.com/tools/html-to-markdown
#### youtube to *
https://www.y2mate.com/kr/youtube-mp3/ffvl9lGGLvg
http://offliberty.co/
#### json to * and formatter
https://jsonformatter.org/
#### jsonlint
https://jsonlint.com/
#### mp3 to bpm
https://getsongbpm.com/tools/audio
#### csv to *
http://shancarter.github.io/mr-data-converter/

### phthon
#### 브라우저에서 텐서플로우 구동 Colaboratory
https://colab.research.google.com/notebooks/intro.ipynb#scrollTo=GJBs_flRovLc

### css
#### flex
https://flexboxfroggy.com/#ko
#### zeplin
https://zeplin.io/
#### css 사용 빈도
https://chromestatus.com/metrics/css/popularity
#### css 라이브러리
https://www.cssscript.com/
#### colorate
https://colorate.azurewebsites.net/ko/
#### design-seeds
https://www.design-seeds.com/winter-issue-no-3/
#### simpleicons
https://simpleicons.org/


### js
#### REST API 란 ?
https://ijbgo.tistory.com/20
#### js begginners
https://jsbeginners.com/javascript-projects-for-beginners/
#### 프론트엔드 개발자를 위한 자바스크립트 프로그래밍 요약
https://jooonho.com/js/2020-07-12-summary/
#### 모던 JavaScript 튜토리얼
https://ko.javascript.info/
#### CORS는 왜 이렇게 우리를 힘들게 하는걸까? | Evans Library
https://evan-moon.github.io/2020/05/21/about-cors/
#### 웹 최적화 방식 모음
https://black7375.tistory.com/72
#### 브라우저 XSS 필터 우회의 모든 것
https://blog.rubiya.kr/index.php/2019/03/28/browsers-xss-filter-bypass-cheat-sheet/
#### express.js req, res 객체
https://luckyyowu.tistory.com/346  
#### jekyll
https://jekyllrb-ko.github.io/
#### gatsby
https://www.gatsbyjs.com/
https://sungchul-p.github.io/gatsby-blog-starter
#### mysql 서버 적용
https://taetoungs-branch.tistory.com/95
https://velog.io/@taelee/mysql-user%ED%99%95%EC%9D%B8-%EB%B0%8F-%EC%B6%94%EA%B0%80
#### sequelize
https://velog.io/@cadenzah/sequelize-document-2

#### ESLint-Prettier-적용
https://velog.io/@recordboy/ESLint-Prettier-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0   
https://velog.io/@kyusung/eslint-prettier-config   
> 추가  
> 최종 세팅(prettier랑 같이 쓰니까 오류 라인 남아있는거 스트레스 받아서 못해먹겠어서 prittier는 삭제했다. beautify로 HookyQR.beautify 설정해서 쓰니 진짜 100배는 나은것 같다.)  
> 다시 추가  
> 리액트는 또 beaytify 안먹혀서 prittier써야 한다고 한다..  

<details>
    <summary>.eslintrc.json</summary>

```
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": ["eslint:recommended", "airbnb-base"],
  "parserOptions": {
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "rules": {
    "indent": [
      "error",
      2
    ],
    "linebreak-style": [
      "error",
      "windows"
    ],
    "quotes": [
      "error",
      "single"
    ],
    "semi": [
      "error",
      "always"
    ],
    "comma-dangle": [
      "error", "never"
    ],
    "import/extensions": [
      "error", "always"
    ]
  }
}
```

</details>

<details>
    <summary>.jsbeautifyrc</summary>

```
{
  "js": {
    "brace_style": "collapse-preserve-inline"
  }
}
```

</details>


### ts
#### 타입스크립트 핸드북
https://joshua1988.github.io/ts/intro.html


### db
#### 지금까지 겪은 DB에 하지 말아야 할 짓
https://velog.io/@juunini/%EC%A7%80%EA%B8%88%EA%B9%8C%EC%A7%80-%EA%B2%AA%EC%9D%80-DB%EC%97%90-%ED%95%98%EC%A7%80-%EB%A7%90%EC%95%84%EC%95%BC-%ED%95%A0-%EC%A7%93

### 강의
#### pluralsight
https://www.pluralsight.com/
#### 구글 코드랩
https://codelabs.developers.google.com/

## 게임
#### 아이펀엔진 doc
https://www.ifunfactory.com/engine/documents/reference/ko/index.html
#### 뒤끝
https://www.thebackend.io/
https://mrbinggrae.tistory.com/category/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8%20%EA%B0%95%EC%A2%8C/%20%EC%9C%A0%EB%8B%88%ED%8B%B0%20+%20%EB%92%A4%EB%81%9D%EC%84%9C%EB%B2%84
#### unity 구글 플레이 연동 및 파이어 베이스 사용기 (환경 및 오류 위주)
https://zprooo915.tistory.com/43
#### Unity 23.구글 서비스 사용하기 앱 등록하기
https://you-rang.tistory.com/143?category=735088
#### 대충 살아가는 게임개발자 :: (수정) "유니티에서는"어째서 PNG보다는 TGA가 더 쓸모있는 파일 포맷인가?
https://chulin28ho.tistory.com/362
#### 유니티 NGUI Sprite 핵심만
https://mailmail.tistory.com/69
#### Unity : 최적화, 용량 줄이기 : 네이버 블로그
https://m.blog.naver.com/PostView.nhn?blogId=friendding&logNo=60204107958&proxyReferer=https:%2F%2Fwww.google.com%2F
#### 가비지컬렉션
https://hijuworld.tistory.com/41
#### c, c#
https://moguwai.tistory.com/entry/C%EA%B3%BC-C%EC%9D%98-%EB%AC%B8%EB%B2%95%EC%A0%81%EC%9D%B8-%EC%B0%A8%EC%9D%B4%EC%A0%90?category=381220
#### C# 강의
http://m.csharpstudy.com/home/index
#### 유니티속 C# 작성 시 주의사항 모음
https://korstrix.github.io/unity/c%23/coding/know/Unity_C-_WarningList/
#### [ Pattern ] State Pattern(상태 패턴) in Unity C# – Rapapa Dev Story
http://rapapa.net/?p=3211
#### 스크린샷
https://charo.tistory.com/m/8
#### 유니티3D에서 2D 이미지 다루기
https://www.slideshare.net/jungsoopark104/3d-2d
#### [C#] Virtual(가상) vs Abstract(추상) vs Interface(인터페이스)
https://hongjinhyeon.tistory.com/m/93
#### 안드로이드 스튜디오 권한설정하기
https://wowon.tistory.com/148
#### 유니티 저장 파일 폴더 위치 확인 / 파일 경로 Application Path :: Chameleon Studio
https://chameleonstudio.tistory.com/62
#### Serializable Dictionary
https://redforce01.tistory.com/243
#### 유니티 에셋 추천 / 유니티 에셋스토어
https://mentum.tistory.com/393
#### [Unity] 유니티 tip 100 정리(Unity tip 100) total 21 tips
https://guks-blog.tistory.com/entry/Unity-%EC%9C%A0%EB%8B%88%ED%8B%B0-tip-100-%EC%A0%95%EB%A6%ACUnity-tip-100-total-21-tips   
#### Drawing 2D lines and Adding Collider to it « Unity Coding – Unity3D
https://unitycoder.com/blog/2017/09/23/drawing-2d-lines-and-adding-collider-to-it/
#### 유니티 모바일 최적화 체크리스트 60 프레임에 도전해보자!
https://dodnet.tistory.com/m/4178
#### A* 알고리즘 쉬운 개념 설명
https://deliorange.tistory.com/110
http://egloos.zum.com/cozycoz/v/9748811#type=comment&page=3
#### 게임 에셋 깃허브 
https://github.com/mixandjam


### 기타
#### 백준/Node.js Node.js 입력 받기
https://velog.io/@exploit017/%EB%B0%B1%EC%A4%80Node.js-Node.js-%EC%9E%85%EB%A0%A5-%EB%B0%9B%EA%B8%B0
https://jeonghwan-kim.github.io/node/2017/07/03/node-stream-you-need-to-know.html
#### 프로그래밍 배울 수 있는 사이트들 많이 모아 놓은곳(엄청 오래됨)
https://blog.naver.com/hannaj92/220136898436
#### IT 관련 유용한 사이트 공유합니다
http://devkorea.co.kr/bbs/board.php?bo_table=m04_01&wr_id=928
#### 배민라이더스운영시스템(1.0)
https://kimchanjung.github.io/projects/2020/01/01/bros-v1/
#### 좋은 남의 글
https://www.notion.so/668fc3a6067f45668ca074857cac0766?v=11d02c095bd940a688fc98adce153575
