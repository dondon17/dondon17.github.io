---
layout: post
title: Django 튜토리얼(2)
category: django
tag: [django, python]
---

# settings.py 파일 설정하기
## 📍데이터베이스 설정
mysite 디렉토리 안에 settings.py 라는 파일이 있는 것을 확인할 수 있을 것이다. 이 파일은 장고 설정을 모듈 변수로 표현한 파이썬 모듈 파일이다. 그냥 기본적인 환경설정하는 파일이라고 생각하면 된다.  
  
이전 포스팅에서는 데이터베이스에 대해서는 아무런 작업을 하지 않아 migration 오류가 났던 것을 기억할 것이다. 이번에는 settings.py 파일에서 데이터베이스를 설정해줄 것이다.  
  
공식 문서에서는 그냥 파이썬에서 기본적으로 제공하는 sqlite3를 사용해도 된다고는 하지만, 이후에 발생할 골치 아픈 일들을 미리 방지하기 위해 postgreSQL 사용을 권장하고 있다. 
```
# mysite/settings.py
# Database
# https://docs.djangoproject.com/en/3.1/ref/settings/#databases

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```
데이터 베이스 설정은 ```ENGINE``` 필드를 바꿔주면 되는데, 기본으로 sqlite3가 설정되있음을 볼 수 있다. 다른 데이터베이스로 바꾸고 싶으면, ```sqlite3``` 부분을 mysql / oracle / postgresql 등으로 바꿔주면 된다. 이 외에도 다른 데이터베이스를 사용하는 경우에는 [공식 문서](https://docs.djangoproject.com/ko/3.1/intro/tutorial02/#database-setup)를 참고하자.  

  
## 📍타임존 설정
데이터베이스 설정을 다했으면 이제 timezone 설정해야한다. 타임존은 아래와 같이 설정해주면 된다. 다른 지역에 살고 있다면 [여기](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)를 참고하길 바란다.
```
TIME_ZONE = 'Asia/Seoul'
```

## 📍settings.py 살펴보기
기본적인 설정은 끝났고, settings.py 파일의 다른 곳을 살펴보도록 하자. 
```
INSTALLED_APPS = [
    'django.contrib.admin',         # 관리용 사이트
    'django.contrib.auth',          # 인증 시스템
    'django.contrib.contenttypes',  # 컨텐츠 타입을 위한 프레임워크
    'django.contrib.sessions',      # 세션 프레임워크
    'django.contrib.messages',      # 메세지 프레임워크
    'django.contrib.staticfiles',   # 정적 파일 관리 프레임워크
]
```
INSTALLED_APPS는 장고와 함께 딸려오는 기본 앱들이다. 음.. 일단 그냥 운영체제 설치시 이미 깔려있는 프로그램들이라고 생각하자.  


## 📍migration
이제 기본적인 설정이 끝났으니 마이그레이션을 해보자. 아래 명령어를 실행하면 자동으로 데이터베이스에 필요한 테이블들을 생성하게 된다. 명령어 입력시 터미널에서 파바박하고 뭔가가 진행되는 것을 볼 수 있다.
```
python3 manage.py migrate
```
