# Django学习笔记
## 安装Django
`pip install django`
## 查看django版本
`python -m django --version`
## django-admin 和 manage . py
django admin 是 Django 用于管理任务的命令行实用程序。
此外，manage . py 会在每个 Django 项目中自动创建。它做的事情和 django-admin 一样，但也设置了 DJANGO_SETTINGS_MODULE 环境变量，使其指向你的项目的 settings . py 文件。

### 创建项目
在当前目录或给定的目标目录中为给定的项目名称创建一个 Django 项目目录结构。
#### 基本语法
`django-admin startproject name [directory]`

### 启动自带的简易服务器
在本地机器上启动一个轻量级的开发 Web 服务器。默认情况下，该服务器在 IP 地址 127.0.0.1 的 8000 端口上运行。你可以明确地传递一个 IP 地址和端口号。

用于开发的服务器在需要的情况下会对每一次的访问请求重新载入一遍 Python 代码。所以你不需要为了让修改的代码生效而频繁的重新启动服务器。然而，一些动作，比如添加新文件，将不会触发自动重新加载，这时你得自己手动重启服务器。
#### 基本语法
`python manage.py runserver [addrport]`

### 创建应用
在当前目录或给定的目标目录中为给定的应用名创建一个 Django 应用目录结构。
#### 基本语法
`python manage.py startapp name [directory]`
### 迁移
迁移是 Django 将你对模型的修改（例如增加一个字段，删除一个模型）应用至数据库架构中的方式。
#### 基于模型的修改创建迁移
##### 基本语法
`python manage.py makemigrations [app_label [app_label ...]]`
#### 应用和撤销迁移
##### 基本语法
`python manage.py migrate [app_label] [migration_name]`
##### 选项
`--database DATABASE`：指定要迁移的数据库。默认值为 default。
#### 展示迁移使用的 SQL 语句
打印指定迁移的 SQL。这需要一个活动的数据库连接，它将用来解析约束名；这意味着你必须针对你希望以后应用它的数据库副本生成 SQL。
##### 基本语法
`python manage.py sqlmigrate app_label migration_name`
##### 选项
`--database DATABASE`：指定要生成的数据库。默认值为 default。
#### 列出项目的迁移和迁移的状态
显示一个项目中的所有迁移。
##### 基本语法
`python manage.py showmigrations [app_label [app_label ...]]`



## 管理静态文件
网站通常需要提供类似图片，JavaScript 或 CSS 的额外文件服务。在 Django 中，我们将这些文件称为“静态文件”。Django 提供了 django.contrib.staticfiles 帮你管理它们。
### 配置静态文件
1. 确保 INSTALLED_APPS 包含了 django.contrib.staticfiles。
2. 在配置文件中，定义 STATIC_URL：

   ```python
   STATIC_URL = '/static/'
   ```

3. 在模板中，用 static 模板标签基于配置   STATICFILES_STORAGE 位给定的相对路径构建 URL：
   ```html
   {% load static %}
   <img src="{% static 'my_app/example.jpg' %}" alt="My image">
   ```
4. 将你的静态文件保存至程序中名为 static 的目录中。例如 my_app/static/my_app/example.jpg。

## 模型
模型准确且唯一的描述了数据。它包含您储存的数据的重要字段和行为。一般来说，每一个模型都映射一张数据库表。
### 基础：

- 每个模型都是一个 Python 的类，这些类继承 django.db.models.Model
- 模型类的每个属性都相当于一个数据库的字段。
- 利用这些，Django 提供了一个自动生成访问数据库的 API
### 字段
模型中最重要且唯一必要的是数据库的字段定义。字段在类属性中定义。定义字段名时应小心避免使用与 模型 API 冲突的名称， 如 clean, save, or delete 等.
#### 字段类型
模型中每一个字段都应该是某个 Field 类的实例， Django 利用这些字段类来实现以下功能：

字段类型用以指定数据库数据类型（如：INTEGER, VARCHAR, TEXT）。
在渲染表单字段时默认使用的 HTML 视图 (如： `<input type="text">, <select>`)。
基本的有效性验证功能，用于 Django 后台和自动生成的表单。
Django 内置了数十种字段类型；你可以在 模型字段参考 中看到完整列表。如果 Django 内置类型不能满足你的需求，你可以很轻松地编写自定义的字段类型。
### 示例

### 在一个包中管理模型
manage.py startapp 命令创建了一个应用结构，包含一个 models.py 文件。若你有很多 models.py 文件，用独立的文件管理它们会很实用。

为了达到此目的，创建一个 models 包。删除 models.py，创建一个 myapp/models 目录，包含一个 __init__.py 文件和存储模型的文件。你必须在 __init__.py 文件中导入这些模块。

比如，若你在 models 目录下有 organic.py 和 synthetic.py：

myapp/models/__init__.py:
```python 
from .organic import Person
from .synthetic import Robot
```
显式导入每个模块，而不是使用 from .models import * 有助于不打乱命名空间，使代码更具可读性，让代码分析工具更有用。

### 执行查询
一旦创建 数据模型 后，Django 自动给予你一套数据库抽象 API，允许你创建，检索，更新和删除对象。

#### 创建对象
为了用 Python 对象展示数据表对象，Django 使用了一套直观的系统：一个模型类代表一张数据表，一个模型类的实例代表数据库表中的一行记录。

要创建一个对象，用关键字参数初始化它，然后调用 save() 将其存入数据库。
##### 示例
```python
from blog.models import Blog
b = Blog(name='Beatles Blog', tagline='All the latest Beatles news.')
b.save()
```
这在幕后执行了 INSERT SQL 语句。Django 在你显式调用 save() 才操作数据库。

save() 方法没有返回值。

#### 将修改保存至对象
要将修改保存至数据库中已有的某个对象，使用 save()。
##### 示例
有一个已被存入数据库中的 Blog 实例 b5，本例将其改名，并在数据库中更新其记录:
```python
b5.name = 'New name'
b5.save()
```
这在幕后执行了 UPDATE SQL 语句。Django 在你显示调用 save() 后才操作数据库。

#### field查找
字段查找是指定 SQL WHERE 子句的方法。它们被指定为 QuerySet 方法 filter()、exclude() 和 get() 的关键字参数。

Django 的内置查找功能如下。也可以为模型字段写 自定义查找。

为方便起见，当没有提供查找类型时（如 Entry.objects.get(id=14)），查找类型被假定为 exact。

##### exact
完全匹配。如果提供的比较值是 None，它将被解释为 SQL NULL （详见 isnull）。
##### iexact
不区分大小写的完全匹配。如果提供的比较值是 None，它将被解释为 SQL NULL （详见 isnull）。
##### contains
区分大小写的包含测试。
##### icontains
不区分大小写的包含测试。
##### in
在一个给定的可迭代对象中；通常是一个列表、元组或**查询集**。这不是一个常见的用例，但字符串（可迭代）是可以接受的。
###### 性能考量
谨慎使用嵌套查询，了解你的数据库服务器的性能特点（如果有疑问，请做基准测试！）。一些数据库后端，最主要的是 MySQL，并不能很好地优化嵌套查询。在这些情况下，提取一个值的列表，然后将其传递到第二个查询中会更有效率。也就是说，执行两个查询而不是一个查询：
```python
values = Blog.objects.filter(
        name__contains='Cheddar').values_list('pk', flat=True)
entries = Entry.objects.filter(blog__in=list(values))
```
注意 Blog QuerySet 周围的 list() 调用，以强制执行第一个查询。如果没有它，一个嵌套查询就会被执行，因为 QuerySet 是惰性的。
##### gt
大于。
##### gte
大于等于。
##### lt
小于。
##### lte
小于等于
##### startswith
区分大小写的开头为。
##### istartswith
不区分大小写的开头为。
##### endswith
区分大小写的结尾为。
##### iendswith
不区分大小写的结尾为。
##### range
范围测试（含）。
###### 举例：
```python
import datetime
start_date = datetime.date(2005, 1, 1)
end_date = datetime.date(2005, 3, 31)
Entry.objects.filter(pub_date__range=(start_date, end_date))
```
在 SQL 中，你可以在任何你可以使用 BETWEEN 的地方使用 range——用于日期、数字甚至字符。
###### 警告
用日期过滤 DateTimeField 不会包括最后一天的项目，因为界限被解释为“给定日期的 0 点”。一般来说，你不能把日期和日期时间混在一起。

##### date
对于日期时间字段，将值投射为日期。允许链接其他字段的查找。取一个日期值。

当 USE_TZ 为 True 时，字段在过滤前会被转换为当前时区。这需要 数据库中的时区定义。
###### 举例
```python
Entry.objects.filter(pub_date__date=datetime.date(2005, 1, 1))
Entry.objects.filter(pub_date__date__gt=datetime.date(2005, 1, 1))
```

##### year
对于日期和日期时间字段，精确匹配年份。允许链接其他字段的查询。取整数年。
###### 举例
```python
Entry.objects.filter(pub_date__year=2005)
Entry.objects.filter(pub_date__year__gte=2005)
```

##### month
对于日期和日期时间字段，精确的月份匹配。允许链接其他字段的查询。取整数 1（1 月）到 12（12 月）。
###### 举例
```python
Entry.objects.filter(pub_date__month=12)
Entry.objects.filter(pub_date__month__gte=6)
```
##### day
对于日期和日期时间字段，精确匹配日期。允许链接其他字段的查询。取整数日。
##### time
对于日期时间字段，将其值强制转换为时间。允许链式附加字段查找。取一个 datetime.time 的值。
##### regex
区分大小写的正则表达式匹配。

正则表达式语法是使用中的数据库后端的语法。对于没有内置正则表达式支持的 SQLite 来说，这个功能是由（Python）用户定义的 REGEXP 函数提供的，因此正则表达式语法是 Python 的 re 模块的语法。

##### iregex
不区分大小写的正则表达式匹配。