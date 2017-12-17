# Python变量常量

## 一、变量(variable)

### 1、概要

> 要想要说变量，首先，要理解，编程是什么。编程，就是我们告诉计算机，你要帮我做什么。在这个过程中，有人、编程语言 、计算机三个角色，因为计算机是看不懂人类的语言的，而我们也无法直接地告诉计算机要做什么，

### 2 、什么是变量

> 变：变化，核心在与变化 量：衡量，计量，表达是一种状态
>
> 我们初学计算机语言的时候，就接触到了变量的概念，当然，那时候不可能给出精确的定义，很多书在讲的时候就像大家看到了变量这个词大概就能知道它是什么一样无需解释，比如《C语言程序设计》里直接就提到了变量的说明而没有说什么是变量。当我们带着这种模糊的感觉变成“有经验”的程序员时，似乎已经没人在意变量究竟是什么了
>
> ​	In computer programming, a variable is a storage location and an associated symbolic name (an identifier) which contains some known or unknown quantity or information, a value
>
> 变量是一个**存储位置**和一个关联的**符号名字**，这个**存储位置**包含了一些已知或未知的量或者信息，即值，所有理解变量要从这三个方面去理解
>
> 1. 名字（运行时会变成数字化的名字，内存地址）
> 2. 存储位置（某一位置开始的一定大小的存储空间）
> 3. 该存储位置里内容的解释方式（即类型，整数、浮点数还是字符串？）

## 二、变量声明与赋值

### 1、变量声明

> 在Python中，变量不需要明确的声明类型来保留内存空间。当向变量分配值时，Python会自动发出声明。 等号(`=`)用于为变量赋值。因为Python中变量声明变量不需要类型所有声明时最好直接赋值

### 2、示例代码

1. 基础使用

   ```python
   #!/usr/bin/python3 

   number1 = 1 #整形
   number2 = 1.2 #浮点型
   s= '字符串' #字符串类型
   t = Ture #布尔类型
   ```

2. 多重赋值

   ```python
   #不同的变量赋同一个值
   x=y=z=1
   ```

3. 多元赋值

   ```python
   #多元赋值
   #等号两边是元组 通常元组需要小括号,此处可以忽略
   x,y,z = 1,2,'a'
   #建议加上小括号,增加可读性
   (x,y,z) = (1,2,'a')
   ```

4. 变量交换

   ```python
   x = 1
   y ='3'
   x,y = y,x
   ```

## 三、变量命名规范

1. 变量名可以包括字母、数字、下划线，但是数字不能做为开头。

   ```python
   name1 = '老王' #合法变量名，
   1name='老王'  #错误声明
   ```

2. 系统关键字不能做变量名使用

   ```python
   def =1 #错误
   class = 'werner'#错误
   ```

3. 除了下划线之个，其它符号不能做为变量名使用

   ```python
   $name='jack' #错误

   user_name='jack' #正确(推荐命名,单词之间用下划线隔开,字母全部小写)

   userName ="rose" #正确
   ```

4. Python的变量名是除分大小写的，例如：name和Name就是两个变量名，而非相同变量哦。 

5. 变量命名尽量起的有意义,而且使用前尽量先赋值

## 四、常量

### 1、概念

> python中没有专门定义常量的方式，通常使用大写变量名表示。常量是一旦初始化之后就不能修改的固定值。例如:数字"5",字符串"abc"都是常量

### 2、示例代码

1. Python中并没有提供定义常量的保留字。Python是一门功能强大的语言，可以自己定义一个常量类来实现常量的功能。

   ```
   #fileName:const.py
   class _const:
     class ConstError(TypeError):pass
     def __setattr__(self,name,value):
       if name in self.__dict__:
         raise self.ConstError("Can't rebind const(%s)"%name)
       self.__dict__[name] = value
   import sys
   sys.modules[__name__] = _const()
   ```

   ```
   import const
   const.name='老王'
   const.name='小明'
   ```

### 3、命名规范

1. 字母全部大写,单词之间用下划线(_)连接

   ```python
   SYS_VERSION=1
   ```

   ​





