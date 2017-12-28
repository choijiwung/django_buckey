http://raccoonyy.github.io/django-2-0-release-note-summary/



인강은 1.9 버전으로 진행되었고 저는 2.0버전을 사용했기 때문에 다소 다른점이 있을 수도 있습니다. 

제가 개인적으로 django를 하면서 덧 붙였던 내용도 들어가 있습니다.

이해하는데 도움이 되셨으면 좋겠고 태클은 언제나 환영입니다.

이것은 저의 개인적인 공부를 위한 것입니다.



django란?

파이썬을 활용한 프레임워크입니다.

파이썬이란 프로그래밍 언어로써 사람과 기계가 소통하기 위한 언어라고 생각하시면 됩니다.

프레임워크란 간단히 설명하면 레고로 집을 만든다고 합시다. 작은 블럭(코드) 를 쌓아서 만들수도 있지만, 이미 완성된 틀을 가져와서 약간의 변형만 해서 집(프로그램)을 만들 수도 있겠죠.

빠르고 간편하게 개발을 위해서 만들어진 것이 프레임 워크 입니다.  





파이썬 프로젝트 생성

```
django-admin startproject website
```



파이참과 같은 IDE로 열어보면 

![1](1.PNG)

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



`python manage.py startapp music` 

music 이라는 app이 생긴것입니다.

모든 app은 database와 연결되어 있음.



`models.py` 는 데이터 베이스의 청사진이다. 나중에 이것을 토대로 데이터베이스가만들어진다.

`apps.py`이 어플리케이션을 위한 설정파일 `settings.py`와 같다.

`views.py`는 파이썬에서 function을 담당한다.  사용자로부터 데이터를 받고 가공하여 다시돌려주는 그런역할을 한다 (controller)



기본적인 원리는 편지(HTML문서)를 주고받는 것과 같다. 보통 편지를 쓰면 우표가 있어야 하고 받는사람 이름이있어야하고 주소가있어야하고 하는식의 정해진 양식에 따라야 한다. 이것을 HTTP라고 한다.  

우편배달부가 편지를 받으면 어디에 보내는지 주소를 보고 찾아야하는데 이것을 라우팅이라고 한다. 

편지를 쓰면 편지를 우체통에 넣고 우편배달부가 관할 우체국으로 보낸다. 그리고 관할 우체국에서 받는 사람의 관할 우체국으로 보내고, 관할 우체국의 우편배달부가 받는사람에게 편지를 전달한다. 이렇게 편지를 주고 받으면서 하는 것이 통신의 원리는 매우 흡사하다. 

django에서는 

`urls.py `에서 라우팅을 해주고 쉽게 표현하면 우편 배달부가 편지를 어디에 전달해야할지 알려준다고 보면 된다.

`views.py`에서는 답장을 해준다고 생각하면 된다. 우리가 편지를 받았고 그 편지에 답장을 어떻게 보낼지 정해준다고 생각하면된다. 

최상위 URLconf(우체국) 에서 `music.urls` 에서 편지를 받을 수 있도록 우편배달부에게 알려줍시다.

 `mysite/urls.py`  파일을 열고, `django.urls.include` 를 import 하고, `urlpatterns` 리스트에 [`include()`](https://docs.djangoproject.com/ko/2.0/ref/urls/#django.urls.include) 함수를 다음과 같이 추가 합니다.

`mysite/urls.py`

```
from django.urls import include, path
from django.contrib import admin

urlpatterns = [
    path('music/', include('music.urls')),
    path('admin/', admin.site.urls),
]

```



[`include()`](https://docs.djangoproject.com/ko/2.0/ref/urls/#django.urls.include) 함수는 다른 URLconf 들을 참조할 수 있도록 도와줍니다.

Django 가 함수 [`include()`](https://docs.djangoproject.com/ko/2.0/ref/urls/#django.urls.include) 를 만나게 되면, URL 의 그 시점까지 일치하는 부분을 잘라내고, 남은 문자열 부분을 후속 처리를 위해 include 된 URLconf 로 전달합니다.



즉 [`include()`](https://docs.djangoproject.com/ko/2.0/ref/urls/#django.urls.include) 를 만나게 되면 우편 주소로치면 서울광역시 관악구 까지만 잘라내고 남은 부분을 관악구 우체국에 보내게 됩니다. 남은 주소는 관악 우체국에서 처리하겠죠?



[`include()`](https://docs.djangoproject.com/ko/2.0/ref/urls/#django.urls.include) 에 숨은 아이디어 덕분에 URL 을 쉽게 연결할 수 있습니다. music 앱에 그 자체의 URLconf (`music/urls.py`) 가 존재하는 한, "/music/", 또는 "/fun_music/", "/content/music/" 와 같은 경로, 또는 그 어떤 다른 root 경로에 연결하더라도, 앱은 여전히 잘 동작할 것입니다.

```
언제 include() 를 사용해야 하나요?

admin.site.urls 를 제외한, 다른 URL 패턴을 include 할 때마다 항상 include() 를 사용해야 합니다.

이제 index view 가 URLconf 에서 연결되었습니다.

```





music 디렉토리에서 URLconf 를 생성하려면, `urls.py` 라는 파일을 생성해야 합니다. 정확히 생성했다면, app 디렉토리는 다음과 같이 보일겁니다.

```
music/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    urls.py
    views.py
```



"music/urls.py" 파일에는 다음과 같이 코드를 작성해 봅시다.

`music/urls.py`

```
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]

```



아까 위쪽에서 서울광역시 관악구 까지 짜르고 넘겨준다고 한거 기억나나요?

남은 신림동 최지웅씨 라는 주소를 여기서 처리한다고 보면 됩니다.

즉 이곳에서는 view에 있는 index로 편지를 보낸다는 뜻으로 이해하시면 됩니다.

`views.py`에 index라는 이름의 친구가 답장을 하게 되겠죠?

다시 한번 상기들이면 `view.py` 는 편지를 받아서 답장을 하는 곳이라고 말씀드렸습니다.



`music/views.py` 에 가서 다음과 같이 작성해 보겠습니다.

```
from django.http import HttpResponse

def index(request):
    return HttpResponse("<h1> This is my first HomePage</h1>")
```

앞에서 말한 편지(request라고 부릅니다) 가 왔을때 response라는 이름의 편지를 답으로 보내고 내용은 `This is my first HomePage` 가 되는 것입니다.

Django 에서 가장 간단한 형태의 view 입니다. view 를 호출하려면 이와 연결된 URL 이 있어야 하는데, 이를 위해 URLconf 가 사용됩니다.

이해가 안되는 말은 너무 오래 붙잡지 마시고 이해 되는 것부터 소화해 보세요!

여러분은 아직 코딩 베이비니까요!

나중에 전부다 먹어 치울 수 있을껍니다! 시간이 필요할 뿐이에요



아까 명령어를 실행했던 cmd화면에서 다음과 같이 실행해봅시다.

(앞서 실행했다면 다시실행시키지않아도괜찮아요!)

```
$ python manage.py runserver

```

브라우저에서 http://127.0.0.1:8000/music/를 입력하면 `index` view 로 정의한 " This is my first HomePage." 가 보일 것입니다.





# DataBase

