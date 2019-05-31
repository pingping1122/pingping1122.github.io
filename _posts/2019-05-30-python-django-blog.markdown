---
layout: post
title:  "使用Python框架Django搭建简易博客!"
date:   2019-05-30 10:50:08 +0800
categories: jekyll update
---

* [本文基于慕课网咚咚呛老师的三小时入门Django框架课程](https://www.imooc.com/learn/1110)
* [github本项目地址](https://github.com/pingping1122/DjangoProjects)

* 本文主要知识点：
![本文主要内容](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/summary.png)

* 最终效果展示：

![blog首页](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/blog_index_result.png)

![blog详情页](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/blog_detail_result.png)


* Python安装框架Django安装
* Django(MVC)--django_seed项目
* Django视图与模型--blog应用

### 一、Python安装框架Django安装
* (1)[python安装下载地址](https://www.python.org/)   ----推荐安装Python3
* (2)Win+R---cmd---python查看版本---说明已安装成功
* (3)配置系统变量---系统变量中增加python路径
* (4)可有选择的安装Anaconda---要与python版本一样
* (5)使用python的包安装工具pip安装django>2.0
    
    ![安装流程图](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/pip_install_django.png)

因为我的电脑有两个版本的python，所以此处需指定python版本(python在我的电脑上代表python3)

    python -m pip install --upgrade pip  // 安装pip
    python -m pip install django         // 安装django
    django-admin // 查看django是否安装成功

* IDE:pyCharm(community)
安装之后需要设置python解释器的版本--两种方法：
(1)设置全局解释器： configure-setting--Project Interpreter---解释器版本
(2)设置项目解释器file--setting--Project Interpreter ---选择指定项目的python解释器版本

### 二、Django(MVC)项目

#### (1).django命令
   win+r--cmd---（django-admin）查看django命令

   ![django常用命令1](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/django_command_01.png)

   ![django常用命令2](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/django_command_02.png)

#### (2).创建django项目

 * 此处注意项目位置，到项目所在目录下边执行 django-admin startproject django_seed  创建一个名为django_seed的项目

 ![创建django项目django_seed](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/create_django_project.png)

项目目录介绍

      manage.py     // 项目管理文件
      django_seed/setting.py  // 配置文件
      django_seed/urls.py  // 项目路由文件
      django_seed/wsgi.py  
      django_seed/_init_.py 


#### (3). 创建应用

应用目录分析

     python manage.py  startapp blog // 创建项目下的blog应用
     blog/views.py  // 视图---产生内容
     blog/models.py // 定义应用模型的地方
     blog/admin.py // 定义admin模块管理对象的地方
     blog/ app.py  // 声明应用的地方
     blog/urls.py // 管理应用路由的地方


 ![创建django应用blog](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/create_django_app.png)

#### (4). python项目与应用关系----项目与应用是多对多的关系

 ![多对多](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/project_vs_app_01.png)

 ![区别1](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/project_vs_app_02.png)

  ![区别2](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/project_vs_app_03.png)

#### (5).django_seed项目运行

    python manage.py runserver
    
![运行django_seed项目](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/run_django_seed.png)


#### (6). blog应用执行

在django_seed/settings.py 增加应用配置

     INSTALLED_APPS = [
     'django.contrib.admin',
     'django.contrib.auth',
     'django.contrib.contenttypes',
     'django.contrib.sessions',
     'django.contrib.messages',
     'django.contrib.staticfiles',
     # myapp--blog
     'blog.apps.BlogConfig',
     ] 

在django_seed/urls.py增加应用路由---如果路由中有blog，则跳转至blog下的路由

      from django.urls import path,include
      urlpatterns = [
          path('admin/', admin.site.urls),
          path('blog/', include('blog.urls')),
       ]

在blog/urls.py中配置路由---绑定视图函数和Url

      from django.urls import path, include
      import blog.views
      urlpatterns = [
           path('hello_world', blog.views.hello_world)
           ]

在blog/views.py中定义hello_world视图函数，返回hello_world字符串(HttpResponse)

          from django.http import HttpResponse
          def hello_world(request):
              return HttpResponse("Hello World!")


运行 python manage.py runserver
    
![效果](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/run_blog_hello_world.png)              

#### (7).应用分析
![helloworld分析](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/helloworld.png)              



### 三、Django视图与模型---blog应用

#### (1).模型定义

blog/models.py代码：

    class Article(models.Model):
    # 文章ID
    article_id=models.AutoField(primary_key=True)
    # 文章标题
    article_title=models.TextField()
    # 文章摘要
    brief_content=models.TextField()
    # 文章内容
    content = models.TextField()
    # 文章发布日期
    publish_date=models.DateTimeField(auto_now=True)
    # 注：函数前后两个下划线
    def __str__(self):
        return self.article_title

#### (2).模型的迁移

     python manage.py makemigrations   // 将模型的变更生成迁移文件
     python manage.py migrate         // 运行迁移文件，将迁移文件内容同步到数据库

#### (3)django shell

     python shell---交互式的pythonb编程
     django shell---上类似，且继承Django项目环境

使用django shell 新建一篇文章

     python manage.py shell // 进入django shell环境
     from blog.models import Article  // 引入文章模型
     a = Article()   // 新建文章
     a.article_title='xxx' // 添加文章具体内容
     a.brief_content='tttt'
     a.content='dddd'
     print(a) // 打印出文章a  ----Article object(None)
     a.save()    //将新建的文章a保存到数据库！！！
     articles=Article.objects.all()  // 把数据库中所有文章查询出来
     article= articles[0]
     print(article.content) // 打印文章内容，确认添加数据库成功  

#### (4)django admin--django后台管理工具---自动生成，读取定义的模型元数据

     python manage.py createsuperuser   // 创建管理员用户--填写用户名和密码
     username:
     password:
     password_again:

     python manage.py runserver  
     浏览器打开localhost:8000/admin     // 登陆页面进行管理 

![效果图](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/django_admin.png)      

发现没有刚才创建的博客模型,需要将模型注册到admin里面，才能在admin后台看到。在blog/admin.py中添加

     # 需要注册到admin里才能在admin后台看到
    from .models import Article
    admin.site.register(Article)

在blog/models.py中补充代码--用于在后台看到的是文章名区分各文章

    # 注：函数前后两个下划线
    def __str__(self):
        return self.article_title

#### (5).博客数据返回页面

blog/views.py中添加

    from blog.models import Article
    def article_content(request):
    article = Article.objects.all()[0]
    article_title = article.article_title
    brief_content = article.brief_content
    content = article.content
    article_id = article.article_id
    publish_date = article.publish_date
    return_str = 'article_title:%s,brief_content:%s,' \
                 'content:%s,article_id:%s,publish_date:%s' % (
                 article_title, brief_content, content, article_id, publish_date)
    return HttpResponse(return_str)

配置路由blog/urls.py

     urlpatterns = [
    path('hello_world', blog.views.hello_world),
    path('content', blog.views.article_content)  // 文章内容显示路由 
    ]

    python  manage.py runserver
    浏览器中打开 localhost:8000/blog/content  ---就可以看到文章内容

#### (6). blog开发

* django模板系统

变量
![变量](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/django_model_variable.png)  

for标签
![for](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/django_model_for.png) 

if-else标签
![if-else](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/python_django_blog/django_model_if_else.png) 

* 定义博客主页和详情页blog/template/index.html 、和blog/template/detail.html

* 同时使用blog/tool/import_data.py想django数据库导入blog/data中文章数据

* 再配置urls和views添加相应路由和视图函数


    打开localhost:8000/blog/index 查看blog首页
        localhost:8000/blog/detail 查看detail详情页

* 文章首页-->文章详情页面的跳转---url路径参数的获取和传递

blog/urls.py中修改路由---加上article_id

      urlpatterns = [
         path('hello_world', blog.views.hello_world),
         path('content', blog.views.article_content),
         path('index', blog.views.get_index_page),
         # path('detail', blog.views.get_detail_page),
         path('detail/<int:article_id>', blog.views.get_detail_page),
      ]

再blog/views.py中可以获取到article_id

     def get_detail_page(request, article_id):
       all_article = Article.objects.all()
       cur_article = None
       for article in all_article:
         if article.article_id == article_id:
            cur_article = article
            break
       section_list = cur_article.content.split('\n')
       # 自动搜索templates下边的blog/detail.html
       return render(request, 'blog/detail.html', {
         'cur_article': cur_article,
         'section_list': section_list
    })

在index.html中添加跳转路由

     <h4><a href="/blog/detail/{{article.article_id}}">{{article.article_title}}</a></h4>

* django分页组件

django Paginator使用

      # 1、导入分页组件Paginator
     from django.core.paginator import Paginator
      # 2、创建分页对象，通过该对象来调用分页的所有属性 ，
     paginator = Paginator(all_article, 3)  # 设置每页显示几条，此处为3条
     page_num = paginator.num_pages  # page_nums 分页数量
     page_article_list = paginator.page(page)  # 到指定页取值







