# Python数据类型

## 一、简介

> Python3中有六个标准的数据类型：
>
> 1. 字符串（String）
> 2. 数字（Digit）
> 3. 列表（List）
> 4. 元组（Tuple）
> 5. 集合（Sets）
> 6. 字典（Dictionary）

## 二、分类

​

## 三、Numbers（数字）

### 1、说明

> Python 3支持int、float、bool、complex（复数）。
>
> 数值类型的赋值和计算都是很直观的，就像大多数语言一样。内置的type\(\)函数可以用来查询变量所指的对象类型。

### 2、整型\(int\)

#### 2.1、说明

> 通常被称为是整型或整数，是正或负整数，不带小数点。Python3 整型是没有限制大小的，可以当作 Long 类型使用，所以 Python3 没有 Python2 的 Long 类型。

#### 2.1、示例代码

1. 正整数,负整数

   ```python
   i = 1212121212
   i=-1000000
   ```

2. `2进制`、`8进制`、`10进制`、`16进制`

   ```python
   a = 100     # 十进制的100.
   print(a)
   b = 0b100   # 用 0b 开头表示二进制数据
   print(b)
   c = 0o100   # 用 0o 开头表示八进制数据
   print(c)
   d = 0x100   # 用 0x 开头表示十六进制的数据
   print(d)
   ```

   ![](http://opzv089nq.bkt.clouddn.com/17-12-17/7670588.jpg)

### 3、浮点型

#### 3.1、说明

> 浮点型由整数部分与小数部分组成，  **提供大约17位的精度**和范围从-308到308的指数
>
> 浮点数可以用数学写法，如`1.23`，`3.14`，`-9.01`，等等。但是对于很大或很小的浮点数，就必须用科学计数法表示，把10用e替代，`1.23x109`就是`1.23e9`，或者`12.3e8`，`0.000012`可以写成`1.2e-5`等等。

#### 3.2、示例代码

1. 基础使用

   ```
   f=1000.0
   f1=-1000.1233333333333
   c= 3.1415
   ```

2. 科学计算e

   ```
   # 3141.5
   e1 =3.1415e3
   # -0.0031415
   e2 = -3.1415e-3
   ```

   ![](http://opzv089nq.bkt.clouddn.com/17-12-17/2623168.jpg)

#### 3.3、注意

> 整数和浮点数在计算机中的存储方式是不一样的。整数永远可以精确的表示，而大部分的浮点数是近似表示。

### 4、复数

#### 4.1、说明

> 复数由实数部分和虚数部分构成，可以用a + bj,或者complex\(a,b\)表示， 复数的实部a和虚部b都是浮点型

#### 4.2、示例代码

1. 基础使用

   ```python
   var1 = 123j #复数
   var2 = 123+45j #复数
   var3 = 123j+45j #复数
   print(var1.real)  
   print(var2.real) 
   print(var3.real) 

   print(var1.imag)  
   print(var2.imag) 
   print(var3.imag)
   ```

   ![](http://opzv089nq.bkt.clouddn.com/17-12-17/8491331.jpg)

2. complex\(a\)

   ```python
   a = complex(10)
   print(a.real)
   #output实数部分 10
   print(a.imag)
   #output虚数部分 0
   ```

3. complex\(a,b\)

   ```
   a = complex(10,1)
   print(a.real)
   #output实数部分 10.0
   print(a.imag)
   #output虚数部分 1.0
   ```

   ![](http://opzv089nq.bkt.clouddn.com/17-12-17/72809464.jpg)

## 四、String（字符串）

### 1、说明

> Python中的字符串str用单引号\(' '\)或双引号\(" "\)括起来，同时使用反斜杠\(\)转义特殊字符。
>
> 如果你不想让反斜杠发生转义，可以在字符串前面添加一个r，表示原始字符串：

2、其它转椅字符

> 有些字符没有办法直接写在 单引号或者双引号中，比如回车、换行、制表符等。这时候需要借助转义字符来。`\` 是转义字符。\(几乎在所有的编程语言中都是它\)
>
> | 转义字符串 | 含义 |
> | --- | --- |
> | \n | 换行 |
> | \' | 单引号 |
> | \" | 双引号 |
> | \ | \ |
> | \t | 制表符 |
> | \r | 回车 |
> | \b | 退格\(back\) |

### 3、总结

1. 反斜杠可以用来转义，使用r可以让反斜杠不发生转义。
2. 字符串可以用+运算符连接在一起，用\*运算符重复。
3. Python中的字符串有两种索引方式，从左往右以0开始，从右往左以-1开始。
4. Python中的字符串不能改变。

## 五、布尔值\(bool\)

### 1、说明

> 布尔值表示一种逻辑值。在 `python` 中只有 2 个字面量布尔值 `True` 和 `False` 。
>
> 注意：bool 是int的子类，继承自int

### 2、示例代码

> ```python
> a = True
> b = False
> c = 3 > 4
> print(a)
> print(b)
> print(c)
> ```

## 六、空值None类型

### 1、说明

> 空值是Python里一个特殊的值，用None表示。None不能理解为0，因为0是有意义的，而None是一个特殊的空值。可以将None赋值给任何变量，也可以将任何变量赋值给一个None值得对象

### 2、示例代码

> ```
> a = None
> b = None
> ```

### 3、总结

1. None是一个特殊的常量。
2. None和False不同。
3. None不是0。
4. None不是空字符串。
5. None和任何其他的数据类型比较永远返回False。
6. None有自己的数据类型NoneType。

## 七、类型判断

### 1、说明

> 在Python中可以使用type\(\)来对简单的数据库类型进行判断
>
> 为什么要进行数据判断,主要增加健壮性,因为有些时候客服端传过来的数据是不可靠的

### 2、type

1. 说明

   **type\(\)函数**在python中是即简单又实用的一种对象数据类型查询方法

2. 函数

   ```
   obj = type(对象)
   ```

3. 参数说明

   接收一个对象当做参考

4. 返回类型

   返回对象对应的类型

5. 示例代码

   ```python
   # int
   x = 123
   print(type(x))
   # float
   y = 123.1
   print(type(y))
   # str
   print(type('111'))
   # bool
   print(type(True))
   ```

## 8、基本类型转化

### 1、其它类型转化成Int类型

1. 说明

   把符合数学格式的数字型字符串转换成整数  
   把浮点数转换成整数，但是只是简单的取整，而非四舍五入

2. 函数

   ```
   int(x, base=10)
   ```

3. 参数

   * x

     要转化成int的类型\(数字字符串,float\)

   * base

     进制  默认转化成10进制

4. 示例代码

   ```python
   aa = int("124")   
   print("aa = ", aa)

   bb = int(123.45) 
   print("bb = ", bb)

   ee = int("12.3") 
   print(ee)

   cc = int("-123.45")  #注意不能转化负数的字符串
   print("cc = ",cc)

   dd = int("34a") #注意不能转化非数字的字符串
   print("dd = ",dd)
   ```

### 2、其它类型转化成float

1. 说明

   把符合数学格式的数字型字符串转换成浮点数  
   把整数转换成浮点型

2. 函数

   ```
   float(x)
   ```

3. 参数说明

   * x

     要转化的其它类型数据

4. 示例代码

   ```python
   aa = float("124")     
   print("aa = ", aa)    #result = 124.0 
   bb = float("123.45")  
   print("bb = ", bb)   #result = 123.45
   cc = float(-123.6)  
   print("cc = ",cc)    #result = -123.6
   dd = float("-123.34") 
   print("dd = ",dd )    #result = -123.34
   ee = float('123v')    #非数字类型不能转化
   print(ee)
   ```

### 3、将其它类型转化成字符串类型

1. 说明

   将对象 x 转换为字符串

2. 函数

   ```
   str(x)
   ```

3. 参数说明

   * x

     要转化成字符串的其它类型

4. 示例代码

   ```python
   aa = str(110)     
   print("aa = ", aa)   
   bb = str(123.45)  
   print("bb = ", bb)  
   cc = str(-3.131415)  
   print("cc = ",cc)   
   dd = str(-123.34) 
   print("dd = ",dd )    
   ee = float('123')   
   print(ee)
   ```

### 4、将其它类型转化成bool类型

1. 说明

   在python中，除了''、""、0、\(\)、\[\]、{}、None为False， 其他转换都为True。 也就是说字符串如果不为空，则永远转换为True。

2. 函数

   ```
   bool(x)
   ```

3. 参数

   * x

     要转化的字符串

4. 示例代码

   ```python
   bool(0)
   False
   bool('abc')
   True
   bool(' ')   #参数是一个空格，非空。
   True
   bool('')    #参数为空。
   False
   bool([])
   False
   bool()
   False
   bool(None)
   False
   issubclass(bool,int) #判断是否是子类
   True
   ```

   ​

   ​



