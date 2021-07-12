# Django notes

## Day 1 (2021-07-04)

初步感觉Django比较繁琐，而Ruby on rails比较简洁，Rails很多东西可以用command line快速实现。再继续学习下，说不定你也会喜欢上Django，发现它好的一面。

## Day 2 (2021-07-09)

这个视频我居然能坚持听完，讲得挺有意思的😃。

<iframe width="726" height="408" src="https://www.youtube.com/embed/-80wbZiSPRY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Day 3 (2021-07-10)

为什么要用Generic Views呢？感觉一开始不用也很好啊。Django tutorials一开始没有使用Generic Views我觉得挺好，而是用最自然最原始的一种方法处理url，让你可以快速掌握url, view & template这些概念和应用，而不是花时间去适应和深究Generic View这种模版。

Django的好处之一就是可以自动生成url，可以随意调用。

Start a new project.

```
django-admin startproject your-project-name
```

Run the development server.

```
python3 manage.py runserver
```

Create a new app in your project.

```
python3 manage.py startapp your-app-name
```

### Database and model

After creating your app models, you can make migration. 

```
python3 manage.py makemigrations
```

After this command, the migration file is created. Now it is time to migrate and create tables in your database.

```
python3 manage.py migrate
```

## Day 4 (Jul 12, 2021)

Django is good at app structure design. For example, I can easily divide a project to two parts: model-related apps and non-model-related apps.

```
project-name/
  -- model-related app/
  -- non-model-related app/
```

A non-model-related app here can be your static pages, such as `about`, `help` etc. The model-related app can be anyone of your business logic.

```
pages/
  -- urls.py
  -- views.py
  -- templates/pages/
     -- about.html
     -- help.html
```

The `pages/urls.py` may like this.

```py
from django.urls import path
from . import views

urlpatterns = [
    path('about', views.about, name='about'),
    path('help', views.help, name='help')
]
```

The `pages/views.py` may like this.

```py
from django.http import render

def about(request):
    # to get the about.html from the templates/
    pass

def help(request):
    # to get the help.html from the templates/
    pass
```

### Authorization

对权限管理这部分，我的初步想法是，创建一个权限表，记录各类型用户的对各类资源的权限. `Permissions` tables is like.

User_role | Resource | Permission (read,write?)
-- | -- | --
Superuser |  
Admin |   |  
一般user |   | 

`Users` table. 也许创建一个`Roles` table更合理，然后对`User` table进行关联。一个User可以有多种多色，如admin和一般user，这个表怎么处理比较恰当呢？

Name | Role
-- | --
Mary | Admin
Jessie | 一般user
C | 一般user

在用户获取资源前，需先对其身份(role)进行确认，所以我会定义一个叫`check_permission(user)`的function.

```py
def check_permission(user):
    """ Check whether a user has the right to access to a specific resource.
    return True if can, otherwise return False
    """
    pass
```


