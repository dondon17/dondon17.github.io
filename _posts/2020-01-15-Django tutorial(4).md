---
layout: post
title: Django 튜토리얼(3)
category: django
tag: [django, python]
---

# 모델 만들기
## 📍모델이란

모델이란 메타 데이터를 갖는 데이터베이스의 구조(layout)를 의미한다. 공식 문서 튜토리얼에서는 question과 choice 모델을 생성하는데, 어떻게 보면 데이터베이스의 테이블과 비슷한 개념이라는 생각이 든다. 모델의 생성은 자신이 생성한 app의 models.py 파일에 작성해주면 된다.  

## 📍모델 작성
```
# polls/models.py
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```
간단하게 살펴보면, charfield는 문자 타입의 데이터를 의미하고, DateTimeField는 시간 필드를 나타낸다는 것을 추측해볼 수 있다. 데이터베이스를 공부해본 경험이 있다면, 테이블 생성 시 Column의 이름과, 데이터 타입을 명시하는 것과 비슷하다고 느껴질 것이다. 
실로 ForeignKey를 사용함으로써 choice model에서는 question model과 연관되어 있다는 것을 알 수 있다. 이는 데이터베이스에서 외래키 참조 시 1:1, 1:N, N:M 관계로 연관될 수 있다는 것과 동일하다.

## 📍모델의 활성화
모델 활성화는 mysite 디렉토리의 settings.py 파일을 간단하게 수정해주면 된다.
```
# mysite/settings.py
INSTALLED_APPS = [
    'polls.apps.PollsConfig', # 이 코드 추가
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```
자세히 살펴보면, polls 앱의 apps.py 파일에 존재하는 PollsConfig 클래스를 참조하고 있는 것인데, 이를 polls.apps.PollsConfig 라는 경로로 표현하고 있음을 알 수 있다.  
  

```
$ python3 manage.py makemigrations polls
```
다음으로 위 명령어를 입력함으로써 작성한 모델과, 변경사항들을 장고에게 알려주게 된다. 아래의 실행결과를 보면, question과 choice 모델이 생성되었음을 알 수 있다. 즉, 아직 migration이 진행된 것이 아닌, 어떤 것들을 migration 하겠다 라고 알려주는 것이다.
```
# 실행 결과
Migrations for 'polls':
  polls/migrations/0001_initial.py
    - Create model Question
    - Create model Choice
```

다음으로 아래 명령어를 실행해보자.
```
$ python3 manage.py sqlmigrate polls 0001
```
위 명령어는 migraion시에 실행하는 sql 구문을 보여주는, 음... 가시성을 도와주는 명령어이다. 아래 실행 결과를 보면 무슨 의미인지 알 수 있을 것이다.
```
# 실행 결과
BEGIN;
--
-- Create model Question
--
CREATE TABLE "polls_question" (
    "id" serial NOT NULL PRIMARY KEY,
    "question_text" varchar(200) NOT NULL,
    "pub_date" timestamp with time zone NOT NULL
);
--
-- Create model Choice
--
CREATE TABLE "polls_choice" (
    "id" serial NOT NULL PRIMARY KEY,
    "choice_text" varchar(200) NOT NULL,
    "votes" integer NOT NULL,
    "question_id" integer NOT NULL
);
ALTER TABLE "polls_choice"
  ADD CONSTRAINT "polls_choice_question_id_c5b4b260_fk_polls_question_id"
    FOREIGN KEY ("question_id")
    REFERENCES "polls_question" ("id")
    DEFERRABLE INITIALLY DEFERRED;
CREATE INDEX "polls_choice_question_id_c5b4b260" ON "polls_choice" ("question_id");

COMMIT;
```

## 📍 모델 migrate
위에서는 모델을 생성하고, 생성된 모델이 어떤 sql로 생성되었는지 볼 수 있었다. 이제 migrate를 실행시켜 데이터베이스에 모델과 관련된 테이블을 생성해야한다. migrate 과정은 간단하다.
```
$ python3 manage.py migrate
```
위와 같이 명령어 입력 시, 이전에 생성한 모델들을 마이그레이션하여 데이터베이스에 실제 테이블로 생성하게 된다.

## 📍기타 
공식 문서의 튜토리얼을 하다보면, 여러 api를 이용해 생성한 모델에 대하여 작업하는 과정이 있는데, 이 부분은 [공식 문서](https://docs.djangoproject.com/ko/3.1/intro/tutorial02/#playing-with-the-api)를 보면서 실제로 해보는 것을 추천한다. 
