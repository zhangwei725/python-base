

## 一、序列

### 1、概要

> 在Python中，最基本的数据结构是序列（sequence）。序列中的每个元素被分配一个序号——即元素的位置，也称为索引。第一个索引是 0，第二个则是 1，以此类推。序列中的最后一个元素标记为 -1，倒数第二个元素为 -2，一次类推。 Python包含 6 中内建的序列，包括列表、元组、字符串、Unicode字符串、buffer对象和xrange对象。

### 2、序列操作

#### 2.1、通用操作

1. 索引
2. 分片
3. 加
4. 乘
5. 检查某个元素是否属于序列

#### 2.2、内置函数

1. 计算序列长度
2. 计算最大元素及最小元素

### 3、索引

1. 概念

   元素在序列中的编号。这些编号从0开始递增，0表示第一个元素,最后一个元素为序列的长度-1

2. 语法格式

   ```python
   seq[索引]
   ```

3. 结构图

   ![](http://opzv089nq.bkt.clouddn.com/17-12-31/5320930.jpg)

4. 示例代码

   字符串中使用索引

   ```python
   demo = 'Hello World'
   print(demo[0]) #输出 H
   print(demo[5]) #输出空格字符串
   print(demo[-1]) #输出 d
   #思考可不可以索引是-0
   ```

   函数中使用索引，有一些函数的返回值为字符串，有的返回其他的序列，我们可以在函数调用之后使用[]来对返回序列的元素值进行索引

   ```
   In [6]: input("请输入:")[1]
   请输入:123
   Out[6]: '2'
   ```

### 4、切片

1. 定义

   切片也叫分片，即提取一个范围内的序列

2. 语法格式

   ```
   序列名（或字符串字面值）[beg_index：end_index，step] 
   ```

3. 说明

   - beg_index 

     起始下标，默认0

   - end_index

     终止下标，默认取到末尾

   - step：

     表示取值的步长，默认为1，步长值不能为0，默认为1，步长可以为负数，表示从右向左提取元素

4. 注意事项

   - 范围采用左闭右开(顾头不顾尾)，即第一个索引元素包含在分片内，第二个则不包含在分片内。
   - 终止索引超出范围时，分片直接取到序列最后一个元素
   - 索引和步长都具有正负两个值，分别表示左右两个方向取值。索引的正方向从左往右取值，起始位置为0；
   - 负方向从右往左取值，起始位置为-1。因此任意一个序列结构数据的索引范围为 -len到 len-1范围内的连续整数。

5. 示例代码

   1、同时忽略两个索引，整个序列都成为分片了

   ```python
   cele = "you can you up ,no can no bb ^_^"
   print(cele[:]) #输出 全部
   ```

   2、开始索引,结束索引默认,步长默认，从包含的开始索引截取至末尾

   ```python
   print(cele[1:]) 
   ```

   3、开始索引为负数,结束索引默认,步长默认，从右边开始截取至末尾

   ```python
   print(cele[-1:]) 
   ```

   4、结束索引，开始索引忽略，步长默认，截取0至结束索引

   ```python
   print(cele[:5]) 
   ```

   5、结束索引为负数，开始索引忽略，步长默认，截取0至右边结束索引

   ```python
   print(cele[:-3])
   ```

   6、开始索引比结束索引的元素在序列中出现得晚时，切片为空序列

   ```python
   print(cele[-3:1])
   ```

   7、步长为2,截取开始索引到结束索引

   ```python
   print(cele[0:10:2])
   ```

   8、左索引比右索引的元素在序列中出现得晚时

   ```python
   print(cele[::-1]) #反置
   ```

6. 总结

   - seq[start_index]

     返回索引值为start_index的对象。start_index为 -len(seq)到len(seq)-1之间任意整数。

   - seq[start_index: end_index]

     返回索引值为start_index到end_index－1之间的连续对象。

   - seq[start_index: end_index : step]

     返回索引值为start_index到end_index-1之间，并且索引值与start_index之差可以被step整除的连续对象。

- seq[start_index: ]

  缺省end_index，表示从start_index开始到序列中最后一个对象。

- seq[:end_index］

  缺省start_index，表示从序列中第一个对象到end_index-1之间的片段。

- seq[:]

  缺省start_index和end_index，表示从第一个对象到最后一个对象的完整片段。

- seq[::step]

  缺省start_index和end_index，表示对整个序列按照索引可以被step整除的规则取值

### 5、序列相乘

1. 说明

   用数字x乘以一个序列会产生新的序列，在新的序列中，原来的序列将被重复x次

2. 示例代码

   ```python
   i = '1' * 5
   print(type(i))
   print(i)
   ```

### 6、序列相加

1. 说明

   两个序列相加返回一个新的序列

2. 示例代码

   ```python
   seq1 = 'Hello'
   seq2 = 'World'
   seq3 = seq1 + seq2
   print(seq3)
   ```

### 7、使用None创建空序列

1. 示例代码

   ```
   sequence = 10*[None]
   sequence
   [None, None, None, None, None, None, None, None, None, None]
   ```

8、是否包含

1. 说明

   指某值是否在序列中，使用in**运算符**，运算符结果为**布尔值**True 或者 False

2. 语法格式

   ```
   '某值' in 序列
   ```

3. 示例代码

   ```python
   cele = "you can you up ,no can no bb ^_^"
   print('y' in cele) # True
   print('^_^' in cele) # True
   print('you1' in cele) # false
   ```

### 8、序列长度

1. 内置函数

   ```
   len(序列)
   ```

2. 示例代码

   ```
   cele = "you can you up ,no can no bb ^_^"
   print(len(cele)) #32
   ```

### 9、最小值

1. 内置函数

   ```
   min(序列)
   ```

2. 示例代码

   ```python
   #纯数字
   numbers = "123456789"
   print(min(numbers)) #1
   #纯字母
   letter = "abcdef"
   #字母加数字
   letter = "abcdef123"
   print(min(letter)) #1
   #中文 底层比较是Unicode编码 
   letter = "时间在哪里,成就就在哪里"   
   print(min(letter)) #输出  ,(\u002c)
   ```

### 10、最大值

1. 内置函数

   ```
   max(序列)
   ```

2. 示例代码

   ```
   #纯数字
   numbers = "123456789"
   print(max(numbers)) #9
   #纯字母
   letter = "abcdef"
   #字母加数字
   letter = "abcdef123"
   print(max(letter)) #f
   #中文 底层比较是Unicode编码 
   letter = "时间在哪里,成就就在哪里"   
   print(max(letter)) #输出  间(\u95f4)

   ```

## 二、字符串

### 1、字符串的定义

字符串就是一串字符，是编程语言中表示文本的数据类型

在Python中可以使用 一对双引号或者一对单引号定义一个字符串

> 虽然可以使用`\"`或`\'`做字符串的转移，但是实际开发中
>
> - 如果字符串内容需要使用`"`，可以使用`'`定义字符串
> - 如果字符串内容需要使用`'`，可以使用`"`定义字符串

```python
str1 = "hello python"
str2 = "你是'王二狗'么"
str3 = '你是"李小花"么'
print(str1)
print(str2)
print(str3)
```

### 2、连接和重复

在前面的学习中我们已接近了解了什么是字符串，字符串的连接，输出等。下面我们开始学习字符串更高级的功能。

`+` 用来连接两个字符串

`*` 用来重复字符串

上面两个操作符可以都可以操作变量。

```python
a = "你好"
b = a + "world"
c = b * 3
print(b)
print(c)
```

如果两个或多个字符串字面量写在一起，则他们会自动的连接在一起。

```python
d = "a" "b""c"  "你好"
print(d)   # abc你好
```

注意：

1. 只都是字符串字面量才可以通过这种方法连接，变量不能参与
2. 字符串之间不要添加任何标点符号
3. 如果想要打破比较长的字符串，这种方式尤其有用。

```python
text = ("窗前明月光" 
        "疑是地上霜"
        "举头望明月"
        "低头思故乡")
print(text)
```

![](http://o7cqr8cfk.bkt.clouddn.com/17-7-3/70225235.jpg-yztcText)

### 3、获取字符串长度

​    字符串的长度，就是指的字符串中字符的个数。使用内置函数 `len()` 来获取字符串长度。 `len()` 可以获取任何序列的长度，后面我们会了解更多。

```python
s = "hello world"
print(len(s))    # 11
```

### 4、字符串索引\(index\)

​    字符串中的每个字符都有一个编号，这个编号在编程语言中一般称之为索引\(`index`、下标\)。可以通过索引单独去访问字符串中的每个字符。

​    另外，由于 `python` 中没有字符类型，所以即使拿到的是单个字符也是字符串类型的。

​    `index` 是从 `0` 开始，最后一个字符的索引：`字符串长度 - 1`

```python
s = "hello world"
print(s[0])
print(s[3])
print(s[len(s) - 1])
```

![](http://o7cqr8cfk.bkt.clouddn.com/17-7-3/63281545.jpg-yztcText)

------

​    索引也可以是负值，表示从右开始计算。`-1` 就是最后一个元素的索引。  `-0` 和 `0` 是一样的。

```python
s = "hello world"

print(s[-1])
print(s[-2])
print(s[-len(s)])
```

------

如果 `index` 超出了范围，则会抛出异常。所以使用的时候一定要小心，防止下标越界。

```python
s = "hello world"
print(s[len(s)])
```

### 5、 字符串切片\(`slice`\)

​    使用 `index` 只能获取单个的字符。而字符串的切片操作可以获取子字符串。

​    python 的切片操作非常的优雅！如果你使用过别的语言，就知道我为什么这么说了。

```python
s = "life is short, use python"
print(s[0:4])  # 获取下标为 0(包括) 到下标为 4(不包括) 的子字符串    "life"
print(s[2:3])    # "f"
print(s[2:])    # fe is short, use python
print(s[:4])    # life
print(s[-2:])    # on
```

**注意：**

1. 切片的时候，总是开始下标包括，结束下标不包括
2. 第一个下标和最后一个下标都可以省略。如果省略第一个下标则默认值是 `0`，如果省略第二个下标则默认值是字符串的长度

------

虽然在使用下标获取单个字符的时候，如果超出范围会抛出异常。

但是在切片的时候，如果越界则不会抛出异常。

```python
s = "life is short, use python"
print(s[9:100])        # hort, use python
print(s[-1:1000])    # n
```

------

### 6 、字符串的不可变性

字符串的不可变性是指，字符串在内存中一旦创建，则字符串的内容终身无法更改。如果想获取不同的字符串，只能再重新创建一个字符串。

不可变的好处就是，共享而不用担心同步问题。因为大家都不能修改。

所以，通过下标修改字符串中的某个字符是错误，会抛出异常。

```python
s = "life is short, use python"
s[0] = "c"    #    不能修改，这行代码会抛出异常
```

如果需要不同的字符串，应该创建一个新的，如下面的代码:

```python
s = "life is short, use python"
s1 = "P" + s[1:]
print(s1)
```

![](http://o7cqr8cfk.bkt.clouddn.com/17-7-3/3756398.jpg-yztcText)

### 7 、一些其他的与字符串相关的运算符

前面学习了 `+、*、[]、[:]`运算符可以操作字符串，还有一些其他的运算符也可以操作字符串。

 `in`

测试字符串是否包含这样的子字符串

```python
s = "python"
print("p" in s)        # True      s 中是否包含字符串`p`
print("P" in s)        # False
```

 `not in`

与 `in` 的含义相反

```python
s = "python"
print("p" not in s)        # False
print("P" not in s)        # True
```

 `%(了解)`

格式化字符串。格式化字符串有比较多的格则，与 c 语言的 `printf()` 的格式化规则一样。

常用的就下面 3 种。

```python
name = input("请输入你姓名：")
age = int(input("请输入你的年龄："))
print("你好%s,你今年%d, 你的工资是 %.2f" % (name, age, 30000.4598))
```

### 8、字符串对象的常用方法

前面学习的一些函数都是内置函数，直接调用即可。

下面再学习几个字符串对象的方法。\(实例方法, 后面面向对象再具体详细学习\)

**需要注意:在下面的方法中, 如果是涉及到修改字符串的，一定是创建了一个新的字符串，并返回。**

使用： `字符串.方法(参数)` 来调用

1. `s.capitalize()`

   把首字母变换为大写字母，并返回字符串

2. `s.center(w)`

   把字符串居中，用空格填充两边。`w` 是填充后的总长度。如果不想用空格填充，可以传入第二个参数，必须是一个字符。

3. `s.find(str, beg=0, end=len)`

   方法检测字符串中是否包含子字符串 `str` ，如果指定 `beg`（开始） 和 `end`（结束） 范围，则检查是否包含在指定范围内，如果包含子字符串返回开始的索引值，否则返回 -1。

4. `s.isalnum()`

   如果字符串的长度大于 0 ，并且所有字符都是字母或数字，则返回 `True`

5. `s.isalpha()`

   如果字符串的长度大于 0 ，并且所有字符都是字母，则返回 `True`

6. `s.isdigit()`

   如果字符串的长度大于 0 ，并且所有字符都是数字，则返回 `True`

7. `s.lower()`

   所有字母小写

8. `s.upper()`

   所有字母大写

9. `s.strip([chars])`

   把字符左右两端的 `chars` 去掉 。如果不传入参数，默认去除空格。 中间的不去掉。

10. `s.lstrip([chars])` `s.rstrip([chars])`

    去掉左边或右边的指定字符，默认是空格

11. `s.split(chars)`

    使用 `chars` 去切割字符串，如果不传入 `chars`则默认使用 空白字符

12. `s.swapcase()`

    反正字符串中的大小写

13. `s.title()`

    标题化。意思就是说，每个单词的首字母大写，其余字母小写

```python
s = "hello"
print(s.capitalize())
print(s.center(30, "z"))
print(s.find("el"))
print("123".isdigit())
print("122".isnumeric())
print("  ab  c   ".strip())
print("aabbaa".strip("a"))
print(max([100, 30, 40, 90]))
print("10.2.3.5".split("."))
print("hell world".title())
```



##  