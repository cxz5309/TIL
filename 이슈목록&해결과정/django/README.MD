# django 오류 목록

## pip 업그레이드시 거부되는 문제

### 장고 프로젝트 만드는 순서는 이렇다
1. pip install -upgrade pip
2. python -m venv venv
3. 가상환경 접속 - 윈도우
   - venv\Scripts\activate
4. pip install django
5. django-admin startproject config.
6. python manage.py runserver

### 3. venvScriptsactivate: command not found
- 먼저 명령어가 이상하게 나온다.
- 아마도 터미널을 git bash로 사용하기 때문이 아닐까 \가 아닌 /로 바꾸어 보았다.
### 가상환경에 접속했는지 확인이 안됨
- activate를 했으나 아무런 반응이 없다.
- 안되겠다 싶어서 터미널을 power shell로 변경

### 보안 오류
```
 파일을 로드할 수 없습니다. 자세한 내용은 about_Execution_Policies(https://go.microsoft.com/ 
fwlink/?LinkID=135170)를 참조하십시오.
위치 줄:1 문자:1
+ venv\Scripts\activate
+ ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : 보안 오류: (:) [], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess
```
- 잊고있던 power shell 보안 오류
- 그러고 보니 보안 오류 때문에 git bash를 쓰고 있었다.
### - 터미널을 cmd로 변경하니 해결하였다. 예전에 관리자 권한 문제 때문에 cmd도 안쓰고 git bash로 했었던것 같았는데 파이썬 가상환경 실행하는데는 문제없었다.
### - 근본적인 해결 방법
- https://chinsun9.github.io/2020/10/15/vscode-%ED%95%AD%EC%83%81-%EA%B4%80%EB%A6%AC%EC%9E%90-%EA%B6%8C%ED%95%9C-%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0/