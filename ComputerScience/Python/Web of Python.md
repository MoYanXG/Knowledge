# 虚拟环境

在项目目录下，打开cmd
```
python -m venv 环境名称
```

## 激活&停止虚拟环境

### Windows:
```cmd
环境名称\Scripts\activate
```

### Linux
```
source 环境名称/bin/activate
```

### 停止
```
deactivate
```

# Django配置
## 安装Django
```cmd
pip install django
```

## Django中创建项目
```cmd
django-admin startproject learning_log . # 项目名称
```
注意最后有个点
创建了一个与项目名称相同的目录
目录中包含manage.py
该程序用于接受命令并将其交给Django的相关部分运行

```cmd
django-admin startproject projectname
```
无点，则创建 projectname 目录
内含 同名目录 和 manage.py
要执行之后的操作，则需要
```cmd
cd projectname
```

## 创建数据库
```cmd
python manage.py migrate
```
创建了一个文件db.sqlite3
修改数据库称为迁移(migrate)数据库

## 查看项目
```cmd
python manage.py runserver
```
启动了一个名为development server的服务器
使用浏览器输入 http://localhost:8000/
可看到网页
### 启动服务器失败

可能为8000端口被占用
```
python manage.py runserver 8080 # 修改端口
```

### 关闭服务器
在runserver的终端窗口中 Ctrl + C 

# 创建应用程序
在manage.py所在的目录打开cmd并激活虚拟环境(runserver要在另一窗口打开)
```cmd
python manage.py startapp learning_logs # 应用程序名
```
新增与程序名称同名文件夹
文件夹下创建了models.py、admin.py、views.py

## 应用程序目录下，各文件的用处

**_init.py_** 是一个空文件，作用同前。

**admin.py**文件跟网站的后台管理相关。

**models.py**文件跟数据库操作相关。主要用一个 Python 类来描述数据表。运用这个类,你可以通过简单的 Python 的代码来创建、检索、更新、删除 数据库中的记录而无需写一条又一条的SQL语句。

**views.py** 包含了页面的业务逻辑，接收浏览器请求，进行处理，返回页面操作相关。

**tests.py**文件用于开发测试用例，在实际开发中会有专门的测试人员使用。

**apps.py**文件是django1.10之后增加的，通常里面包含对应用的配置。

**migrations**是django 1.8之后推出的migrations机制，使django数据模式管理更容易。

migrations机制有两个指令，makemigrations和migrate。makemigrations指令是用models里面的model和当前的migrations代码里面的model做对比，如果有新的修改，就生成新migrations代码。migrate指令是用migrations目录中代码文件和django数据库django_migrations表中的代码文件做对比，如果表中没有，那就对没有的文件按顺序及依赖关系做migrate apply，然后再把代码文件名加进migrations表中。在目录中自动生成了_init_.py文件

## 定义模型
模型就是一个类，包含属性和方法

打开models.py
```
from django.db import models  
  
class Topic(models.Model):  
    """用户学习的主题"""  
    text = models.CharField(max_length=200)  
    date_added = models.DateTimeField(auto_now_add=True)  
  
    def __str__(self):  
        """返回模型的字符串表示。"""  
        return self.text
```
新建了Topic类，继承了Model
	*Model* --> Django中定义了模型基本功能的类
添加了两个属性
	*text* --> 是一个CharField(由字符组成的数据，即文本)
		定义CharField 属性时，必须告诉Django该在数据库中预留多少空间
	这里将*max_length*设置成了200(200字符)
	*date_added* --> 是一个DateTimeField(记录日期和时间的数据)
		传递了实参auto_now_add=True
			用户创建新主题时，会自动将该属性设置成当前时间

方法__str__() ，它返回存储在 *属性text* 中的字符串

### 模型中使用字段查询

参阅 Django Model Field Reference

## 激活模型

打开 settings.py(在项目文件夹中)

将 INSTALLED_APPS 修改如下
```
INSTALLED_APPS = [  
    # 我的应用程序  
    'learning_logs',  # 应用程序名
  
    # 默认添加的应用程序  
    'django.contrib.admin',  
    'django.contrib.auth',  
    'django.contrib.contenttypes',  
    'django.contrib.sessions',  
    'django.contrib.messages',  
    'django.contrib.staticfiles',  
]
```
务必将自己创建的应用程序放在默认应用程序前面，这样能够覆盖默认应用程序的行为

然后修改数据库,以存储与模型Topic相关的信息
```cmd
python manage.py makemigrations learning_logs # 应用程序名
```
命令 **makemigrations** 
	--> 让Django确定该如何修改数据库，使其能够存储与前面定义的新模型相关联的数据

迁移，让Django来修改数据库
```cmd
python manage.py migrate
```
检查 Running migrations: 下是否迁移正常

## 合并数据库
当修改了Django模型后，需要运行以下命令，将更改应用到数据库中

```cmd
python manage.py makemigrations
```
 这个命令用于生成迁移脚本。当你更新了模型文件之后，需要运行该命令，Django会检测模型的改变，然后自动生成相应的迁移脚本，存储在 `migrations/`  目录下。通常来说，你需要针对每个应用运行一次该命令

```cmd
python manage.py migrate
```
 这个命令用于将迁移脚本应用到数据库中。当你在模型文件中进行更改之后，需要先通过`makemigrations`命令生成迁移脚本，然后运行该命令将这些脚本应用到数据库中。对于新的迁移脚本，Django会逐个执行它们，从而更新数据库结构。对于已经执行过的脚本，Django会跳过它们，避免重复执行

## Django管理网站

### 创建超级用户
```cmd
python manage.py createsuperuser
```

Django并不存储你输入的密码，而是存储从该密码派生出来的一个字符串，称为**散列值**

### 向管理网站注册模型

打开admin.py (应用程序目录下)

为注册Topic，如下输入
```python
# 导入模型
from .models import Topic 
# 让Django通过管理网站来管理模型
admin.site.register(Topic)
```

访问：http://localhost:8000/admin/
登录即可看到网站内容

### 添加主题

单击Topics后单击add，随便输入点东西，单击Save，就完成主题的添加了

## 定义模型Entry

**多对一关系** 
	多个条目可关联到同一个主题

打开models.py，添加模型Entry代码
```python
class Entry(models.Model):  
    """学到的有关某个主题的具体知识"""  
    topic = models.ForeignKey(Topic, on_delete=models.CASCADE)  
    text = models.TextField()  
    date_added = models.DateTimeField(auto_now_add=True)  
  
    class Meta:  
        verbose_name_plural = 'entries'  
  
    def __str__(self):  
        if len(self.text) > 50:  
            return f"{self.text[:50]}..."  
        else:  
            return f"{self.text[:]}"
```

属性 **topic**
	**ForeignKey** 实例
		外键(foreign key)是一个数据库术语，它指向数据库中的另一条记录，这里是将每个条目关联到特定主题
实参 **on_delete=models.CASCADE**
	级联删除
		删除主题的同时删除所有与之相关联的条目
属性 **text**
	**TextField** 实例
属性 **date_added**
	能够按创建顺序呈现条目，并在每个条目旁边放置时间戳
类 **Meta**
	嵌套在Entry 类中
		存储用于管理模型的额外信息
			此处设置为Django在需要时使用Entries 来表示多个条目
			如果没设置这个类，Django将使用Entrys 来表示多个条目
方法 **__str__()**
	控制Django 呈现条目时显示的信息
		超过50字符时，只显示text 前50个字符和省略号
		少于50字符时，显示完全

## 迁移模型Entry

添加了一个新模型，需要再次迁移数据库
```cmd
python manage.py makemigrations learning_logs # 应用程序名
python manage.py migrate
```

## 管理网站注册Entry

新模型需要注册
打开 admin.py，修改如下
```python
from django.contrib import admin  
  
from .models import Topic, Entry  """导入Entry"""
  
admin.site.register(Topic)  
admin.site.register(Entry)  """将Entry可通过管理网站管理"""
```

## Django shell

输入部分数据后，可以通过终端以编程方式来查看数据
这种交互式环境称为**Django shell**
用于*测试项目和排除故障*

在虚拟环境中，执行命令
```
python manage.py shell
```
启动解释器

导入模块的模型并获取模型中的所有实例
```
from learning_logs.models import Topic
Topic.objects.all()
```
返回一个被称为 **查询集(queryset)** 的列表

可遍历查询集来获取分配给主题对象的ID
```
topics = Topic.objects.all()
for topic in topics:
	print(topic.id, topic)
```

知道ID后可以通过方法
```
Topic.objects.get() # 括号内为id
# 例：
t = Topic.objects.get(id=1) 
```
来获取该对象

由于模型Entry 中属性topic 是个ForeignKey，可以获取与其相关联的所有条目
```
t.entry_set.all()
```
用外键来获取数据，可用 **相关模型小写名称_set** 的方法来获取

### 注意
每次修改模型后，都要重启shell
退出shell，Linux按 Ctrl + D，Windows按 Ctrl + Z 再按回车键
# 创建页面

Django创作页面有三个部分：
	定义URL
	编写视图
	编写模板
每个URL都被映射到特定的**视图**（视图函数获取并处理页面所需的数据） 
视图函数使用**模板**来渲染页面
模板定义页面的总体结构

## 映射URL
用户通过在浏览器中输入URL以及单击链接来请求页面

打开项目主文件夹中与项目同名文件夹中的 **urls.py** 
```python
from django.contrib import admin
from django.urls import path
"""前两行导入了一个模块和一个函数，以便对管理网站的URL进行管理"""

urlpatterns = [ """针对整个项目的urls.py文件中，该变量包含项目中应用程序的URL"""
	path('admin/', admin.site.urls), """定义了可在管理网站中请求的所有URL"""
]
```
由于需要包含 应用程序名 的URL，改为
```python
from django.contrib import admin
from django.urls import path, include """记得添加导入函数"""

urlpatterns = [ 
	path('admin/', admin.site.urls),
	path('', include('learning_logs.urls')), """应用程序名.urls"""
]
```

默认的**urls.py** 在文件夹 *项目同名文件* 中，添加了 应用程序名.urls 后需要在 *应用程序同名文件夹* 中创建一个**urls.py** 文件
新建**urls.py** 更改如下
```python
"""定义learning_logs的URL模式"""

from django.urls import path """导入path函数，使用path将URL映射到视图"""

from . import views """导入模块views，句点可从当前urls.py所在文件夹导入views.py"""

app_name = 'learning_logs' """同其他应用程序中同名文件区分"""
urlpatterns = [ """是个列表"""
	# 主页
	path('', views.index, name='index'), 
	"""第一个实参：忽略基础URL(http://localhost:端口)后剩余的URL，空字符与基础URL匹配"""
	"""第二个实参：指定调用views中的特定函数，请求的URL与前面的匹配后调用"""
	"""第三个实参：将此URL模式的名称指定为index，每当需要提供这个主页的链接，都使用这个名字"""
]
```
由于同名文件会很多，建议在第一行加上一串字符串来辨认

## 视图的编写

*应用程序名文件夹* 中的文件views.py 
```python
from django.shortcuts import render


```
render():
	根据视图提供的数据渲染响应

更改为
```python
from django.shortcuts import render

def index(request):
	"""主页"""
	return render(request, 'learning_logs/index.html') """应用程序名/index.html"""
```

## 编写模板
模板定义页面的外观，而每当页面被请求时，Django将填入相关的数据

*应用程序名文件夹* 中新建文件夹 templates (不确定是否一定要这个名字)
文件夹templates 中新建文件夹，并命名为 *应用程序名* (为了Django能明确解读)
再在文件夹 *应用程序名* (新建的那个) 建立一个文件 index.html
并在其中编写代码(学习笔记案例)
```python
<p>Learning Log</p>

<p>Learning Log helps you keep track of your learning,for any topic you're learning about.</p>

```

```
标签<p></p>
	标识段落
```

# 创建其他页面

## 模板继承

### 父模板
创建一个名为 base.html 的模板，存储在 index.html 所在目录中
该模板包含所有页面都有的元素，其余模板都继承它
```Python
<p>
	<a href="{% url 'learning_logs:index' %}">Learning Log</a>
</p>
{% block content %}{% endblock content %}
```
第一部分创建了包含项目名的段落，段落包含了到主页的链接
使用了**模板标签**( {% %} )
这里模板标签内的代码为 生成一个URL，且该URL与 learning_logs/urls.py 中定义的 ‘index’ 的URL模式匹配
learning_logs 为一个**命名空间**，index 为该命名空间下的一个有独特名称的URL模式。该命名空间来自 learning_logs/urls.py 中 app_name 的值

在父模板中，预留了一对**块**标签( {% block %} {% endblock %} )，这里将块命名为 content ，作为占位符，其中包含的信息由子模版决定

子模版可以不用全部定义父模板中的每一个块，因此父模板可以预留多点块空间

### 子模板
现在重写 index.html，来继承 base.html 
将 index.html 更改为如下代码
```python
{% extends "learning_logs/base.html" %} 
{% block content %} 
	<p>Learning Log helps you keep track of your learning, for any topic you're learning about.</p> 
{% endblock content %}
```
第一行指定了要继承哪个模板，导入了继承模板的内容
后续插入名为 content 的块空间，内部包含了父模板中不存在的内容
在末尾的 {% endblock content %} 指出了内容结束位置。但事实上仅使用 {% endblock %} 也可以结束，包含块名方便辨认结束的是哪个块

## 显示所有主题的页面

### URL模式
这里来定义一个显示所有主题的页面的URL，在这里使用 topics 来指代该页面，则 http://localhost:8000/topics/ 将返回该页面
此处修改 learning_logs/urls.py
```python
--snip--
urlpatterns = [ 
	# 主页
	path('', views.index, name='index'),
	# 显示所有的主题
	path('topics/', views.topics, name='topics'),
]
```
此处的字符串参数中添加了 topics/
此模式与该URL匹配（基础URL后跟上topics）
URL与该模式匹配的请求都交给 view.py 中的函数 topics() 处理
### 视图
topics() 需要获取数据并交给模板
在views.py 中添加如下代码
```python
from django.shortcuts import render 
from .models import Topic 
def index(request): 
	--snip-- 
def topics(request): 
	"""显示所有的主题。""" 
	topics = Topic.objects.order_by('date_added') 
	context = {'topics': topics} 
	return render(request, 'learning_logs/topics.html', context)
```
导入与数据相关联的模型( from .models import Topic )
函数 topic 在这里包含一个形参 request，该形参从服务器接收

topics = Topic.objects.order_by('date_added')，查询数据库并请求提供 Topic 对象，并根据属性 date_added 进行排序
返回的查询集被存储在 topics 中

context = {'topics': topics}，定义一个发送给模板的**上下文**(字典，键为在模板中用来访问数据的名称，值为发送给模板的数据)

### 模板
显示所有主题的页面的模板将使用字典context ，得以接收topics() 提供的数据
创建文件topics.html 存储于index.html 所在目录
```python
{% extends "learning_logs/base.html" %}
{% block content %}
	<p>Topics</p>
	<ul>
		{% for topic in topics %}
			<li>{{ topic }}</li>
		{% empty %}
			<li>No topics have been added yet.</li>
		{% endfor %}
	</ul>
{% endblock content %}
```
使用标签{% extends %} 来继承base.html ，后定义content 块
该页面主体为项目列表，列出了用户输入的主题
在HTML 中，此类列表称为**无序列表**，用标签$<ul></ul>$表示


现修改父模板base.html ，使其包含到显示所有主题的页面的链接
```python
<p> 
	<a href="{% url 'learning_logs:index' %}">Learning Log</a> - 
	<a href="{% url 'learning_logs:topics' %}">Topics</a> 
</p> 
{% block content %}{% endblock content %}
```
在主页链接后添加连字符(-)，在页面中会直接显示，再添加一个链接，该链接与名为topics 的URL模式匹配
成功则主页会如此显示—— Learning Log - Topics

## 显示特定主题的页面
### URL模式
需要使用主题的id 来指出请求的是哪个主题
如用户需要查找id 为 1 的主题页面，URL为 http://localhost:8000/topics/1/
现将与该类型匹配的URL模式修改于learning_logs/ urls.py 中
```python
--snip-- 
urlpatterns = [ 
	--snip-- 		   
	# 特定主题的详细页面。 
	path('topics/<int:topic_id>/', views.topic, name='topic'), 
]
```
'topics/<int:topic_id>/' 
这个字符串的第一部分让Django查找在基础URL后包含单词topics的URL
第二部分（/<int:topic_id>/ ）与包含在两个斜杠内的整数匹配，并将这个整数存储在一个名为topic_id 的实参中
URL与该模式匹配时，调用视图函数topic()，将topic_id 的值进行传递

### 视图
函数topic() 需要从数据库中获取指定数据
将views.py 修改为如下所示
```python
--snip--
def topic(request, topic_id):  
	"""显示单个主题及其所有的条目"""
    topic = Topic.objects.get(id=topic_id)  
    entries = topic.entry_set.order_by('-date_added')  
    context = {'topic': topic, 'entries': entries}  
    return render(request, 'learning_logs/topics.html', context)
```
该函数接受表达式/<int:topic_id>/ 所获得的值，并存储到topic_id 中
使用get() 来获取指定主题


```PYTHON
entries = topic.entry_set.order_by('-date_added')  
```
在此句中，获取与该主题相关的条目，且根据date_added 来进行排序（减号为按降序排列）


```PYTHON
context = {'topic': topic, 'entries': entries} 
```
将主题和条目都存储在字典context 中
最后为发送字典给模板topics.html

### 模板
该模板包含显示主题的名称和条目内容
如不包含任何条目，需要指出
修改topic.html
```PYTHON
{% extends 'learning_logs/base.html' %}
{% block content %}
    <p>Topic: {{ topic }}</p>
    <p>Entries:</p>
    <ul>
        {% for entry in entries %}
            <li>
                <p>{{ entry.date_added|date:'M d, Y H:i' }}</p>
                <p>{{ entry.text|linebreaks }}</p>
            </li>
        {% empty %}
            <li>
                There are no entries for this topic yet.
            </li>
        {% endfor %}
    </ul>
{% endblock content %}
```
同样继承了base.html


```PYTHON
<p>Topic: {{ topic }}</p>
```
显示当前主题，存储于模板变量topic 中（其包含在字典context 中）


```PYTHON
<p>{{ entry.date_added|date:'M d, Y H:i' }}</p>
```
列出条目的时间戳，显示属性date_added 的值
竖线表示**模板过滤器**，对模板变量的值修改的函数
这里修改时间的显示格式为：January 1, 2018 23:00


```PYTHON
<p>{{ entry.text|linebreaks }}</p>
```
显示text 的完整值
linebreaks 将包括换行符的条目转换为可理解的格式，避免显示为不间断的文本块


```PYTHON
{% empty %}
    <li>
        There are no entries for this topic yet.
    </li>
```
使用模板标签 {% empty %} （检测为空时）打印消息，告诉用户当前主题无条目


### 将显示所有主题的页面中的主题设置为链接
需要修改topics.html ，来让每个主题都链接到对应的页面
下为原topics.html 内容
```PYTHON
{% for topic in topics %}  
    <li>  
        {{ topic }}  
    </li>
{% empty %}
```
修改为如下
```PYTHON
{% for topic in topics %}  
    <li>  
        <a href="{% url 'learning_logs:topic' topic.id %}">{{ topic }}</a> 
    </li>
{% empty %}
```
使用模板标签url ，根据learning_logs 中的名称为 topic 的URL模式生成链接
由于需要提供实参topic_id ，则在url 中添加了属性topic.id


# 用户账户
## 让用户输入数据
