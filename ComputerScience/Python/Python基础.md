# 变量  
```
money = 50  
print("钱包还剩：", money)  
money = money - 10  
print("花费了10元，还剩余：", money) 
``` 
  
## 查看数据类型 type()
```
print(type(money))  
print(type("亻尔女子"))  
int_type = type(money)  
print(int_type)  
```
  
## 数据类型转换  
```
numTostr = str(11)  
print(type(numTostr), numTostr)  
floatTostr = str(11.4514)  
print(type(floatTostr), floatTostr)  
strTonum = int("22")  
print(type(strTonum), strTonum)  
strTofloat = float("114.514")  
print(type(strTofloat), strTofloat)  
```
数字类型可以随时转换为字符串类型 字符串类型仅为数字时可以转换为数字类型  
  
## 标识符-->各种的名字  

仅允许出现英文字符，数字，下划线  
数字不可以出现在开头  
  
大小写会区分  
  
关键字不准使用  

  
## 变量命名规范  

见名知意  
  
单词用下划线分割  
  
英文全小写  

  
# 运算符  

```
+  加  
-  减  
*  乘  
/  除  
// 取整除  
%  取余  
** 指数 a**b --> a的b次方
```  

  
# 字符串  
```
a = 'Hello'  
aa = "Hello"  
aaa = """Hello""" # 支持换行操作 使用变量接收就是字符串 不接收就是多行注释  
``` 
单引号内包含双引号，输出则包含双引号  
  
双引号包含单引号，输出则包含单引号  
  
```
使用 \ 解除引号的作用，使引号变为字符  
"\"Hello\"" -输出-> ”Hello“  
```
  
## 字符串拼接 (无法和非字符串类型拼接)  
```
print("Hello" + a + "World") # -输出-> HelloHelloWorld  
```
  
## 字符串格式化  
```
handsome_num = 5  
battle_effectiveness = 10  
message = "帅气指数 %s" % handsome_num # %-->占位符号  
print(message) # s-->变量转变为字符串放入占位  
message = "银鳞战甲： 战斗力+%s 时髦度+%s 价格%s" % (battle_effectiveness, handsome_num, "5金")  
print(message)  
```
格式化符号  
%s 转为字符串，放入占位区  
%d 转为整数，放入占位区  
%f 转为浮点数，放入占位区  
  
## 格式化精度控制  

m.n 
m --> 宽度，用数字代替，如宽度小于数字自身则不生效  
.n --> 小数点精度，用数字代替，进行四舍五入  
  
例：  
%5d --> 将整数宽度控制在五位，缺位用空格在数前补齐  
%5.2f --> 将宽度控制为5，小数点精度设置为2  小数点及小数部分也纳入宽度计算  

  
## 快速字符串格式化--> f"{占位}"  
```
warframe_price = "5金"  
print(f"银鳞战甲{warframe_price}一件")  
print(f"树枝： 战斗力+{10*10} 价格{'5铜'}")  
```
 不限类型 不做精度控制  
 使用此字符串格式化方法直接格式字符串表达式，字符串要用单引号  
  
# 数据输入(input)  
 
```
print("请告诉我你的名字")  
name_input = input()  
print("%s吗？不错的名字" % name_input)  
name_friend_input = str(input("请告诉我你劲敌的名字吧"))  
print("原来叫%s吗？好的" % name_friend_input)  
```
  
# bool类型 
```
True Falseresult_bool = 10 > 5  
print(f"10 > 5 的结果为：{result_bool}, 类型为：{type(result_bool)}")  
result_bool = False  
print(f"result_bool的内容为:{result_bool}，类型是:{type(result_bool)}")  
```
  
# if判断&else&elif  
  
```
if 判断条件 :    条件成立时的语句  
    代码块要四个空格缩进  
elif 判断条件 :   
	条件成立执行语句  
else:  
    条件不成立执行语句
```  
and  
or  
值是否在列表中：in  
值是否不在列表中：not in  

  
# while  

```
while 条件:  
    条件成立，执行语句  
```

条件部分，布尔判断为Flase（直接使用布尔变量）  

  
# for  
遍历字符串  
```
name_for = "EldenRing"  
for x in name_for:  
    print(x)  
```
  
# range  
  
```
range(num) --> 从0开始到num结束的数列（不含num本身）  
range(num1, num2) --> 从num1到num2结束的数列（不含num2本身）  
range(num1, num2, step) --> 从num1到num2结束的数列（不含num2本身）  
                        --> 数字之间的步长以step为准（默认为1）
```  
 
  
# continue & break  

```
continue 执行下次循环  
break 退出循环  
```
  
  
# 函数  

```
def 函数名(传入参数):  
    函数体  
    return 返回值  
参数不需要时，可省略  
返回值不需要，可省略 --> 返回 None --> 类型为 'NoneType' --> if判断中None等于False  
```
  
返回多个值  
```
def text_return():  
    return value1, value2, value3  
x, y, z = text_return()  
```
## 函数的说明文档  
```
def add(x,y):  
    """  
    add函数接受两个参数，进行两数相加功能  
    :param x: 形参x表示相加的其中一个数字  
    :param y: 形参y表示相加的另一个数字  
    :return: 返回值为两数相加的结果  
    """   
    result = x + y  
    print(f"两数相加的结果是：{result}")  
    return result  
add(114,1514)  
```
  
## 全局变量  
 
```
num = 100  --> 全局变量  
def add(x,y):  
    global sum = 100  --> 全局变量  
    result = x + y + num + sum    
    return result
    
```
# 参数传入  
## 关键字参数  
   ```
 def key_parameter(name, age, gender):
	 print(f"name:{name}, age:{age}, gender:{gender}")    
	 key_parameter(name = "Alex", age = 20, gender = "Female")# 可以不按照固定顺序  
    key_parameter(age = 20, gender = "Female", name = "Alex") # 可与位置参数混用，但位置参数要在前，且匹配参数次序  
    key_parameter("Alex", gender = "Female", age = 20)
```   
     
## 缺省参数
```
def default_parameter(name, age, gender = "Male"):  
	# 设置默认值，有默认值的参数必须在无默认值的参数之后  
        print(f"name:{name}, age:{age}, gender:{gender}")    default_parameter("Tom", 20) --> Male    
        default_parameter("Rose", 18, "Female") --> Female    default_parameter("Tom", 20) --> Male
```
        
## 不定长参数  
### 位置传递：  
将传进的参数用元组类型收集  
```
def location_passing(*args):            
	print(args)        
	location_passing("Alex",20) --> ('Alex', 20)    
	location_passing("Alex")    --> ('Alex',)
```        

### 关键字传递：  
```
key = value # 来接受元素，组成字典  
def key_passing(**kwargs):            
	print(kwargs)        
# {'name': 'Alex', 'age': 20, 'gender': 'Female'} 
key_passing(name = "Alex", age = 20, gender = "Female")  
```
## 匿名函数：
临时使用一次  
```
lambda 传入参数: 函数体(一行代码)
```
  
# 数据容器  
  
## 列表 list 

### 列表建立&索引
```
变量名称 = [] --> 空列表  
变量名称 = list() --> 空列表  
变量名称 = [element1, element2, element3] --> 列表  
[element1, element2, element3] --> 列表字面量  
列表中，元素类型不限制为单一类型  
嵌套列表 --> [[], []]正向索引 --> 变量名称[0] 变量名称[1] 变量名称[2]  
反向索引 --> 变量名称[-1] 变量名称[-2] 变量名称[-3] (从后往前)  
```
### 列表基本操作  
```
查找某元素的下标 --> 列表.index(元素)  
修改特定位置元素 --> 列表[下标] = 新值  
插入元素 --> 列表.insert(下标, 元素) （插入位置元素及其后元素向后移动一位）  
追加元素 --> 列表.append(元素) & 列表.extend([列表])（尾部增加）  
删除元素 --> del 列表[下标] & 列表.pop(下标) --> pop方法可以得到删除元素的返回值  
删除某元素在列表中第一个匹配的元素 --> 列表.remove(元素)  
清空列表 --> 列表.clear()  
统计指定元素 --> 列表.count(元素)  
统计全部元素 --> len(列表)  

copylist --> A = B[:]  
```
  
```
my_favorite_singer = ["Vansire", "milet", "AJR", "Utada Hikaru",  
                      "Fuji Kaze", "Vaundy", "Hirai Dai"]  
print("The first three items in the list are:")  
for name in my_favorite_singer[:3]:  
    print(name)  
print("Three items from the middle of the list are:")  
for name in my_favorite_singer[2:5]:  
    print(name) 
``` 
  
### 列表解析  

```
squares = [value**2 for value in range(1,1)]  
```
  
两者等价，上为使用列表解析方法  
  
```
squares = []  
for value in range(1,11):  
    square = value**2    squares.append(square)
```
  
## 元组 tuple 
定义完成后，不可修改
### 元组建立&基本操作
```
变量名称 = ()
变量名称 = tuple()
变量名称 = (element1, element2)
变量名称 = (element, ) --> 仅有一个元素，则必须带有逗号
```
  
```
变量 = 元组名称[下标] --> 元组元素取出  
元组名称.index()  
元组名称.count()  
len(元组名称)  
```
  
元组内嵌套的list可以修改list内容  

  
## 字符串 str 
无法修改旧字符串，仅能新建字符串
### 字符串建立
```
变量 = 字符串名[下标]  
```
### 字符串基本操作
```
字符串.index()  
字符串.replace(旧字符串, 新字符串) --> 将旧字符串替换为新字符串 (得到一个新字符串)  
字符串.split(分隔符字符串) --> 字符串本身不变，得到一个新列表对象  
字符串.strip() --> 去除字符串前后空格  
字符串.strip(字符串) --> 去除前后指定字符串（将指定字符串中的单个单个删除）  
字符串.count(字符串) --> 统计指定字符串出现次数  
len(字符串)  
```
#### 示例代码
```
str_split = "Hello World"  
str_split_list = str_split.split(" ")  
print(str_split_list) # ['Hello', 'World']  
str_replace = "Hello World Elden Ring"  
str_replace= str_replace.replace(" ", "|")  
print(str_replace) # "Hello|World|Elden|Ring"  
str_strip = "  Elden Ring  "  
print(str_strip.strip()) # "Elden Ring"  
str_strip = "54Elden Ring45"  
print(str_strip.strip("54")) # "Elden Ring"  
```
  
## 序列 
内容连续、有序，可使用下标索引的数据容器 
列表、元组、字符串，可视为序列  
  
### 序列操作 
切片 --> 从一个序列中，取出子序列  
```
序列[起始下标:结束下标:步长] --> 步长为负数，反向取  
起始下标留空视为从头开始  
结束下标留空视为到尾为止  
  
不影响序列本身，得到一个新序列 
``` 

  
## 集合 set  
不允许重复元素，无序 --> 不支持下标索引访问  
集合遍历 --> 不能使用while循环，可以使用for循环 
### 集合基本操作
```
变量名称 = {element, element}变量名称 = set()  
集合.add(element) --> 添加新元素  
集合.remove(element) --> 移除元素 --> 原集合被修改  
集合.pop() --> 随机取出一个元素  
集合.clear() --> 清空集合  
A.difference(B) --> A-B (差集)  
A.difference_update(B) --> A = A-B (A内删除与B相同的元素，A被修改)  
A.union(B) --> A并B (原集合不变，生成新集合)  
len(集合) --> 统计元素数量
```   
  
## 字典、映射 dict 
key:value  
  
key相同时，较前的value会被较后的value覆盖  
不可以使用下标索引  
通过key来取得对应value  
  
key除字典外可为任意类型  
value可为任意类型  
### 字典基本操作
```
变量名称 = {key:value, key:value}变量名称 = dict()  
基于key获取value
dict_A.get() 基于键返回值
dict_A = {}  
value = dict_A[key1] --> value1
dict_B[Newkey] = value --> 新增  
dict_B[Oldkey] = newValue --> 更新  
value = dict_B.pop[key] --> 删除元素并返回value  
dict_B.clear() --> 清空  
keys = dict_B.keys() --> 得到全部key 
```  
  
#### 嵌套字典  
```
dict_B = {KEY:{key1:value1, key2:value2}}  
value = dict_B[KEY][key2] --> value2
```  
  
#### 字典遍历  
```
for key in dict_B:  
```
  
## 数据容器通用功能  

```
len() --> 元素个数  
max() --> 最大元素  
min() --> 最小元素  
  
list(容器) --> 转列表  
str(容器) --> 转字符串  
tuple(容器) --> 转元组  
set(容器) --> 转集合  
  
sorted() --> 临时排序,原序列未改变  
sorted(容器) --> 由小到大排序 （结果变成列表对象）  
sorted(容器, reverse = True) --> 由大到小排序  
  
sort()  --> 永久排序,原序列改变  
  
reverse() --> 反转列表排序  

Counter(容器) -->  计数器

'分隔符'.join(B) --> 将B 以分隔符分割并成字符串(元素必须为字符串型)
```
  
# 文件  
 
```
open(name, mode, encoding)  
name : 打开的目标文件名的字符串（可以包含文件具体路径）  
mode : 打开文件的模式 ：只读(r)、写入(w)、追加(a) （写入会删除原有内容）  
encoding : 编码格式 （建议 UTF-8 ）
```  
  
```
f = open("D:/text.txt", "r", encoding = "UTF-8")  
f.read(10) --> 读取10字节  
f.read() --> 读取全部内容 （多次调用read()，下一个read()开头就是在上个结尾之后）  
lines = f.readlines() --> 读取文件全部行，封装到列表中 （受read()影响）  
line = f.readline() --> 读取文件一行 （受read()影响）  
f.close() --> 关闭文件  
```
  
```
with open("D:/text.txt", "r", encoding = "UTF-8") as f:  
# 打开文件,并在代码块结束后关闭文件

代码块  
f.write(字符串) --> 文件写入 (并未写入文件,积攒在缓冲区)  
f.flush() --> 内容刷新 (真正写入文件) (close()带有相同功能)  
  
  
print 内加 rstrip() 可消除多余空白行  
```

# 异常  

异常具有传递性 

## 捕获常规异常  
```
try:  
    可能发生错误的代码  
except:  
    如果出现异常就执行的代码  
```
## 捕获指定异常  
```
try:  
    代码  
except 异常类型 as e:    
	出现异常则执行的代码  
```
 
## 捕获多个指定异常  
```
try:  
    代码  
except (异常类型, 异常类型) as e:  
    出现异常则执行的代码  
  
```
## 捕获全部异常  
```
try:  
    代码  
except Exeption as e:  
    出现异常则执行的代码  
```
 

  
# Python 模块  
 
## 导入模块  
```
[from 模块名] import [模块|类|变量|函数|*] [as 别名]  
from 可以省略  
  
from time import sleep --> 导入模块time中sleep函数  
from time import * --> 导入模块time的全部功能  
from time import sleep as s --> 导入模块time中sleep函数并命名为s  
import time --> 导入模块time
``` 
  
## 自定义模块  
 
建立py文件  
导入  
  
同名模块，后者会覆盖前者  
  
```
模块文件测试时 使用 __main__ 变量来测试  
  
__all__ --> 当模块文件中有'__all__'变量，使用'from xxx import *'  
            导入时，只能导入该变量列表中的元素  
```
# Python 包  
```
要在'__inti__.py'中添加'__all__ = []'来控制可导入的模块列表
from 包名 import * 模块名.目标  
```
## 导入包  
```
import 包名.模块名 
```
## 使用  
```
包名.模块名.目标 
``` 
  
## 第三方包安装  
 
```cmd
pip install 包名  
```
 
  
# 方法