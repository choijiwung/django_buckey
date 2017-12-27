파이썬 프로젝트 생성

```
django-admin startproject website
```



파이참과 같은 IDE로 열어보면 

![1](django_bucket/1.PNG)

와 같이 프로젝트가 생성되어 있다.

`manage.py`는 건들이지말것!!!!!!

`setting.py`설정을 관리하는파일

`urls.py` 웹사이트 만들때 라우팅을 해주는 파일

ex) 우편 배달부가 어디로 우편을 보내야 하는지 적어놓은 곳이다.

 `wsgl.py` 나중에배움



# 서버실행시키기

콘솔창에 가서 실행시킨다. 

`python manage.py runserver`

각자 사용하는 인터넷 브라우저에서 

`127.0.0.1:8000`



App이란 프로그램으로써 실행 될 수 있는 최소단위 

(한줄로 요약할수 있으면 된다.)



`python manage.py startapp music` music 이라는 app이 생긴것이다.

모든 app은 database와 연결되어 있음.

