# Django是什么
>Django是Python的一个非常强大的Web应用框架, Django的优点主要在于强大的URL路由管理, APP管理, 后台管理, 全套的解决方案(包括session, cache, auth, 模板等), 以及非常丰富的支持文档. 非常适用于快速开发基于MVC的Web应用.

  ----

# 了解Djano的目录结构

![这里写图片描述](http://img.blog.csdn.net/20170406154621278?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMTU4MDcxNjc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

* **settings.py** 种存放这Djano的配置
```

import os

# Build paths inside the project like this: os.path.join(BASE_DIR, ...)
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

# Quick-start development settings - unsuitable for production
# See https://docs.djangoproject.com/en/1.11/howto/deployment/checklist/

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = '36=f$e19&zgqz94v!0t^0dxw9ul4(!)6t501ul!!e(!4apol%('

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True

ALLOWED_HOSTS = []

# Application definition  我们应用的定义（增加# 应用的话，需要在此方法后面进行追加）
# 非常方便的做到APP的管理。

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

# 是Django项目的根路由文件，该文件决定了所有路由配置规则
ROOT_URLCONF = 'DjangoDemo.urls'

# 设置web前端的模板目录
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates')]
        ,
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'DjangoDemo.wsgi.application'

# Database
# https://docs.djangoproject.com/en/1.11/ref/settings/#databases

# 数据库的设置
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        'PASSWORD': '',
        'HOST': '',

    }
}

# Password validation
# https://docs.djangoproject.com/en/1.11/ref/settings/#auth-password-validators

AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]

# Internationalization
# https://docs.djangoproject.com/en/1.11/topics/i18n/

LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'Asia/shanghai'

USE_I18N = True

USE_L10N = True

USE_TZ = True

# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/1.11/howto/static-files/

STATIC_URL = '/static/'

```

* **urls.py**用来进行地址映射
```
"""DjangoDemo URL Configuration

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/1.11/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  url(r'^$', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  url(r'^$', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.conf.urls import url, include
    2. Add a URL to urlpatterns:  url(r'^blog/', include('blog.urls'))
"""
from django.conf.urls import url
from django.contrib import admin

# 将项目文件进行导入
import DjangoDemo.blog.view as bv

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    # 我们先声明导入的文件后，即可通过文件进行操作我们需要当前路径映射到的方法
    url(r'^hello/$', bv.hello),

]

```

* 自己创建的**View.py**用来进行映射我们需要展现的前端内容
```

from django.http import HttpResponse

def hello(request):
    return HttpResponse("Hello world")
```
如果是**html文件，则可以使用**
```
from django.shortcuts import render  
def index(request):  
    return render(request, 'index.html')  
```
进行加载html.会从模板目录中找到index.html, 将其渲染到浏览器.


  ----
[Demo地址](https://github.com/houshuai0816/DjangoDemo)
