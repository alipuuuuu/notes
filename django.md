## makemigration和migrate做了什么？
makemigration的作用是将python中的模型写下的新的schema转成一份migration文件，作为一个版本记录，可以用于回退等等的操作，此时还是一份python文件；
migrate的作用是将migration文件转成数据库可以执行SQL语言，然后交给数据库执行；
需要注意，所有的操作都是在schema，结构层面执行的，每次migrate并不会对所有的migration进行转译，只会转译那些未应用的内容，最后生成的SQL的目的是进行改动得到一个符合最新python中要求的版本的数据库。

## Question.objects为什么是objects？
objects是Question类的管理器，
对记录的操作是不需要makemigration和migrate的。

## self.client是什么？
self.client是TestCase类中的一个属性（方法），
client中包含get等等方法来实现用户的操作，在views level来测试网页代码。

代码：
response=self.client.get(reverse("polls:index"))
response.context["latest_question_list"]
## 为什么会返回一个QuerySet，QuerySet中包含了什么，是什么类型？
因为在views文件中写的类视图中包含了查询方法，这个查询方法得到的结果也就是QuerySet，会作为context传给对应的模板，类试图中包含了一个context_object_name，这个变量就是这个context也就是QuerySet的名称；
QuerySet有一个重要的特点就是它是一个延迟执行的包含了所有的当前Question类的对象的一个集合。

## Question.objects.filter(pub_date__lte=timezone.now())的pub_date__lte是什么意思？
这是Django ORM 的查询表达式（lookup），表达的意思是发布日期less than or equal，小于或等于，可以用这个方法实现查询不到到未来的数据。

## 子类中的方法__str__是什么意思，做了什么？
这是方法复写，override，当这个类被作为一个字符串进行操作时，就会调用这个方法。

>>> from django.test.utils import setup_test_environment
>>> setup_test_environment()
setup_test_environment() installs a template renderer which will allow us to examine some additional attributes on responses such as response.context that otherwise wouldn’t be available. 
## setup_test_environment()的作用
安装了一个模板渲染器，用以我们访问检查responses传过来的属性，比如content或context

# 精简版：
Django ORM & Testing Notes

makemigrations:
- 根据 models 变化生成迁移脚本（Python）
- 记录 schema 变更历史

migrate:
- 执行未应用的 migration
- 转换为 SQL 并更新数据库结构

Manager:
- Question.objects 是类级管理器（表操作）
- instance.save() 是行操作

TestCase:
- self.client = 内置测试浏览器

QuerySet:
- 惰性执行
- 包含模型实例
- 迭代时查询数据库

Lookup:
- field__lte = <=
- 过滤未来数据

__str__:
- 定义对象的可读字符串表示


