---
layout: post
title: Django 튜토리얼(1)
category: django
tag: [django, python]
---

# 개발 서버 시작

서버를 시작하려면 간단한 명령어를 입력하면 된다. 이전 글에서도 말했지만, python 명령어는 본인이 설치한 파이썬 버전에 맞게끔 입력하면 된다.(3.x 버전의 파이썬도 환경변수를 설정하면 python 명령어로 입력 가능하지만, 본인은 그냥 진행하였다.)  
> ```python3 manage.py runserver```   

위 명령어를 실행하면 ```You have unapplied migration(s). Your project may not work properly until you apply the migrations for app(s)```라는 경고문과 함께 8000번 포트번호로 localhost url ```http://127.0.0.1:8000/```이 뜨게 된다. default로 설정된 포트번호가 8000번이므로 이와같은 주소가 생성되는데, 다른 포트번호를 이용하고 싶다면, ```python3 manage.py runserver 사용할포트번호```로 입력하면 된다.  
  
경고문은 아직 데이터베이스에 대해서 migration을 진행하지 않았기 때문에 출력되는 것이므로 일단 무시해도 문제 없다.  
  
위 주소로 접속해보면 로켓이 이륙하는 모습과 함께 congratulations 라는 문구가 보이면 성공적으로 동작한다고 볼 수 있다.
  
  
# 프로젝트를 구성하는 앱 만들기

이전 포스팅에서는 ```startproject```명령어를 입력해서 mysite 라는 프로젝트를 생성했다. 이번에는 ```startapp``` 명령어를 입력해 앱을 생성해볼 것이다. project는 다양한 기능의 app들의 집합체로 웹 사이트라고 보면 된고 app은 특정 기능을 제공하는 구성요소(?)라고 볼 수 있겠다.  
우선 아래 명령어를 입력해 설문조사 app을 생성해보자.  
> ```python3 manage.py startapp polls```    
```
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```
polls라는 디렉토리가 만들어지고 하위 파일 및 폴더가 생성된다.
  
   
# 뷰 작성하기

뷰를 작성하기 위해서는 polls 디렉토리의 views.py을 수정해야 한다. 
```
# polls/views.py
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```
index 페이지 요청에 대해 'hello world ~'라는 요청을 하는 것으로 보인다. 지금 생성한 뷰를 호출하기 위해서는 polls 디렉토리에 urls.py 라는 파일을 생성한 다음, index 페이지에 대한 요청임을 식별할 수 있도록 설정해주어야 한다.
```
# polls/urls.py
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```
index라는 뷰에 대해 url pattern을 지정해 주고 있다는 것을 짐작할 수 있다. 다음으로 현재는 polls app에서의 뷰를 생성하였으므로, 상위 디렉토리인 mysite 즉, 프로젝트에서 polls의 urls.py 파일을 읽을 수 있도록 설정해주어야 한다.
```
# mysite/urls.py
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
```
include 함수는 다른 urlconf를 참조할 수 있도록 도와주는 함수라고 한다. 즉, 하위 앱에서 정의한 urlconf를 쉽게 연결할 수 있도록 도와주는 함수라고 보면 된다.
  
이제 첫 페이지인 index view가 생성되었다. 이를 확인해 보려면 다시 runserver 명령어를 실행해주면 된다. 출력된 주소에 에러가 나타났다면 ```http://127.0.0.1:8000/polls/```를 입력해 보면 정상적으로 출력될 것이다.(포트번호의 경우 자신이 지정한 포트번호로 입력해야 한다.)  
  
여기까지 성공했다면 아직까지 장고를 포기하지 않고 공부하고 있다는 것이다...😅

