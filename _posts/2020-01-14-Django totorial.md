---
layout: post
title: Django 시작
category: django
tag: [django, python]
---

# 장고란?

🧑🏻‍💻 웹 공부를 하다보면 한번쯤 **장고**라는 이름을 한번쯤 들어봤을 것이다. [**Django**](https://www.djangoproject.com/)는 파이썬에서 제공하는 오픈소스 웹 프레임워크이다. 쉽게 말해 웹사이트를 쉽고 빠르게 그리고 편리하게 개발할 수 있도록 파이썬에서 제공하는 프레임워크라고 생각하면 된다.   

> ### 📍 대표적인 웹 프레임워크  
> Java - Spring  
> Python - Django, flask    
> Node.js - Express  
> Ruby - Ruby on Rails 

우연히 노마드코더 nicolas쌤의 강의를 보다가 장고에 대해 공부를 시작해보기로 했다. Flask도 파이썬에서 제공하는 오픈소스 웹 프레임워크 중 하나이다. Flask는 풀스택(Full-stack) 프레임워크인 Django와 다르게 마이크로(Micro) 프레임워크라고 한다. 음... 자신이 어떻게 웹 개발을 하느냐에 따라 두 프레임워크 중 하나를 선택하면 되는데, 장고는 기능은 엄청 많아서 정말 편리하지만 복잡하다는 경향이 조금 있는 것 같다. 반면 플라스크는 장고에 비해 매우 단순하고 가벼운 프레임워크라고 보면 될 것 같다. 두 프레임워크의 차이는 [장고 플라스크 차이](https://wendys.tistory.com/172) 게시글에 잘 정리되어 있으니 참고하면 좋을 것 같다.  
  
 
# 장고 설치

장고 공식 문서에 친절하게 설치하는 방법이 설명되어 있다. **[장고 공식 설치 가이드](https://docs.djangoproject.com/ko/3.1/intro/install/)**  
> ### 📍 빠른 설치 가이드
> 1. 파이썬 설치 - [파이썬 최신 버전 설치](https://www.python.org/downloads/)  
> 파이썬 버전은 이 후 설치할 장고 버전과 관련되있으므로, 서로 호환되는 버전을 설치하면 된다.  
> 2. 장고 설치 - [installing an official release with pip](https://docs.djangoproject.com/ko/3.1/topics/install/#installing-official-release)  
> 일반적으로 공식 릴리즈 설치를 진행하면 된다. 이 방법 외에도 개발자 버전으로 설치할 경우, 현재 개발중인 버전을 사용하면서 버그 리포트 등을 할 수도 있다.  
> 3. 설치된 장고 및 파이썬 버전 확인(mac os)  
> 본인은 맥에서 사용중이므로 아래와 같이 확인해 볼 수 있다. mac os에는 파이썬이 기본으로 설치되어 있는데 아마 2.7버전일 것이다. 현재 2021년 1월 기준으로 3.9 버전까지 나와있는데, 3.x 버전과 2.x 버전은 꽤 큰 차이가 있다고 하니 3.x 버전으로 설치하는게 좋을 것 같다.  
> 파이썬 버전 확인 : ```$ python3 --version``` (python --version 입력 시 2.7 버전이 출력된다.)  
> 장고 버전 확인 : ```$ python3 -m django --version```  

# 장고 시작  

이제 설치를 다했으니 진짜 장고를 시작해보자.  
먼저 본인이 작업할 디렉토리로 이동하고 터미널에 다음과 같이 ```$ django-admin startproject mysite``` 명령어를 입력하면 된다. 생성되는 디렉토리명은 mysite이며 디렉토리 이름은 자신이 원하는 것으로 설정하면 된다.  
```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```
생성된 mysite 디렉토리에 가보면 위와 같이 사이트 관리를 도와주는 역할을 하는 manage.py 파일과, 프로젝트를 위한 실제 파이썬 패키지들이 저장된 mysite라는 하위 디렉토리가 생성된다. 사실 공식문서에 있는 말을 그대로 한거라 정확히는 모르겠다.. 프로젝트를 서버에 올리는 것은 다음 포스팅으로 넘기자...
