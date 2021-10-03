# 장고(Django) 소개
 - 파이썬 기반의 웹 프레임워크
 - 풀스택 개발 지원
 - 무료 오픈소스
 - 생산성이 높다

## 프레임워크(FrameWork)
- 소프트웨어 개발을 위한 기능, 구조의 틀을 제공
- 시스템 흐름을 프레임워크 제어함

## 라이브러리(Library)
- 소프트웨어 개발을 위한 기능을 제공
- 시스템 흐름을 개발자가 제어함

## 장고 작동 흐름
![image](https://eunhyejung.github.io/assets/contents/django-content01.PNG)
기본적인 장고의 작동 흐름
![image](https://eunhyejung.github.io/assets/contents/django-content02.PNG)
장고 프로젝트 실행시 생성되는 파일들

## 장고 특징
- 장고는 웹개발시 필요한 기능들을 제공함: 
  1. ORM, 
  2. Admin, 
  3. Authentication, 
  4. Security
  5. Templates
  6. Internationalization
- MTV 디자인패턴을 사용
- 장고는 앱(App)단위로 프로젝트가 구성됨

## MTV 디자인 패턴
| 구분     | 역할                                 | 파일      |
| -------- | ------------------------------------ | --------- |
| Model    | 데이터관리, 데이터베이스와연결및실행 | models.py |
| Template | 데이터출력, 사용자에게표현방식정의   | html      |
| View     | 컨트롤러, 비즈니스로직을처리         | views.py  |

## 장고앱(App)
- 앱(App)이란 장고프로젝트 구성하는 모듈을 의미함
- 장고프로젝트 관점에서 관련된 기능을 모아둔 파이썬 파일
- 앱이름은 영문 복수형으로 생성
  
### pip(Package Installer for Python)
- 파이썬 패키지를 관리해주는 프로그램 
- pip‒h를 통해 명령어 확인할수 있음

### PyPI(Python Package Index)
- 파이썬 코드로 작성된 패키지 저장소

## 가상환경(Virtual Environments)
- 독립적인 파이썬 환경을 제공 
- 가상환경 별로 설치된 모듈, 패키지의 영향을 받지 않음

## 장고 프로젝트

### venv
- 프로젝트별 가상환경 디렉토리
- 가상환경명은 사용자가 정하나 일반적으로 venv로 많이 사용됨
- 가상환경 생성 명령어 : python‒m venv[가상환경명]
  - Windows: python‒m venv venv
  - MacOS: python3‒m venv venv

### config
- 프로젝트 설정 파일을 모아두는 프로젝트 디렉토리
- 프로젝트 이름은 개발자가 정하나 config로 사용하는것을 권장

### &#95;	_init__.py
- 디렉토리를 패키지로 인식할 수 있도록 하는 파일
- 파이썬에서 정한 규칙

### asgi.py
- ASGI(Asynchronous Server Gateway Interface)
- 비동기 서버 게이트웨이 인터페이스로 웹서버와 WAS를 연결해주는 역할

### settings.py
- 장고 프로젝트를 설정하는 파일

### urls.py
- 장고프로젝트의 URL을 선언 
- 파일, 클라이언트가 요청을 할수 있도록 URL을 선언

### wsgi.py
- WSGI(Web Server Gateway Interface)
- 웹 서버 게이트웨이 인터페이스로 웹 서버와 WAS를 연결해주는 역할

### manage.py
- 장고의 명령어를 실행하기 위한 파일
- 자주사용하는명령어
  - python manage.py runserver
  - python manage.py createsuperuser
  - python manage.py makemigrations
  - python manage.py migrate