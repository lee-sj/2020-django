
# Django project Start

## 가상환경 생성
``` bash
$ python3 -m venv myvenv
```

## 가상환경 실행
``` bash
$ source myvenv/bin/activate

# 가상환경 종료
$ deactivate
```

## django 설치
``` bash
# pip 최신화
$ python3 -m pip install --upgrade pip

$ pip install django

```

## django 프로젝트 생성
``` bash
$ django-admin startproject mysite 

```

# Django App Start

## django 앱 생성
``` bash
$ python manage.py startapp blog
```

## mysite/settings
``` python
# mysite/settings.py
# INSTALLED_APPS 에 추가하기

'blog',

```

## blog/templates/index
``` html
<!-- blog/templates/index.html
! + tab , h1 + tab , 텍스트 작성 -->
```

## blog/views
``` python
# blog/views.py
def index(request):
    return render(request, 'index.html')
```

## mysite/urls
``` python 
import blog.views
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', blog.views.index, name="index")
]
```

# Django URLS 

## blog/urls
``` python
from django.urls import path
from . import views

urlpatterns = [
	# Index
    path('', views.index, name='index'),
]
```

## mysite/urls
``` python
from django.contrib import admin
from django.urls import path, include
# import blog.views
from django.conf.urls import url

urlpatterns = [
    path('admin/', admin.site.urls),
    url('', include('blog.urls')),
    # path('', blog.views.index, name="index"),

]
```

# 404 handler

### New app Handler / App_Name=handlerpage / templates/404.html

## mysite/urls
``` python
# mysite/urls.py
from django.conf.urls import handler404
import handlerpage.views

handler404 = 'handlerpage.views.handler404'

```

## handlerpage/views
``` python
# handerpage/views.py
from django.views.defaults import page_not_found

def handler404(request, exception):
    return page_not_found(request, exception, template_name="404.html")

```

## handler/templates/404
``` html
<!-- handlerpage/templates/404.html
! + tab , h1 + tab , 텍스트 작성 --> 
```

# Sorry page

### Add views, urls, templates about Sorry_page and JS code to Index_page

## blog/views
``` python
# blog/views.py
def sorry(request):
	return render(request, 'sorry.html')
```

## blog/urls
``` python
# blog/urls.py
	path('sorry', views.sorry, name='sorry'),
```

## blog/templates/index
``` html
<!-- 파일 상단부에 JS 코드 추가 -->
<script type="text/javascript">
    if (screen.width <= 699) {
    document.location.href = "sorry";
    }
</script>
```

## blog/templates/sorry
``` html
<!-- sorry.html 파일 추가 
! + tab , h1 + tab , 텍스트 작성 --> 
```
