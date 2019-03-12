
---
layout: post
title: " 第三百七十七节，Django+Xadmin打造上线标准的在线教育平台—apps目录建立，以及数据表生成 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百七十七节，Django+Xadmin打造上线标准的在线教育平台—apps目录建立，以及数据表生成**



****apps目录建立****

**我们创建一个apps目录，将所有的app放到 **apps目录里去，这样方便管理，也使目录更清楚，不管有多少app都统一到 **
**apps目录里去********

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170909133044585-34019575.png)**





**设置python可以识别apps目录路径**

**注意：我们在创建app后，python会自动到paa文件夹中找到相应的文件运行，当我们移动app到apps文件夹后，python程序将无法找到相应的文件了，**

****当我们移动app到apps文件夹后，** 此时我们需要两步解决**

**第一步，解决PyCharm无法识别 **paa文件的方法，在 **PyCharm将apps设置成python可识别路径，在apps文件夹 鼠标右键-
标记目录为-Sources Root******

******![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170909134526491-1560008522.png)******



******第二步，在 settings.py设置文件，将apps目录设置成python可识别目录，******

[code]

    https://docs.djangoproject.com/en/1.10/topics/settings/
    
    For the full list of settings and their values, see
    https://docs.djangoproject.com/en/1.10/ref/settings/
    """
    
    import os
    import sys
    
    # Build paths inside the project like this: os.path.join(BASE_DIR, ...)
    BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))      # 当前目录路径
    sys.path.insert(0, os.path.join(BASE_DIR, 'apps'))                          # 将apps目录设置成python可识别目录
    
    # Quick-start development settings - unsuitable for production
    # See https://docs.djangoproject.com/en/1.10/howto/deployment/checklist/
    
    # SECURITY WARNING: keep the secret key used in production secret!
    SECRET_KEY = '!#-519=(t8yl=of8^u$(zdcfcovctqlh0n2p#fky&9c3la+j1k'
    
    # SECURITY WARNING: don't run with debug turned on in production!
    DEBUG = True
    
    ALLOWED_HOSTS = []
    
    
    # Application definition
    
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app_users',                        # 注册 APP
        'app_courses',
        'app_organization',
        'app_operation',
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
    
    ROOT_URLCONF = 'MxOnline.urls'
    
    TEMPLATES = [
        {
            'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [os.path.join(BASE_DIR, 'templates')],           # 配置模板文件路径，也就是html路径
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
    
    WSGI_APPLICATION = 'MxOnline.wsgi.application'
    
    
    # Database
    # https://docs.djangoproject.com/en/1.10/ref/settings/#databases
    #
    # DATABASES = {
    #     'default': {
    #         'ENGINE': 'django.db.backends.sqlite3',
    #         'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    #     }
    # }
    
    #MySQL数据库
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',       # 配置数据库引擎名称
            'NAME': 'mxonline',                         # 数据库名称
            'USER': 'root',                             # 数据库用户名
            'PASSWORD': '279819',                       # 数据库密码
            'HOST': '127.0.0.1',                        # 数据库链接地址
            'PORT': '3306',                             # 数据库端口
        }
    }
    
    
    
    # Password validation
    # https://docs.djangoproject.com/en/1.10/ref/settings/#auth-password-validators
    
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
    # https://docs.djangoproject.com/en/1.10/topics/i18n/
    
    LANGUAGE_CODE = 'en-us'
    
    TIME_ZONE = 'UTC'
    
    USE_I18N = True
    
    USE_L10N = True
    
    USE_TZ = True
    
    
    # Static files (CSS, JavaScript, Images)
    # https://docs.djangoproject.com/en/1.10/howto/static-files/
    
    STATIC_URL = '/static/'
[/code]



**数据表生成**

**生成表需要在PyCharm的终端输入命令，先输入  makemigrations  然后在输入   migrate   来生成表**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170909140621694-1563539721.png)**



