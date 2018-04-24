# django
MVC(model, view, controller)</br>
MVC框架的核心:解耦</br>
降低各功能模块之间的耦合性，方便变更，更容易重构代码，最大程度上实现代码的重用</br>
model：数据库层的封装</br>
view：向用户展示结果</br>
controller：处理请求，获取数据，返回结果</br>

MVT(modle, view, template)</br>
mvt中的vt相当于mvc中的cv</br>
B/S 浏览器/服务器</br>
C/S 客服端/服务器</br>

安装虚拟环境
```
pip install virtualenv
```
在env文件夹中安装虚拟环境</br>
```
cd env
virtualenv --no-site-packages testenv(如果版本只有一个3.x的)、
virtualenv --no-site-packages -p 路径 testenv(指定安装的版本)
```

进入虚拟环境
```
cd testenv\Scripts>activate
```
现在就可以安装我们需要的库了</br>
退出虚拟环境
```
deactivate 
```
安装django
```
pip install django==1.11
```
创建项目
```
django-admin startproject 名称
```
修改setting里面的编码
```
LANGUAGE_CODE = 'zh-hans' 
```
运行项目 启动服务器
```
python manage.py runserver 
```
启动djingo项目
```
python manage.py runserver ip:端口
```
初始化配置
```
__init__.py 初始化，配置pymysql链接的地方
setting.py 配置信息位置，databases等
urls.py url路由
wsgi.py 网关
```

创建app 
```
python manage.py startapp app名字
```
配置
```
在setting.py文件中installed_app中写入app的name
```
模型model
```
在models.py文件中定义class模型名称
继承models.Model
db_tables:定义数据库中的表名称
```
app
```
__init__.py:初始化
admin.py:管理后台注册模型
apps.py: settings.py里面注册app的时候需要使用到。一般不推荐这样使用
from app.apps import AppConfig
AppConfig.name
models.py:写模型的地方
views.py:写处理业务逻辑的地方
```
迁移数据库
```
python manage.py makemigrations
python manage.py migrate
```
保持数据
```
stu = Student()
stu.name = 'xxx'
stu.save()
```
生成映射文件
```
makemigrations
```
执行映射文件
```
migrate 
```
model操作
```
将settings.py中的
DATABASES={
         #链接数据库
         'default':{
         'ENGINE': 'django.db.backends.mysql',
        	'HOST': '阿里云服务器的公网地址',
        	'USER': 'root',
        	'PASSWORD': '123456',
        	'PORT': '3306',
        	'NAME': 'firsthello',
         }
}
```
创建超级管理员的账号密码
```
python manage.py createsuperuser
```
admin.py
```
# -*- coding:utf-8 -*-
from django.contrib import admin

# Register your models here.
from stu.models import Student

# 第二种注册方式
@admin.register(Student)
class StudentAdmin(admin.ModelAdmin):

    def set_sex(self):
        if self.sex:
            return '男'
        else:
            return '女'
    # 修改描述
    set_sex.short_description = '性别'
    # 展示字段
    list_display = ['id','name',set_sex]
    # 过滤
    list_filter = ['name']
    # 搜索
    search_fields = ['name']
    # 分页
    list_per_page = 3
# 1. 注册的第一种方式
# admin.site.register(Student,StudentAdmin)
```
