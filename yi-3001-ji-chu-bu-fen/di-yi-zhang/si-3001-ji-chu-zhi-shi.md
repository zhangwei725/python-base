# Python基础知识

## 一、编码规范

PEP-8 编码规范 

Python Enhancement Proposals ：python改进方案

Guido的关键点之一是：代码更多是用来读而不是写。编码规范旨在改善Python代码的可读性。

风格指南强调一致性。项目、模块或函数保持一致都很重要。

## 二、语法规范

### 1.1、注释

所谓注释，就是在程序中添加解释说明，能够大大增强程序的可读性。注释中的内容，不是真正要执行的程序，起辅助说明作用

**单行注释**

以#开头，#右边的所有东西当做说明

```python
# 我是注释，可以在里写一些功能说明之类的哦
print('hello world')
```

**多行注释**

使用3引号，3个单引号或者3个双引号

```python
'''
我是多行注释，可以写很多很多行的功能说明
        这就是我牛X指出
        哈哈哈。。。
'''

"""
我也是多行注释啊，巴拉巴拉。。
"""
```

### 1.2、缩进

**每级缩进用4个空格**

python 不使用 `{}` 来组织代码，完全依靠缩进，所以缩进的格式非常重要。

使用4个空格来缩进，不要使用 `tab` ,更不能 `tab` 和 空格混用。  

使用空格的时候永远使用4个空格，不能使用其他数量的空格，否则语法错误。

建议把开发工具的`tab`改成4个空格。

sublime 用如下方式设置：另外`pycharm`默认已经用4个空格替换`tab`

 ![](http://o7cqr8cfk.bkt.clouddn.com/17-7-1/72191093.jpg)

```python
# 对准左括号
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# 不对准左括号，但加多一层缩进，以和后面内容区别。
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

# 悬挂缩进必须加多一层缩进.
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)
```

注意：

括号中使用垂直隐式缩进或使用悬挂缩进。后者应该注意第一行要没有参数，后续行要有缩进。



### 1.3、分号

`python`不严格要求使用分号( `;`)。

理论上应该每行放一句代码。每行代码之后可以添加分号`;` 也可以不添加 分号`;`

尽量不要多句代码放在一行，如果放在一行，则需要添加分号把他们隔开。

### 1.4、行长度

每行不超过80个字符(最大行宽为79字符，文本长块，比如文档字符串或注释，行长度应限制为72个字符。)

以下情况除外：

1. 长的导入模块语句
2. 注释里的URL

不要使用反斜杠连接行。
如果一个文本字符串在一行放不下, 可以使用圆括号来实现隐式行连接:

```
x = ('这是一个非常长非常长非常长非常长 '
     '非常长非常长非常长非常长非常长非常长的字符串')
```

### 1.5、空行

两行空行分割顶层函数和类的定义。
类的方法定义用单个空行分割。
额外的空行可以必要的时候用于分割不同的函数组，但是要尽量节约使用。
额外的空行可以必要的时候在函数中用于分割不同的逻辑块，但是要尽量节约使用。

### 1.6、源文件编码

在核心Python发布的代码应该总是使用UTF-8(ASCII在Python 2)。

```python
# Python推荐使用
#-*- coding:utf-8 -*-
# 简化写法
# encoding: utf-8
```

Python 3(默认UTF-8)不应有编码声明。

### 1.7、导入在单行

```python
import os
import sys
from subprocess import Popen, PIPE
```

导入始终在文件的顶部，在模块注释和文档字符串之后，在模块全局变量和常量之前。

导入顺序如下：标准库进口,相关的第三方库，本地库。各组的导入之间要有空行。

> 禁止使用通配符导入。
>
> 通配符导入(from import *)应该避免，因为它不清楚命名空间有哪些名称存，混淆读者和许多自动化的工具。

### 1.8、括号

宁缺毋滥的使用括号，除非是用于实现行连接, 否则不要在返回语句或条件语句中使用括号. 不过在元组两边使用括号是可以的.

括号里边避免空格

```python
# 括号里边避免空格
# Yes
spam(ham[1], {eggs: 2})
# No
spam( ham[ 1 ], { eggs: 2 } )
```

### 1.9、空格

按照标准的排版规范来使用标点两边的空格

**1.9.1、括号内不要有空格.**

```
Yes: spam(ham[1], {eggs: 2}, [])
```

```
No:  spam( ham[ 1 ], { eggs: 2 }, [ ] )
```

**1.9.2、不要在逗号, 分号, 冒号前面加空格, 但应该在它们后面加(除了在行尾).**

```python
Yes: if x == 4:
         print x, y
     x, y = y, x

No:  if x == 4 :
         print x , y
     x , y = y , x
```

**1.9.3、参数列表, 索引或切片的左括号前不应加空格.**

```
Yes: spam(1)
```

```
no: spam (1)
```

```
Yes: dict['key'] = list[index]
```

```
No:  dict ['key'] = list [index]
```

**1.9.4、在二元操作符两边都加上一个空格,**

比如赋值(=), 比较(==, <, >, !=, <>, <=, >=, in, not in, is, is not), 布尔(and, or, not). 至于算术操作符两边的空格该如何使用, 需要你自己好好判断. 不过两侧务必要保持一致.

```
Yes: x == 1
```

```
No:  x<1
```

但是注意：当'='用于指示关键字参数或默认参数值时, 不要在其两侧使用空格.

```
Yes: def complex(real, imag=0.0): return magic(r=real, i=imag)
```

```
No:  def complex(real, imag = 0.0): return magic(r = real, i = imag)
```

不要用空格来垂直对齐多行间的标记, 因为这会成为维护的负担(适用于:, #, =等):

```
Yes:
     foo = 1000  # 注释
     long_name = 2  # 注释不需要对齐

     dictionary = {
         "foo": 1,
         "long_name": 2,
         }

No:
     foo       = 1000  # 注释
     long_name = 2     # 注释不需要对齐

     dictionary = {
         "foo"      : 1,
         "long_name": 2,
         }
```

------

**强烈不建议使用复合语句(Compound statements: 多条语句写在同一行)。**

```python
if foo == 'blah': print(100)
```

### 2.1、标识符和关键字

标识符就是对程序中变量，常量，类，方法，参数等命名时使用的 字符序列。

关键字就是python中预先保留下来，具有特殊含义的词。

Python的关键字：

```python
and	as	assert	break	class	continue	def	del	elif	else	except	
exec	finally	for	from	global	if	in	import	is	lambda	not	or	pass
print	raise	return	try	while	with	yield
```

命名规则如下

1. 标识符由字母，下划线，和数字组成，且数字不能开头
2. python 大小写敏感。  a 和 A 是完全不同的。
3. 不能是python关键字。

编码习惯：

1. 见名知意，使用有意义的，英文单词或词组，绝对不要使用汉语拼音。

2. 下划线命名和驼峰式命名

   ​	下划线：student_name

   ​	小驼峰：studentName

   ​	大驼峰：StudentNameTable	

3. 各种类型的命名规范：
   <img src="http://o7cqr8cfk.bkt.clouddn.com/markdown/1499780681915.png">


1. 避免采用的名字

   决不要用字符'l'(小写字母el)，'O'(大写字母oh)，或 'I'(大写字母eye) 作为单个字符的变量名。一些字体中，这些字符不能与数字1和0区别。用'L' 代替'l'时。

## 三、输入和输出

### 1、输出(见补充)

### 2、输入

#### 1.1、简介

> 输入输出，简单来说就是从标准输入中获取数据和将数据打印到标准输出，常被用于交互式的环境当中，Python中 input()来输入标准数据

#### 1.2、语法格式

> 格式：input() 
>
> 功能：接受一个标准输入数据，
>
> 返回：返回string类型。ctrl+z结束输入

#### 1.2、示例代码

1. 等待一个任意字符的输入

   ```python
   input('请输入用户名:\n')
   ```

   ![](http://opzv089nq.bkt.clouddn.com/17-12-17/72640959.jpg)

2. 接受多个数据输入，使用eval（）函数，间隔符必须是逗号

   ```python
   a,b,c=eval(input())
   ```

   ![](http://opzv089nq.bkt.clouddn.com/17-12-17/28041633.jpg)