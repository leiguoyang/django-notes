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

## Day 5 (Jul 13, 2021)

今天看了authentication这一章，感觉还是云里雾里的。^_^

设计model field时一定要严谨，一方面是合理利用database，减少不必要的浪费。看了下Heroku提供的Postgres database的价格，最便宜的也要$50/month，容量才64GB，太贵了。1TB的要$1400/month。

## Many to many relationship (Jul 20, 2021)

今天学习model中[many to many relationship](https://docs.djangoproject.com/en/3.2/topics/db/models/#extra-fields-on-many-to-many-relationships)这一部分，突然懂了好多东西。其实可以先不谈many to many relationship这种概念或它所调用的API。先从最基础的表谈起，有些表和表之间本身就存在这种many to many的关系。比如其官网举的例子。

```py
from django.db import models

class Person(models.Model):
    name = models.CharField(max_length=128)

    def __str__(self):
        return self.name

class Group(models.Model):
    name = models.CharField(max_length=128)
    members = models.ManyToManyField(Person, through='Membership')

    def __str__(self):
        return self.name

class Membership(models.Model):
    person = models.ForeignKey(Person, on_delete=models.CASCADE)
    group = models.ForeignKey(Group, on_delete=models.CASCADE)
    date_joined = models.DateField()
    invite_reason = models.CharField(max_length=64)
```

这里会涉及两个对象，`Person` and `Group`，一个用户可以属于多个不同的Group，而一个Group也可以有多个不同的成员，也就是所谓的mang to many relationship。实际在database里面会有这样三个表，

- `persons`
- `groups`
- `memberships`

`memberships`这个表其实是用来记录哪个用户什么时候加入什么组别之类的这些信息。

id | person_id | group_id | date_joined | invite_reason
-- | -- | -- | -- | --

再比如一个订单系统，其中会有这样三个表。

`users`
`products`
`orders`

`orders`这个表是用来记录哪个客户什么时候买了多少数量的产品。

id | user_id | product_id | quantity | purchase_datetime
-- | -- | -- | -- | --

其实刚才谈的这两个案例，无论是加入群组也好还是下订单，其实抽象出来逻辑都一样，也就是所有的东西其实都是假的，只是名字不同而已。突然豁然开朗^_^。












