# 링크 모음

## node.js
- ### express.js req, res 객체
https://luckyyowu.tistory.com/346  

- ### ESLint-Prettier-적용
https://velog.io/@recordboy/ESLint-Prettier-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0   
https://velog.io/@kyusung/eslint-prettier-config   
> 추가  
> 최종 세팅(prettier랑 같이 쓰니까 오류 라인 남아있는거 스트레스 받아서 못해먹겠어서 prittier는 삭제했다. beautify로 HookyQR.beautify 설정해서 쓰니 진짜 100배는 나은것 같다.)  
> 다시 추가  
> 리액트는 또 beaytify 안먹혀서 prittier써야 한다고 한다..  
- .eslintrc.json
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
  
- .jsbeautifyrc
```
{
  "js": {
    "brace_style": "collapse-preserve-inline"
  }
}
```

