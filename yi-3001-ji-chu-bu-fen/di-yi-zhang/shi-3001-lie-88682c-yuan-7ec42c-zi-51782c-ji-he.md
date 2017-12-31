# Python列表,元组,字典

一、概要

> 到目前为止，我们如果想保存一些数据，只能通过变量。但是如果遇到较多的数据要保存，这个时候时候用变量就变的不太现实。我们需要能够保存大量数据的类似变量的东东，这种东东就是数据结构\(Data Structures\)。
>
> 数据结构，它们只是一种结构，能够将一些数据聚合在一起的结构。换句话说，它们是用来存储一系列相关数据的集合。
>
> **python 提供了 4 种内置数据结构：**`List`**\(列表\)、**`Tuple(元组)`**、**`Dictionary`**\(字典\)、**`Set`**\(集合\)**
>
> 严格来说，字符串也是一种数据结构，因为他把字符组织在了一起。

## 二、list\(列表\)

### 1 、简介

> `list`python 中一般把它翻译为列表.
>
> list\` 是处理一组有序数据的数据结构，即你可以在一个列表中存储一个序列的数据,
>
> `list` 是 python 中用途最广的一种数据结构。
>
> `list` 可以存储多个数据，这些数据用 `[ ]` 包裹，各个数据之间用 `,` 分割。
>
> `list`中的元素可以是任意类型的，但是实际使用的时，一个`list` 中一般只存储一种数据类型的数据。
>
> `list` 中可以存储的元素是有顺序的，且允许重复。
>
> `list` 中的元素也可以更改。

### 2、如何定义

1. 语法结构

   ```python
   [元素1,元素2,元素3,...]
   ```

2. 结构图

   ![](http://opzv089nq.bkt.clouddn.com/17-12-21/33264806.jpg)

3. 说明

   * 列表是写在⽅括号**\[\]** 之间
   * ⽤**逗号 **  ,  分隔开的元素列表
   * 列表中元素的类型可以是不相同

4. 示例代码

   ```
   list = ["小花","小明",18,5000.00,"武汉市高新区"]
   ```

### 3、获取元素

#### 3.1、通过索引

1. 语法格式

   ```
   list[index]
   ```

2. 说明

   index：表示列表中元素的下标\(或者理解为位置，从0开始。到长度-1。不能越界\)

3. 示例代码

   ```python
   info_list = ["小花","小明",18,5000.00,"武汉市高新区"]
   print(info_list[0]) #输出 '小花'
   print(info_list[1]) #输出 '小明'
   print(info_list[-1]) #输出 "武汉市高新区"  删除倒数第一个 
   print(info_list[6]) #输出错误 
   """
   Traceback (most recent call last):
     File "list.py", line 6, in <module>
       print(info_list[6])
   IndexError: list index out of range
   """
   ```

#### 3.2、通过for循环

1. 语法格式

   ```python
   for 变量名 in 列表名:
       print(变量名)  # 就是打印输出列表中的每一个元素
   ```

2. 示例代码

   ```python
   info_list = ["小花",18,5000.00,"武汉市高新区"]
   for item in info_list:
   print(item)

   小花
   18
   5000.0
   武汉市高新区
   ```

#### 3.3、通过whille

1. 语法格式

   ```python
   index = 0
   while index < len(列表) :
       #通过索引获取列表的中的元素
       print(列表[index])
         index +=1
   ```

2. 示例代码

   ```python
   info_list = ["小花",18,5000.00,"武汉市高新区"]
   index = 0
   while index < len(列表):
       print(info_list[index])
       index += 1
   ```

#### 3.4、通过切片

1. 语法格式

   ```python
   list(eg，end，delta)
   ```

2. 说明

   截取部分元素

3. 参数

   * eg（起始下标）

4. end（终止下标）

5. delta（变化量）

6. 返回值

   返回一个所有截取的值,生成一个新的列表,不影响原来的列表

7. 示例代码

   ```python
   num_list = [1,2,3,4,5,6,7,8,9]
   print(num_list[0:3]) #截取第一位到第三位的元素 输出结果 [1, 2, 3]
   print (num_list[:]) #截取列表的全部  输出结果[1,2,3,4,5,6,7,8,9]
   print (num_list[0:3]) #截取列表的全部 输出结果[1, 2, 3]
   print (num_list[6:]) #截取第七个元素到结尾  输出结果[7, 8, 9]
   print (num_list[:-3]) #截取从头开始到倒数第三个元素之前 输出结果[1, 2, 3, 4, 5, 6]
   print (num_list[2]) #截取第三个元素 输出结果[3]
   print (num_list[-1]) #截取倒数第一个元素 输出结果[9]
   print (num_list[-3:-1]) #截取倒数第三位与倒数第一位之前的元素 输出结果[7, 8]
   print (num_list[-3:]) #截取倒数第三位到结尾 输出结果[7, 8, 9]
   print (num_list[:-5:-3])#逆序截取 输出结果[9, 6]
   ```

   **注意:**

   ​    所有的切片操作都是返回一个新的 `list` ,所以我们可以通过切片非常轻松的 copy 一个`list`

### 4、添加元素

#### 4.1、append

1. 语法格式

   ```
   list.append(obj)
   ```

2. 说明

   向 `list` 的末尾添加元素,参数obj

3. 参数

   要添加的对象

4. 返回值

   无返回值，修改原来的列表

5. 示例代码

   ```
   nums = [10, 20, 40, 30, 25]
   nums.append(1000)
   print(nums)
   ```

#### 4.2、insert

1. 语法格式

   ```python
   list.insert(index, obj)
   ```

2. 说明

   把元素 `ele` 插入到指定的 `index` 位置。原来的元素会自动右移动

3. 参数

   * index -- 对象 obj 需要插入的索引位置。
   * obj -- 要插入列表中的对象

4. 返回值

   没有返回值，修改原来的列表

5. 示例代码

   ```python
   nums = [10, 20, 40, 30, 25]
   nums.insert(2, 2000)
   print(nums)
   ```

#### 4.3、extend

1. 语法格式

   ```
   list.extend(seq)
   ```

2. 说明

   用于在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）

3. 参数

   元素列表

4. 返回值

   没有返回值，但会在已存在的列表中添加新的列表内容。

5. 示例代码

   ```python
   it = ['Python', 'Java', 'JavaScript']
   it2 = ['H5','Androi','IOS']
   it.extend(it2)
   print(it)

   ['Python', 'Java', 'JavaScript', 'H5', 'Androi', 'IOS']
   ```

### 5、删除元素

#### 5.1、del

1. 语法格式

   ```python
   del 列表[索引]
   ```

2. 说明

   可以删除指定下标的值,`del`关键字本质上是用来将一个变量从内存中删除的。

3. 返回值

   无

4. 示例代码

   ```python
   nums = [10, 20, 40, 30, 25]
   del nums[0]
   print(nums)
   del nums[0:2]
   print(nums)
   ```

#### 5.2、pop

1. 语法格式

   ```
   列表.pop([index])
   ```

2. 说明

   移除列表中的一个元素（默认最后一个元素），并且返回该删除元素的值

3. 返回值

   该方法返回从列表中移除的元素对象。

4. 示例代码

   ```python
   nums = [10, 20, 40, 30, 25]
   #pop 指定位置删除
   del_value =  nums.pop(0)
   # 删除最后⼀个
   last_value =  nums.pop()
   print(lastvalue)
   ```

#### 5.3、remove

1. 语法格式

   ```
   list.remove(obj)
   ```

2. 说明

   移除列表中某个值的第一个匹配项 没有会抛异常

3. 返回值

   无返回值

4. 示例代码

   ```python
   nums = [10, 20, 40, 30, 25,10]
   nums.remove(10)#移除指定位置
   print(nums)
   nums.remove(100) #移除不存在的 抛出异常

   [20, 40, 30, 25, 10]
   ```

#### 5.4、clear

1. 语法

   ```
   list.clear()
   ```

2. 说明

   清空列表中所有的元素

3. 参数

   无

4. 返回值

   无

5. 示例代码

   ```python
   nums = [10, 20, 40, 30, 25,10]
   nums.clear()
   print(nums)

   []

   nums2 = [10, 20, 40, 30, 25,10,[1,2,3,4]]
   nums2.clear()
   print(nums2)

   []
   ```

6、修改元素

6.1、通过定位到下标直接修改

1. 语法格式

   ```python
   list[索引] = 值
   ```

2. 示例代码

   ```python
   cities =['上海','北京','广州']
   cities[0] = '深圳'
   cities[1] = '武汉'
   cities[-1] = '长沙'
   print(cities)

   ['深圳', '武汉', '长沙']
   ```

### 6、其它函数

#### 6.1、len

1. 语法格式

   ```
   len(list)
   ```

2. 说明

   len\(\) 方法返回列表元素个数。

3. 参数

   要计算元素个数的列表

4. 返回值

   返回列表元素个数

5. 示例代码

   ```python
   cities =['上海','北京','广州']
   print(len(cities))

   3
   ```

#### 6.2、list

1. 语法格式

   ```
   list( seq )
   ```

2. 说明

   将元组转换为列表

3. 参数

   要转换为列表的元组

4. 返回值

   返回列表

5. 示例代码

   ```python
   str = 'abcdefjg'
   strs = list(str)
   print(strs)

   ['a', 'b', 'c', 'd', 'e', 'f', 'j', 'g']
   ```

#### 6.3、sort

1. 语法格式

   ```
   list.sort([func])
   ```

2. 说明

   对原列表进行排序，如果指定参数，则使用比较函数指定的比较函数

3. 参数

   如果指定了该参数会使用该参数的方法进行排序

4. 返回值

   该方法没有返回值，但是会对列表的对象进行排序

5. 注意事项

   python3.0不允许不同数据类型进行排序

6. 示例代码

   ```python
   nums = [1,2,1,3,1,5,6,6];
   nums.sort()#默认按照ASCII表先后顺序排序
   #[1, 1, 1, 2, 3, 5, 6, 6]
   print(nums)

   cars = ['Lamborghini','maybach', 'Ferrari',  'Bentley']
   cars.sort(key=len)    # 默认第一原则 字符串从短到长排序，第二原则ASCII表先后顺序
   print(cars) # ['maybach', 'Ferrari', 'Bentley', 'Lamborghini']
   ```

   ```python
   # python3.0不允许不同数据类型进行排序
   a = ['x', 'y', 1, 2]
   a.sort()
   """
   TypeError: '<' not supported between instances of 'int' and 'str'
   """
   ```

#### 6.4、count

1. 语法格式

   ```
   list.count(obj)
   ```

2. 说明

   统计某个元素在列表中出现的次数

3. 参数

   列表中统计的对象

4. 返回值

   返回元素在列表中出现的次数

5. 示例代码

   ```python
   aList = [1,2,1,3,1,5,6,6];
   count = aList.count(1)
   count = aList.count(6)
   print(count)

   3
   2
   ```

### 7、嵌套列表

1. 说明

   嵌套的意思是，列表中的元素也可以是列表。因为列表中的元素可以是任意类型，所以嵌套也是很容易理解的

2. 示例代码

   ```python
   nums = [[1, 2], [3, 4], [20, 10]]
   shops = [['mate10','牛逼',5000.00],['IPhone','装逼',8000.00],['IPhone','傻逼',1000.00]]
   ```

### 8、列表推到

1. 简介

   列表推导，有人也叫列表包含。他提供了一种更加简洁的方式去创建列表。

2. 语法格式

   ```python
   list = [表达式 for 变量 in 列表]
   list = [表达式 for 变量 in 列表 if 条件]
   ```

3. 说明

   会对序列中的每个 item 执行表达式, 然后把满足条件的值存入到一个新的列表中

4. 示例代码

   1、生成list \[1, 2, 3, 4, 5, 6, 7, 8, 9, 10\]可以用list\(range\(1, 11\)\)

   ```
   nums = list(range(1, 11))
   print(nums)  # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   ```

   2、求一个数的3次方

   ```python
   nums = [n**3 for n in range(10)]
   print(nums)
   ```

   3、求30以内能被3整除的数

   ```python
   #示例代码
   multiples = [i for i in range(30) if i % 3 is 0]
   print(multiples)
   [0, 3, 6, 9, 12, 15, 18, 21, 24, 27]
   ```

   4、遍历文件

   ```python
   #常规代码
   import os
   import os
   files = []
   for file in os.listdir('/Users/zhangwei/work/ipython/demo1'):
       if file.endswith('.py'):
           files.append(file)
   print(files)

   简化
   import os
   files = [file for file in os.listdir('/Users/zhangwei/work/ipython/demo1')
               if file.endswith(".py")  ]
   #或者
   import os
   files = [file.endswith(".py") for file in os.listdir("/Users/zhangwei/work/ipython/demo1")]
   ```

   5、推导也支持`for 的嵌套`

   ```python
   s1 = ["a", "b", "c"]
   s2 = [20, 30]

   s3 = [x + str(y) for x in s1 for y in s2]
   print(s3)

   (x, y) for x in range(10) if x % 2 if x > 3 for y in range(10) if y > 7 if y != 8
   ```

```
6、模拟多个掷硬币事件
```

```python
   from random import random
   results = []
   for x in range(10):
       results.append(int(round(random())))
       #简化
       results = [int(round(random())) for x in range(10)]
```

### 9、总结

> | 序号 | 分类 | 关键字/函数/方法 | 说明 |
> | --- | --- | --- | --- |
> | 01 | 增加 | 列表.insert\(索引，数据\) | 在指定位置插入数据 |
> |  |  | 列表.append\(数据\) | 在末尾追加数据 |
> |  |  | 列表.extend\(列表2\) | 将列表2的数据追加到列表 |
> | 02 | 修改 | 列表\[索引\] = 新值 | 修改指定索引的数据 |
> | 03 | 删除 | del 列表\[索引\] | 删除指定索引的数据 |
> |  |  | 列表.remove\[数据\] | 删除第一个出现的指定数据 |
> |  |  | 列表.pop | 删除末尾数据 |
> |  |  | 列表.pop\(索引\) | 删除指定索引数据 |
> |  |  | 列表.clear | 清空列表 |
> | 04 | 统计 | len\(列表\) | 列表长度 |
> |  |  | 列表.count\(数据\) | 数据在列表中出现的次数 |
> | 05 | 排序 | 列表.sort\(\) | 升序排序 |
> |  |  | 列表.sort\(reverse=True\) | 降序排序 |
> |  |  | 列表.reverse\(\) | 逆序，反转 |
> | 06 | 切片 | 列表\[start:end\] |  |

## 三、元组

### 1、简介

1. python 作为一个发展中的语言，也提供了其他的一些数据类型。`tuple`也是 python 中一个标准的序列类型。
2. Python 的元组与列表类似，不同之处在于元组的元素不能修改。
3. 不可变的tuple有什么意义？因为tuple不可变，所以代码更安全。如果可能，能用tuple代替list就尽量用tuple
4. 元组使用小括号，列表使用方括号。
5. 元组创建很简单，只需要在括号中添加元素，并使用逗号隔开即可
6. 如果元组的元素只有一个可以省略不写

### 2、定义元组

#### 2.1、通过\(\)来定义

1. 说明

   元组使用 **\(\)** 定义，用于存储一串信息，使用`comma(逗号)`隔开的多个值就组成了`tuple索引从0开始。(索引就是数据在元组中的位置编号)`

2. 语法格式

   ```python
   tuple = (元素,元素,元素,...)
   ```

3. 结构图

   ![](http://opzv089nq.bkt.clouddn.com/17-12-21/33264806.jpg)

4. 示例代码

   ```python
   t = ()  #空元组
   print(type(t)) # <class 'tuple'>

   t =(1,)  #单个元素元组，注意逗号必须
   print(type(t)) # <class 'tuple'>

   names =('空空','佟亚丽','赵丽颖')
   print(type(names)) # <class 'tuple'>

   t = (‘abs’,(‘def’,’ghi’)) #嵌套元组
   print(type(t)) # <class 'tuple'>

   t = 0,’达康数据’,1.2,3 #四个元素的元组，混合类型,知道就行,不要这么写
   print(type(t)) # <class 'tuple'>
   ```

5. 常见的错误代码

   ```python
   t = (1)
   print(type(t)) # <class 'int'>
   #定义的不是tuple，是1这个数！这是因为括号()既可以表示tuple，又可以表示数学公式中的小括号，这就产生了歧义，因此，Python规定，这种情况下，按小括号进行计算，计算结果自然是1
   #所以，只有1个元素的tuple定义时必须加一个逗号,，来消除歧义

   t1 =('abc')
   print(type(t1)) # <class 'str'>
   ```

#### 2.2、通过tuple\(\)定义

1. 语法格式

   ```python
   t = tuple(seq)
   ```

2. 说明

   将一个序列对象的项转换为元组

3. 参数

   要转换为元组的序列

4. 示例代码

   ```python
   names = ['元素1','元素2','元素3']
   t = tuple(names)
   print(type(t))  #<class 'tuple'>
   print(t) #('元素1', '元素2', '元素3')

   s='123456'
   nums = tuple(s)
   print(nums) # ('1', '2', '3', '4', '5', '6')
   ```

   ```python
   #传入非迭代器会报错
   test = tuple(1)
   """
   TypeError  Traceback (most recent call last)
   <ipython-input-21-8d74e633de98> in <module>()
   ----> 1 test = tuple(1)
   TypeError: 'int' object is not iterable
   """

   test = tuple(1.2,)
   """
   TypeError  Traceback (most recent call last)
   <ipython-input-20-e66128089188> in <module>()
   ----> 1 test = tuple(1.2,)
   TypeError: 'float' object is not iterable
   """
   ```

### 3、获取元素

#### 3.1、通过索引获取

1. 语法格式

   ```python
   tuple[index]
   ```

2. 说明

   index：表示列表中元素的下标\(或者理解为位置，从0开始。到长度-1。不能越界\)

3. 示例代码

   ```python
   tup = ('Python', 'Java', 'H5', 'C++');
   print(tup[0])
   print(tup[-1])#从右边开始取元素
   print(tup[6])#抛出异常
   """
   Traceback (most recent call last):
     File "tup.py", line 5, in <module>
       print(tup[6])
   IndexError: tuple index out of range
   """
   ```

#### 3.2、通过for循环获取

1. 语法格式

   ```python
   for 变量 in 元组:
         # todo
   ```

2. 说明

   跟列表的操作是一样的

3. 示例代码

   ```python
   its = ("Python",'Java',"Android",'IOS')
   for item in its:
       print(item)

   #输出结果    
   Python
   Java
   Android
   IOS
   ```

#### 3.3、通过while循环

1. 语法格式

   ```python
   tup = (元素1,元素2,元素3)
   index = 0
   while index < len(tup):
       tup[index]
       index += 1
   ```

2. 说明

   跟列表的操作是一样的

3. 示例代码

   ```
   its = ("Python",'Java',"Android",'IOS')
   index = 0
   while index < len(its):
       print(its[index])
       index += 1
   ```

### 4、元组的更新

#### 1、添加元组元素

1. 语法格式

   ```
   tup1 = ['元素1','元素2','元素3',...,'元素n']
   tup1 += 序列对象
   ```

2. 说明

   不能操作添加单个元素,通过+号连接序列对象,并且序列对象自动转化成元组

3. 示例代码

   ```python
   #示例代码1
   tup = [1,'happy',['name','sex'],('小花','女'),7-9j]
   tup += (1,1.2)
   print(tup)
   #输出
   """
   [1, 'happy', ['name', 'sex'], ('小花', '女'), (7-9j), 1, 1.2]
   """

   #示例代码2
   tup = [1,'happy',['name','sex'],('小花','女'),7-9j]
   tup += '元素'
   print(tup)

   #输出
   """
   [1, 'happy', ['name', 'sex'], ('小花', '女'), (7-9j), '元', '素']
   """
   #说明 注意+号操作符只能是序列对象,会自动转化成元组,添加至末尾

   #示例代码3
   tup = [1,'happy',['name','sex'],('小花','女'),7-9j]
   tup += [100,200]
   print(tup)
   #输出
   """
   [1, 'happy', ['name', 'sex'], ('小花', '女'), (7-9j), 100, 200]
   """
   ```

   ```python
   tup = [1,'happy',['name','sex'],('小花','女'),7-9j]
   tup += 1

   #抛出异常
   """
   TypeError: 'int' object is not iterable
   """
   ```

#### 2、元组整体合并

1. 语法格式

   ```
   tup = ['元素1','元素2','元素3',...,'元素n']
   tup =tup , 序列对象
   ```

2. 说明

   不能操作添加单个元素,通过,号连接序列对象,并且序列对象自动转化成元组

3. 示例代码

   ```python
   #示例代码1
   tup = [1,'happy',['name','sex'],('小花','女'),7-9j]
   tup = tup,"GG"
   print(tup)
   #输出
   """
   ([1, 'happy', ['name', 'sex'], ('小花', '女'), (7-9j)], 'GG')
   """
   #示例代码2
   tup = tup,[1,False,True]
   #输出
   """
   (([1, 'happy', ['name', 'sex'], ('小花', '女'), (7-9j)], 'GG'), [1, False, True])
   """
   ```

### 5、删除元组

常见元组常量和运算

| 运算 | 解释 |
| --- | --- |
| \(\) | 空元组 |
| T = \(0,\) | 单个元素的元组（非表达式） |
| T = \(0,’NI’,1.2,3\) | 四个元素的元组，混合类型 |
| T = 0,’Ni’,1.2,3 | 四个元素元组，与前列相同 |
| T = \(‘abs’,\(‘def’,’ghi’\)\) | 嵌套元组 |
| T = tuple\(‘spam’\) | 一个可迭代对象的项转换为元组 |
| T\[i\],T\[i\]\[j\],T\[i:j\],len\(T\) | 索引，索引的索引，分片，长度 |
| T1+T2,T \* 3 | 合并，重复\(元素项重复\) |
| for x in T : print\(x\) | 迭代 |
| ‘spam’ in T | 成员关系 |
| \[x \*\* 2 for x in T\] | 列表解析 |
| T.index\(‘Ni’\) | 搜索 |
| T.count\(‘Ni’\) | 计数 |
| sorted\(T\) | 返回一个排序后的列表 |

## 四、字典\(Dictionary\)

### 1、概要

> 字典是Python语言中唯一的映射类型。在其他语言里例如在c语言里叫 联合内存 （ associative memories ）在JavaScript里 联合数组 （ associative arrays \)，在java里就是通常所说的map。
>
> 序列是以连续的整数为索引，与此不同的是，字典以 key为索引，key可以是任意不可变类型，通常用字符串或数值。如果元组中只包含字符串和数字，它可以做为key，如果它直接或间接的包含了可变对象，就不能当做key。不能用列表做关键字，因为列表可以用索引、切割或者 `append()` 和 `extend()` 等方法改变
>
> 理解字典的最佳方式是把它看做无序的键： _值对_ （key:value 对）集合，键必须是互不相同的（在同一个字典之内）。一对大括号创建一个空的字典： `{}` 。初始化列表时，在大括号内放置一组逗号分隔的键：值对，这也是字典输出的方式

### 2、定义字典

1. 语法格式

   ```python
   dict1 = {}
   dict1 = {key1：value1,key2：value2,...}
   ```

2. 方法

   ```python
   dict2 = dict()  # 用函数
   dict2 = dict(key=value,key1=value1,key2=value2)#key必须唯一
   ```

3. 结构图

   ![](http://opzv089nq.bkt.clouddn.com/17-12-30/42136956.jpg)

4. 说明

   * 用大括号声明
   * 键与值用冒号“：”分开；
   * 元素与元素用逗号“，”分开；
   * 字典键key可以是任意不可变类型，通常是数字、字符串甚至是元组，使用格式一创建的字典的时候key可以不唯一（不唯⼀，取最后⼀个值，不建议这样写），使用格式二创建的时候 key必须唯一
   * 值可以是任意类型

5. 示例代码

   ```python
   #格式一初始化
   user = {'name': 'laowang', 'age': 18, 'sex': '男', 'email': '123@163.com'}
   #格式二初始化
   user =dict(name='laowang', age=18, sex=男, email='123@163.com')
   #值其它复杂类型
   user =dict(name=['1',2,'hehe'], age=18, sex=男, email='123@163.com')
   user =dict(address=('北京市','深圳市','武汉市','长沙市'), age=18, sex='男', email='123@163.com')
   ```

```python
   #键不唯一 取最后一个
   user = {ame='呵呵',address=('北京市','深圳市','武汉市','长沙市'),address='上海'}

   user =dict(name='呵呵',address=('北京市','深圳市','武汉市','长沙市',address='上海'))#错误的写法
   print(user.get('address'))
```

### 3、获取键值

1. 语法格式一

   ```python
   dict[key]
   ```

2. 方法

   ```python
   dict.get(key, default=None)
   ```

3. 说明

   通过字典的key取值或者get方法

4. 参数

   * key

     字典中要查找的键。

   * default

     如果指定键的值不存在时，返回该默认值值。

5. 返回值

   返回指定键的值，如果值不在字典中返回默认值None

6. 注意事项

   如果获取不存在的键的值就会触发的一个KeyError异常,字典有一个get方法,可以使用字典get方法更加安全的获取字典

7. 示例代码

   ```python
   user =dict(name='呵呵',address=('北京市','深圳市','武汉市','长沙市'),age=18, sex='男', email='123@163.com')
   print(user['name'])
   print(user['aaa']) #直接抛出异常
   print(user.get('address'))#输出元组
   print(user.get('aaa')) #输出None
   print(user.get('aaa','name'))#dict.get(key, default=None)则如果不存在则返回一个默认值，如果设置了则是设置的，否则就是None
   ```

   ```
   In [22]: user =dict(name='呵呵',address=('北京市','深圳市','武汉市','长沙市'),age=18, sex='男', email='12 3@163.com')

   In [23]: user['name']
   Out[23]: '呵呵'

   In [24]: user['aaa']
   ---------------------------------------------------------------------------
   KeyError                                  Traceback (most recent call last)
   <ipython-input-24-d3b16260a8cd> in <module>()
   ----> 1 user['aaa']
   KeyError: 'aaa'
   ```

### 4、更新/添加

1. 语法格式

   ```python
   dict[key] = value
   ```

2. 方法

   ```python
   dict.update(dict2)
   ```

3. 说明

   字典dict2的键/值对更新到dict里

4. 参数说明

   * dict2

     添加到指定字典dict里的字典

5. 示例代码

   ```python
   user= dict()
   user['name'] = '空空'
   user['age'] = 18 
   user[1] = 2
   print(user)
   ```

   ```python
   user= dict()
   user1=dict(name='呵呵',address=('北京市','深圳市','武汉市','长沙市'),age=18, sex='男', email='123@163.com')
   user.update(user1)

   user.update(phone='110',state=1)#推荐写法

   print(user)
   ```

### 5、字典删除

1. 语法格式一\(不推荐\)

   ```python
   del dict[key] 
   #无返回值
   ```

2. 方法

   ```python
   dict.pop(key[,default])
   ```

3. 说明

   删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。 否则，返回default值。

4. 参数

   * key:

     要删除的键值

   * default: 如果key不存在，返回 default 值

5. 返回值

   返回被删除的值

6. 示例代码

   ```python
   user=dict(name='呵呵',address=('北京市','深圳市','武汉市','长沙市'),age=18, sex='男', email='123@163.com')
   del user['name']
   print(user)
   #输出
   {'address': ('北京市', '深圳市', '武汉市', '长沙市'), 'age': 18, 'sex': '男', 'email': '123@163.com'}
   ```

   ```python
   user=dict(name='呵呵',address=('北京市','深圳市','武汉市','长沙市'),age=18, sex='男', email='123@163.com')
   name = user.pop('name')
   print(name) #输出 '呵呵'
   key = user.pop('sex','test') #字典存在,返回'男'
   print(key) # '男'
   key = user.pop('key','111') #字典不存在,返回'111'
   print(key)# '111'
   ```

### 6、遍历元组

#### 6.1 、遍历所有的key

1. 语法格式

   ```python
   dict_keys = dict.keys()
   ```

2. 说明

   获取所有的key

3. 返回值

   以列表返回一个字典所有的键

4. 示例代码

   ```python
   user=dict(name='呵呵',address=('北京市','深圳市','武汉市','长沙市'),age=18, sex='男', email='123@163.com')
   user_keys = user.keys()#输出 dict_keys(['name', 'address', 'age', 'sex', 'email'])
   for user_key in user_keys:
       print(user_key)
       #输出
       name
       address
       age
       sex
       email
   ```

#### 6.2、遍历所有的value

1. 方法

   ```python
   dict_values = dict.values()
   ```

2. 说明

   以列表返回字典中的所有值

3. 返回值

   返回字典中的所有值

4. 示例代码

   ```python
   dict_values(['呵呵', ('北京市', '深圳市', '武汉市', '长沙市'), 18, '男', '123@163.com'])user = dict(name='呵呵', address=('北京市', '深圳市', '武汉市', '长沙市'), age=18, sex='男', email='123@163.com')

   dict_values = user.values()
   print(dict_values)#输出 dict_values(['呵呵', ('北京市', '深圳市', '武汉市', '长沙市'), 18, '男', '123@163.com'])

   for value in dict_values:
       print(value)
       #输出
       呵呵
       ('北京市', '深圳市', '武汉市', '长沙市')
       18
       男
       123@163.com
   ```

#### 6.3、遍历所有的value

1. 方法

   ```python
   dict_items = dict.items()
   ```

2. 说明

   以列表返回可遍历的\(键, 值\) 元组数组

3. 返回值

   返回可遍历的\(键, 值\) 元组数组。

4. 注意事项

   字典元素的顺序通常没有定义。换句话说，迭代的时候，字典中的键和值都能保证被处理，但是处理顺序不确定。如果顺序很重要的话，可以将键值保存在单独的列表中，例如迭代前进行排序

5. 示例代码

   ```python
   user = dict(name='呵呵', address=('北京市', '深圳市', '武汉市', '长沙市'), age=18, sex='男', email='123@163.com')

   user_item = user.items()

   print(user_item)

   #dict_items([('name', '呵呵'), ('address', ('北京市', '深圳市', '武汉市', '长沙市')), ('age', 18), ('sex', '男'), ('email', '123@163.com')])
   ```

   ```python
   user = dict(name='呵呵', address=('北京市', '深圳市', '武汉市', '长沙市'), age=18, sex='男', email='123@163.com')
   user_items = user.items()
   for key, value in user_items:
       print("%s=" % key, value)

       #输出
       name= 呵呵
       address= ('北京市', '深圳市', '武汉市', '长沙市')
       age= 18
       sex= 男
       email= 123@163.com
   ```

   ```python
   user = dict(name='呵呵', address=('北京市', '深圳市', '武汉市', '长沙市'), age=18, sex='男', email='123@163.com')
   user_items = user.items()
   keys=[]
   values=[]
   for key, value in user_items:
      keys.append(key)
      values.append(value)
   ```

6. 练习

   编写字典程序:

   * 用户添加单词和定义
   * 查找这些单词
   * 如果查不到，请让用户知道
   * 循环

   ```python
   dictionary = {}
   flag = 'a'
   pape = 'a'
   off = 'a'
   while flag == 'a' or 'c' :
       flag = raw_input("添加或查找单词 ?(a/c)")
       if flag == "a" :                             # 开启
           word = raw_input("输入单词(key):")
           defintion = raw_input("输入定义值(value):")
           dictionary[str(word)] = str(defintion)  # 添加字典
           print "添加成功!"
           pape = raw_input("您是否要查找字典?(a/0)")   #read
           if pape == 'a':
               print dictionary
           else :
               continue
       elif flag == 'c':
           check_word = raw_input("要查找的单词:")  # 检索
           for key in sorted(dictionary.keys()):            # yes
               if str(check_word) == key:
                   print "该单词存在! " ,key, dictionary[key]
                   break
               else:                                       # no
                   off = 'b'
           if off == 'b':
               print "抱歉，该值不存在！"
       else:                               # 停止
           print "error type"
           break
   ```

### 7、其它方法

#### 7.1、 fromkeys

字典类型与序列类型的区别：

1. 存取和访问数据的方式不同。
2. 序列类型只用数字类型的键（从序列的开始按数值顺序索引）；
3. 映射类型可以用其他对象类型作键（如：数字、字符串、元祖，一般用字符串作键），和序列类型的键不同，映射类型的键直4.接或间接地和存储数据值相关联。
4. 映射类型中的数据是无序排列的。这和序列类型是不一样的，序列类型是以数值序排列的。
5. 映射类型用键直接“映射”到值。

## 五、集合



