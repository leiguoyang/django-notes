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
