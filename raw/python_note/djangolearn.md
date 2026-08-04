## Shell里面一些命令
创建一个django项目
```
django-admin startproject projectname
```
在 Django 项目创建完成后，你可以使用 django-admin startapp 命令在项目的根目录下创建一个新的应用。例如，如果你想创建一个名为 app 的应用，你可以在 lyricslab 项目的根目录下执行：
```
python manage.py startapp app
```
运行：
```python manage.py runserver # 启动```

其他
```
python manage.py createsuperuser # 创建admin用户

python manage.py makemigrations #生成迁移文件
或
python manage.py makemigrations your_app_name

python manage.py migrate #迁移到数据库

```

## 1. model部分
改变模型需要这三步：
1. 编辑 models.py 文件，改变模型。
2. 运行 python manage.py makemigrations 为模型的改变生成迁移文件。
3. 运行 python manage.py migrate 来应用数据库迁移。

## 2. view部分
Django模板语法：
```
view（py文件）：｛"HTML变量名" : "views变量名"｝
HTML：｛｛变量名｝｝
```

render(): 载入模板，填充上下文，再返回由它生成的 HttpResponse 对象
get_object_or_404(): 尝试用 get() 函数获取一个对象，如果不存在就抛出 Http404 错误

request.POST 是一个类字典对象，让你可以通过关键字的名字获取提交的数据。 这个例子中， request.POST['choice'] 以字符串形式返回选择的 Choice 的 ID。 request.POST 的值永远是字符串。

通用视图 DetailView 使用一个叫做 <app name>/<model name>_detail.html 的模板。
类似地，ListView 使用一个叫做 <app name>/<model name>_list.html 的默认模板