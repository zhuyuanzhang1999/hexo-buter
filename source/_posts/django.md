---
title: Django简单实用方法
tags:
  - python
  - Django
id: '666'
categories:
  - - 编程语言
date: 2023-04-29 10:00:00
---

### 一个简单的Django示例的步骤
需要先安装好Django框架和相关的依赖包。我假设你已经安装好了Python和pip，并且知道如何使用虚拟环境。下面是一个简单的Django示例的步骤：

## 1. 创建一个虚拟环境，并激活它。例如，你可以使用virtualenv或venv工具，命令如下：

```bash
$ virtualenv -p python3 venv # 使用 virtualenv 命令创建一个名为 venv 的虚拟环境，指定使用 python3 作为解释器
$ source venv/bin/activate # 使用 source 命令激活该虚拟环境
```
`source` 是一个 Linux 命令，它可以在当前 shell 环境中读取并执行指定文件中的命令。它常用于加载函数、变量和配置文件到 shell 脚本中。`source` 是 Bash 和其他流行的 Linux 和 UNIX 操作系统中的 shell 内置命令，其行为可能因 shell 而异。

可以使用 `source filename [options]` 来执行 `source` 命令，也可以使用 `.`（点）代替 `source` 命令，例如：`. filename [options]`。

## 2. 安装Django框架，命令如下：

```bash
$ pip install django
```

## 3. 创建一个Django项目，命名为myblog，命令如下：

```bash
$ django-admin startproject myblog
```
这是一条用于创建一个名为 `myblog` 的 Django 项目的命令。`django-admin` 是 Django 的命令行工具，它提供了许多有用的管理命令，其中之一就是 `startproject`。该命令用于创建一个新的 Django 项目，其参数为项目名称。

## 4. 进入项目目录，创建一个Django应用，命名为blog，命令如下：

```bash
$ cd myblog
$ python manage.py startapp blog
```

## 5. 在项目目录下的settings.py文件中，注册blog应用，将'blog.apps.BlogConfig'添加到INSTALLED_APPS列表中，代码如下：

```python
INSTALLED_APPS = [
    # ...
    'blog.apps.BlogConfig',
]
```

## 6. 在blog应用目录下的models.py文件中，定义一个Post模型，表示博客的文章，代码如下：

```python
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=100) # 文章标题
    content = models.TextField() # 文章内容
    created_at = models.DateTimeField(auto_now_add=True) # 文章创建时间

    def __str__(self):
        return self.title # 返回文章标题作为对象的字符串表示
```
这是一段用于在 Django 应用中定义模型的代码。Post 类继承自 models.Model，它表示一个数据库表，用于存储博客文章。该类定义了三个字段：title、content 和 created_at，分别表示文章的标题、内容和创建时间。

title 字段是一个 CharField 类型，它表示一个字符串字段，最大长度为 100 个字符。content 字段是一个 TextField 类型，它表示一个文本字段，用于存储大量文本。created_at 字段是一个 DateTimeField 类型，它表示一个日期时间字段，其 auto_now_add 参数设置为 True，表示在创建对象时自动设置为当前时间。

此外，该类还定义了一个 __str__ 方法，它返回文章的标题作为对象的字符串表示
## 7. 在项目目录下，执行数据库迁移，创建Post模型对应的表，命令如下：



``` bash

$ python manage.py makemigrations  # 使用 manage.py 命令行工具创建数据库迁移文件
# 使用 manage.py 命令行工具应用数据库迁移
$ python manage.py migrate
```
这是两条用于在 Django 项目中创建和应用数据库迁移的命令。`manage.py` 是 Django 项目的命令行工具，它提供了许多有用的管理命令，其中之一就是 `makemigrations` 和 `migrate`。

`makemigrations` 命令用于根据模型定义创建数据库迁移文件。它会检查项目中所有应用的模型定义，并为每个应用生成一个迁移文件，用于描述模型更改。

`migrate` 命令用于应用数据库迁移。它会根据迁移文件中的指令，对数据库进行相应的更改，以便将数据库结构更新为最新状态。
## 8. 在项目目录下，创建一个超级用户，用于登录后台管理界面，命令如下：

```bash
$ python manage.py createsuperuser
```

## 9. 在blog应用目录下的admin.py文件中，注册Post模型，使其可以在后台管理界面中操作，代码如下：

```python
from django.contrib import admin
from .models import Post

admin.site.register(Post) # 注册Post模型
```

## 10. 在blog应用目录下的views.py文件中，定义一个index视图函数，用于显示所有文章的列表，代码如下：

```python
from django.shortcuts import render
from .models import Post

def index(request):
    posts = Post.objects.all() # 获取所有文章对象
    context = {'posts': posts} # 构造上下文数据
    return render(request, 'index.html', context) # 渲染模板并返回响应
```

## 11. 在blog应用目录下的urls.py文件中（如果没有则创建），定义一个URL路由规则，将根路径映射到index视图函数，代码如下：

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'), # 将根路径映射到index视图函数，并命名为index
]
```

## 12. 在项目目录下的urls.py文件中，包含blog应用的urls.py文件，将所有以'blog/'开头的路径交给blog应用处理，代码如下：

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls), # 管理后台路径
    path('blog/', include('blog.urls')), # blog应用路径
]
```

## 13. 在blog应用目录下创建一个templates目录，并在其中创建一个index.html文件，作为index视图函数的模板文件，代码如下：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>我的博客</title>
</head>
<body>
<h1>我的博客</h1>
<ul>
{% for post in posts %} <!-- 遍历所有文章对象 -->
    <li>
        <h2>{{ post.title }}</h2> <!-- 显示文章标题 -->
        <p>{{ post.content|truncatechars:100 }}</p> <!-- 显示文章内容的前100个字符 -->
        <p>{{ post.created_at|date:"Y-m-d H:i:s" }}</p> <!-- 显示文章创建时间 -->
    </li>
{% endfor %}
</ul>
</body>
</html>
```
这是一段用于在 Django 应用中定义模板的代码。它是一个 HTML 文件，其中包含了一些 Django 模板标签和过滤器，用于动态生成页面内容。

在这段代码中，{% for post in posts %} 和 {% endfor %} 之间的代码会被遍历执行，每次遍历都会取出一个 Post 对象，并将其赋值给 post 变量。在遍历过程中，可以使用 {{ post.title }}、{{ post.content }} 和 {{ post.created_at }} 来分别显示文章的标题、内容和创建时间。

此外，该模板还使用了两个过滤器：truncatechars 和 date。truncatechars:100 用于截取文章内容的前 100 个字符；date:"Y-m-d H:i:s" 用于格式化文章创建时间。
## 14. 在项目目录下，运行开发服务器，命令如下：

```bash
$ python manage.py runserver
```


- `runserver`：用于在本地启动一个开发服务器，以便在本地运行和测试 Django 项目。
- `migrate`：用于应用数据库迁移。它会根据迁移文件中的指令，对数据库进行相应的更改，以便将数据库结构更新为最新状态。
- `makemigrations`：用于根据模型定义创建数据库迁移文件。它会检查项目中所有应用的模型定义，并为每个应用生成一个迁移文件，用于描述模型更改。
- `createsuperuser`：用于创建一个超级用户账号，该账号具有所有权限，可以登录 Django 管理后台。
- `shell`：用于启动一个交互式 Python shell，可以在其中执行 Python 代码并访问 Django 项目的所有模块和变量。
- `test`：用于运行 Django 项目中的测试代码。

可以使用 `python manage.py help` 命令查看所有可用命令及其说明。


## 15. 在浏览器中，访问http://127.0.0.1:8000/admin/，输入超级用户的用户名和密码，进入后台管理界面，添加一些文章数据，：
![](/image/QQ20230505234508.png)


## 16. 在浏览器中，访问http://127.0.0.1:8000/blog/，查看博客首页的效果
![](/image/QQ20230505234342.png)
