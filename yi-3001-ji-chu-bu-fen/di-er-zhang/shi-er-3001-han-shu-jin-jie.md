# 函数进阶

## 一、作用域

### 1、概要

> 有了函数之后，我们必须要面对一个作用域的问题。比如：你现在访问一个变量，那么 python 解析器是怎么查找到这个变量，并读取到这个变量的值的呢？ 依靠的就是作用域规则！

### 2、概念

#### 2.1、命名空间（namespace）

1. 定义

> A _namespace_ is a mapping from names to objects
>
> 命名空间是名字和对象的映射。也就是可以把一个namespace理解为一个字典，实际上很多当前的Python实现namespace就是用的字典。各个命名空间是独立的，没有任何关系的，所以一个命名空间中不能有重名，但不同的命名空间是可以重名而没有任何影响。
>
> 命名空间表示变量的可见范围，一个变量名可以定义在多个不同的命名空间，相互之间并不冲突，但同一个命名空间中不能有两个相同的变量名。比如：两个叫“张三”的学生可以同时存在于班级A和班级B中，如果两个张三都是一个班级，那么带来的麻烦复杂很多了，在Python中你不能这么干。

1. 命名空间的种类\(2.2以前三种,2.2四种\)

   * 局部，函数内的命名空间就是局部的\(函数内部声明但没有使用global的变量\)—&gt;local；
   * 全局，模块内\(.py文件内\)的命名空间就是全局的—&gt;global；
   * 内置，包括异常类型、内建函数和特殊方法，可以代码中任意地方调用—&gt;built-in；
   * 闭包，嵌套的父级函数的局部作用域，即包含此函数的上级函数的局部作用域，但不是全局的\(闭包函数外的函数中 \)—&gt;enclosing

2. 作用范围结构图

   ![](http://opzv089nq.bkt.clouddn.com/18-1-13/23830955.jpg)

3. 举个栗子1

   * 局部

     ```python
     #test.py
     def fun():
         """
         局部作用域
         """
         name = '吃鸡'
           print(name)
     if __name__ == '__main__':
         fun()
         print(name)#程序出错
     ```

   * 全局

     ```python
     #demo1.py
     txt = '大吉大利,今晚吃鸡'
     print(txt)
     #demo2.py
     print(txt)#程序出错
     ```

   * 系统内置

     ```python
     #vars()查看内置全局变量
     """
     全局作用域2
     """
     print(vars)
     if __name__ == '__main__':
         print(__doc__)
         print(__file__)
            print(__package__)
     ```

   * 闭包

     ```python
     def outer():
         num = 200  # 闭包作用域
         def inner():
             num = 300 # 本地作用域
             return num
         return inner
     print outer()() # 输出300
     ```

4. 举个栗子2

   * 栗子1

     ```python
     num = 0
     def fun():
         num = num + 1
         print(num)
     if __name__ == '__main__':
          fun()
     ```

     代码分析

     运行结果

     ![](http://opzv089nq.bkt.clouddn.com/18-1-13/27861516.jpg)

     1、通过控制台的错误提示,本地变量“num”在使用之前未被赋值

     2、num + 1中的num是个本地变量, 本地变量,本地变量。python解释器在函数运行时,num = 相当于声明了一个本地变量num ，而num+1解释器先会从本地作用域中查找，所以虽然你在全局中定义了,通过上面的知识不能理解

     3、所以在使用变量前一定要赋值

   * 栗子2

     ```python
     name = '小明'
     def ex_global():
         # 这里是新创建了一个局部变量name .并不是修改的全局作用域的变量name
         name = '小花'
         print(name)

     if __name__ == '__main__':
         ex_global()
         print(name)
         #输出结果  小花 小明
     ```

     代码分析

     1、运行程序在全局作用域中声明了一个name内存中的值是'小明'

     2、执行函数ex\_global\(\)在本地作用域声明又声明了一个name的变量值是'小花'

     3、调用函数print\(\),根据上面说的作用域的查找顺序可以知道先从本地作用域查找,所以第一次输出结果是小花

     4、此时方法执行完毕,执行第二个print\(name\)由于前面学过的作用域可以知道第二个name变量只会在全局作用域中查找,所以输出小明

5. 总结
   * 在局部命名空间处，全局命名空间的同名变量是不可见的（只有变量不同名的情况下，可使用 global关键字让其可见）
   * 闭包函数外的函数中
   * 全局命名空间和局部命名空间中， 如果有同名变量，在全局命名空间处，局部命名空间内的同名变量是不可见的
   * 内置命名空间在代码所有位置都是可见的，所以可以随时被调用

#### 2.2、作用域（scope）

> A _scope_ is a textual region of a Python program where a namespace is directly accessible.
>
> 作用域是Python程序（文本）的某一段或某些段，在这些地方，某个命名空间中的名字可以被直接引用。
>
> 简单说就是一个变量的命名空间。代码中变量被赋值的位置，就决定了哪些范围的对象可以访问这个变量，这个范围就是命名空间。python赋值时生成了变量名，当然作用域也包括在内。
>
> 简单的来说就是命名空间的可见性

#### 2.3、查找顺序

1. 查找顺序结构图

   ![](http://opzv089nq.bkt.clouddn.com/18-1-13/29261200.jpg)

2. 说明

   * 如果在函数内调用一个变量，先在函数内（局部命名空间）查找，如果找到则停止查找。否则在函数外部（全局命名空间）查找，如果还是没找到，则查找内置命名空间。如果以上三个命名都未找到，则抛出NameError 的异常错误。

3. 如果在函数外调用一个变量，则在函数外查找（全局命名空间，局部命名空间此时不可见），如果找到则停止查找，否则到内置命名空间中查找。如果两者都找不到，则抛出异常。只有当局部命名空间内，使用global 关键字声明了一个变量时，查找顺序则是上面的查找顺序

#### 2.4、其它

##### 1、块级作用域\(语法块\)

1. 想想此时运行下面的程序会有输出吗？执行会成功吗？

   ```python
   #块级作用域 
   if 1 == 1:    
     name = "hehe"   
   print(name)  

   for i in range(10):   
       age = i  
   print(age)
   ```

2. 说明

   代码执行成功，没有问题；在Java/C\#中，执行上面的代码会提示name，age没有定义，而在Python中可以执行成功，这是因为在Python中是没有块级作用域的，代码块里的变量，外部可以调用，所以可运行成功；

##### 2、局部作用域

1. 数是个单独的作用域，Python中没有块级作用域，但是有局部作用域

   ```python
   def  fun():
       name = "hehe"
   print(name)
   ```

2. 说明

   ```
   Traceback (most recent call last):
     File "xxx/xxx/xx.py", line 3, in <module>
       print(name)
   NameError: name 'name' is not defined
   ```

   代码运行出错

### 3、global和nonlocal

#### 1、global

1. 说明

   global语句用来声明一系列变量，这些变量会引用到当前模块的全局命名空间的变量,在函数体外声明的默认就是global

2. 举个栗子

   * 栗子1

     ```python
     num = 0
     def fun():
          global num
          num = num + 1
          print(num)

     if __name__ == '__main__':
          fun()
     ```

     代码分析

     运行结果

     ![](http://opzv089nq.bkt.clouddn.com/18-1-13/27861516.jpg)

     1、通过控制台的错误提示,本地变量“num”在使用之前未被赋值

     2、num + 1中的num是个本地变量, 本地变量,本地变量。python解释器在函数运行时,num = 相当于声明了一个本地变量num ，而num+1解释器先会从本地作用域中查找，所以虽然你在全局中定义了,通过上面的知识不能理解

     3、所以在使用变量前一定要赋值

3. 栗子2

   ```python
   name = '小明'
   def ex_global():
        # 这里是新创建了一个局部变量name 
        # 并不是修改的全局作用域的变量name
        name = '小花'
        print(name)
    if __name__ == '__main__':
        ex_global()
        print(name)
        #输出结果  小花 小明
   ```

   代码分析

   1、运行程序在全局作用域中声明了一个name内存中的值是'小明'

   2、执行函数ex\_global\(\)在本地作用域声明又声明了一个name的变量值是'小花'

   3、调用函数print\(\),根据上面说的作用域的查找顺序可以知道先从本地作用域查找,所以第一次输出结果是小花

   4、此时方法执行完毕,执行第二个print\(name\)由于前面学过的作用域可以知道第二个name变量只会在全局作用域中查找,所以输出小明

#### 2、nonlocal\(Python3.2引入的\)

1. 说明

   用来在函数或其他作用域中使用外层\(非全局\)变量

2. 举个栗子

   * 栗子1

     ```python
     def outer():
         num = 1
         def inner():
             # 把 num 绑定到外部函数的局部变量 num 上
             nonlocal num
             num = 2
             print("inner:", num)
         inner()
         print("outer:", num)
     if __name__ == '__main__':
         outer()
     ```

     代码分析

     1、outer\(\)函数执行

     2、定义一个局部变量 num 并且赋值1

     3、执行inner函数，把 num 绑定到外部函数的局部变量 num 上

     4、赋值num为2,所以第一个print\(\)函数在控制台输出2,函数执行完毕

     5、执行第二个print\(\)方法，由于上一步可以知道,num=2，所以也是输出2，代码执行完毕

### 4、综合栗子

1. 栗子1

   ```python
   def scope_complex():
       def ex_local():
            # 此函数定义了另外的一个var字符串变量，并且生命周期只在此函数内。
            # 此处的var和外层的var是两个变量，
           var = "本地作用域2" 

       def ex_nonlocal():
           nonlocal var  #使用外层的var变量
           var = "闭包作用域"

       def ex_global():
           global var
           var = "全局作用域"

       var = "局部作用域1"

       ex_local()
       print(var)

       ex_nonlocal()
       print(var)

       ex_global()
       print(var)

   scope_complex()                   
   print(var)
   ```

   代码分析

   1、执行函数 scope\_complex\(\) ，定义局部变量 var = "局部作用域1"

   2、执行函数ex\_local\(\) ，定义局部变量var = "本地作用域2" ，作用范围仅仅ex\_local函数中

   3、执行函数print\(var\) ，输出的第一步定义的局部变量,而不是第二步定义的局部变量

   4、执行函数ex\_nonlocal\(\)，将var变量绑定在第一步定义的变量上，讲var的值改为"闭包作用域"

   5、执行函数print\(var\)，输出"闭包作用域"

   6、执行函数ex\_global\(\)，声明全局变量var赋值"全局作用域"

   7、执行函数print\(var\)，先从本地函数作用域查找,所有输出还是"闭包作用域",

   8、scope\_complex\(\)  执行完成

   9、执行函数print\(var\),从本地作用域中查找,由于在第七步声明了var，所以输出"全局作用域"

2. 栗子2

   ```python
   def test():
     def ex_nonlocal():
       def ex_nonlocal2():
         nonlocal var
         var = "闭包变量"

         ex_nonlocal2()

         var = "局部变量"
         ex_nonlocal()
         print(var)
   if __name__ == '__main__':
       test()
   ```

### 5、作用链

#### 1、说明

​    变量会由内到外找，先去自己作用域去找，自己没有再去上级去找，直到找不到报错,形成一条链

#### 2、举个栗子

1. 栗子1

   ```python
   name = "小明"

   def fun1():
       name = "小花"

       def func2():
           name = "老王"
           print(name)

       func2()

   if __name__ == '__main__':   
      fun1()
      #输出老王
   ```

2. 栗子2

   ```python
   name = "小明"
   def fun1():
       print(name)

   def fun2():   
       name = "小花"
       return fun1 

   chain = fun2()

   if __name__ == '__main__':
       chain()
   ```

   代码分析

   1、chain\(\)相当执行fun2\(\)函数返回的fun1\(\)的内存地址,即chain=f1执行chain\(\)相当于执行fun1\(\)

   2、执行fun1\(\)时与fun2\(\)没有任何关系，name = "小明"与fun1在一个作用域链，所以输出的是"小明"

### 6、总结

能改变作用域的

1. python能够改变变量作用域的代码段是def、class、lamda
2. if/elif/else、try/except/finally、for/while 并不能涉及变量作用域的更改，也就是说他们的代码块中的变量，在外部也是可以访问的

## 二、lambda表达式\(匿名函数\)

### 1、概念

> lambda函数也叫匿名函数，即，函数没有具体的名称
>
> ```python
> def multip(x):  
>     return x * 2  
>
> lam = lambda x : x * 2  
>
> print(multip(2))
> print(lam(2))
> ```
>
> 运行完成之后的结果都是6,通过结果我们可以知道，lambda在Python这种动态的语言中确实没有起到什么特别大的作用，因为有很多别的方法能够代替lambda，所以python对 ambda有比较简单有限的支持
>
> 简单来说好比电影里面的群众演员，往往他们的戏份很少，最多是衬托主演，跑跑龙套\(出来就死的那种\)，他们需要名字吗？不需要，因为他们仅仅只是临时出镜，下次可能就用不着了，所以犯不着费心思给他们每个人编个号取个名字，毕竟取个优雅的名字是很费劲的事情

### 2、为什么要使用lambda

> 通过上面的代码，我们会发现
>
> 1. lambda简化了函数定义的书写形式。是代码更为简洁，但是使用函数的定义方式更为直观，易理解。
> 2. 对于一些抽象的，不会别的地方再复用的函数，有时候给函数起个名字也是个难题，使用lambda不需要考虑命名的问题

### 3、语法格式

> ```python
> lambda 形参列表 : 表达式
> ```
>
> 说明
>
> 1. 关键字`lambda`后面紧跟着形参列表. 注意形参列表不能用圆括号括起来
> 2. 形参列表后面紧跟着一个冒号\(`:`\)
> 3. 冒号后面是唯一的表达式. 注意:此表达式必须是合法的表达式.
> 4. `lambda`会自动返回表达式的运算结果
>
> 注意事项
>
> 1. lambda 表达式只是对简单到只有一行代码的函数的语法糖\(简写\), 如果有多行代码, 则无法使用 lambda 表达式
>
> 2. lambda 函数可以接收任意多个参数 \(包括可选参数\) 并且返回单个表达式的值
>
> 3. lambda用来编写简单的函数，而def用来处理更强大的任务
>
>    ​

### 4、示例代码

1. 无参

   ```python
   #函数名为fun
   def fun():
     return Ture  
   #无参数 无函数名
   lambda : Ture
   ```

2. 位置参数

   ```python
   m = lambda x,y,z: x*y*z
   print(m(2,3,4))
   ```

3. 关键字参数

   ```python
   #函数
   def add(x,y=2)
       return x + y
   #lambda表达式
   add = lambda x,y=2: x+y
   print(add(10))
   ```

4. 不定长参数,返回元组

   ```python
   #函数定义
   def fun(*args):
       return args
   #表达式
   a = lambda *z: z

   if __name__ == '__main__':
       print(a(1, 2, 3, 4, '姓名'))
   ```

5. 不定长参数,返回字典

   ```python
   # 函数
   def fun_kwargs(**kwargs):
       return kwargs

   # 表达式
   c = lambda **kwargs: kwargs

   if __name__ == '__main__':
       print(c(arg1=1, arg2=1, arg3='姓名'))
   ```

6. 直接后面传递实参

   ```python
   if __name__ == '__main__':
       print((lambda x, y: x if x > y else y)(100, 200))
       print((lambda x: x ** 10)(2))
   ```

7. 配合函数使用

   ```python
   def say(name, content):
       return (lambda name, content: name + 'say: ' + content)(name, content)

   if __name__ == '__main__':
       print(say('小明', 'Hello World'))
   ```

   ​

### 5、结合内置函数

#### 5.1、说明

>

#### 5.2、map

1. 说明

   对一个及多个序列执行同一个操作，返回一个列表

2. 语法格式

   ```python
   map(func, *iterables)
   ```

3. 结构图

   ​

4. 参数说明

   * 参数1: 函数,不能为None

5. 参数2: sequence,序列

6. 返回值

   * 返回map对象

7. 注意

   返回一个新的迭代对象,不会对原来的序列有影响

8. 举个栗子

   * 基本使用

     ```python
     li = [1, 2, 3, 4, 5]
     iter1 = map(lambda x: x * 2, [1, 2, 3, 4, 5])

     if __name__ == '__main__':
         print(li)
         print(list(iter1))
     ```

   * 元组和列表配合使用

     ```python
     #注意 传入两个可迭代对象，所以传入的函数必须能接收2个参数
     iter2 = map(lambda x, y: x + y, [1, 2, 3, 4], (10, 20, 30, 40))
     if __name__ == '__main__':
         print(tuple(iter2))
     ```

   * 当传入多个可迭代对象时，且它们元素长度不一致时，生成的迭代器只到最短长度

     ```
     iter3 = map(lambda x, y: x + y if y else x + 10, [1, 2, 3, 4, 5], (1, 2, 3, 4))
     if __name__ == '__main__':
         print(tuple(iter3))
         # 输出(2, 4, 6, 8)
     ```

   * 结合函数使用

     ```python
     nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]
     def fun(x):
         return x * x

     if __name__ == '__main__':
         print(list(map(fun, nums)))
     ```

#### 5.3、filter

1. 说明

   对于序列中的元素进行筛选，最终获取符合条件的序列，相当于一个迭代器，调用一个布尔函数func来迭代seq中的每个元素，返回一个是bool\_seq返回为True的序列

2. 语法格式

   ```python
   list[, tuple, str] = filter(function or None, sequence)
   ```

3. 结构图

   ​

4. 参数说明

   * 参数1: function or None, 函数或None

5. 参数2: sequence,序列

6. 返回值

   * 如果参数为function,那么返回条件为真的序列\(列表，元祖或字符串\)
   * 如果参数为None的话,那么返回序列中所有为True的项目

7. 举个栗子

   * 要过滤掉所有值为False的列表

     ```python
     li = [1, 0, 0.0, None, {}]

     if __name__ == '__main__':
         print(filter(None, [-2, 0, 2, '', {}, ()]))
     ```

   * 过滤字母\(字符串\)

     ```python
     filter(lambda x: x !='a','abcd')
     if __name__ == '__main__':
         print(filter(None, [-2, 0, 2, '', {}, ()]))
     ```

   * 过滤元素\(列表\)

     ```python
     names = ['老宋','老王','小张','小花','小明',''] 

     if __name__ == '__main__':
         # f_names = filter(lambda name: name != '', names)
         # 等价
         f_names = filter(None, names)
         for name in f_names:
             print(name)
     ```

   * 过滤列表中的奇数

     ```python
     nums = [0,101,10,7,3,5,8,131,88] 
     if __name__ == '__main__':
       filter(lambda x: x%2, nums)
     ```

   * 将2-10间所有质数列出来

     ```python
     if __name__ == '__main__':
         filter(lambda x: not [x for i in range(2,x) if x%i == 0],range(2,10))
     ```

   * 过滤所有子列表中，元素是'IPhone'

     ```python
     def filter_shop(shop):  
         if shop:
             return shop != 'IPhone'
         else:return False
     shops = [['huawei', 'Iphone', 'xiaomi'], ['Iphone', 'meizu','vivo']]

     if __name__ == '__main__':
        filter(fitler_shop(shop)) for shop in shops
     ```

   * 过滤文件

     ```python
     #需要的模块  
     import os                               
     #列出需要查找的目录的所有文
     files = os.listdir('D:\work\Demo') 
     if __name__ == '__mian__':
         print(filter(lambda file: file.endWith('.py'),files))
     ```

     ​

   * 底层实现

     ```python
     def filter(func,seq):
         #建一个空序列，用于存储过滤后的元素
         f_seq = []
         #对序列中的每个元素进行迭代
         for item in seq:    
             #如果为真的话
             if func(item): 
                   #满足条件者，则加入
                 f_seq.append(item)  
         #返回过滤后的元素          
         return f_seq
     ```

#### 5.4、reduce

1. 说明

   reduce函数会对参数序列中元素进行累积。

   在Python 3里,reduce\(\)函数已经被从全局名字空间里移除了,它现在被放置在fucntools模块里 用的话要 先引入。

2. 语法

   ```python
   reduce(function, sequence, initial=None)
   ```

3. 参数说明

   * 参数一  处理序列的函数
   * 参数二  序列对象
   * 参数三  第一次调用的参数

4. 返回值

   函数处理过的对象

5. 备注

   function有三个参数，reduce依次从sequence中取一个元素，和上一次调用function的结果做参数再次调用function。 第一次调用function时，如果提供initial参数，会以sequence中的第一个元素和initial作为参数调用function，否则会以序列sequence中的前两个元素做参数调用function

6. 举个栗子

   * 对字符串的处理

     ```python
     value1 = reduce(lambda x, y: x + y,['hello', 'word'])
     if __name__ == '__main__':
         print(value1)
     ```

   * 两个参数的数字类型处理

     ```python
     value2 = reduce(lambda x, y: x * y, [1, 2, 3, 4])
     if __name__ == '__main__':
         print(value2)
     ```

   * func\(\)函数不能为None,否则报错

     ```python
     reduce(None,[1,2,3,4])
     '''
      Traceback (most recent call last):
        File "/Users/zhangwei/work/PycharmProjects/Demo/day05/src/lambda_reduce.py", line 12, in <module>
          print(reduce(None,[1,2,3,4])  )
      TypeError: 'NoneType' object is not callable
     '''
     ```

   * func(x,y)只能有两个参数，否则报错

     ```python
     print(reduce(lambda x: x * 2, [1, 2, 3, 4], 10))
     '''
       Traceback (most recent call last):
         File "/Users/zhangwei/work/PycharmProjects/Demo/day05/src/lambda_reduce.py", line 12, in <module>
        print(reduce(lambda x: x * 2, [1, 2, 3, 4], 10))
       TypeError: <lambda>() takes 1 positional argument but 2 were given
       '''
     ```

   * 底层实现

     ```python
     def reduce(function, iterable, initializer=None):
         it = iter(iterable)
         if initializer is None:
             value = next(it)
         else:
             value = initializer
         for element in it:
             value = function(value, element)
             return value
     ```

## 三、闭包

### 1、闭包的概念

> 在一些语言中，在函数中可以（嵌套）定义另一个函数时，如果内部的函数引用了外部的函数的变量，则可能产生闭包。闭包可以用来在一个函数与一组“私有”变量之间创建关联关系。在给定函数被多次调用的过程中，这些私有变量能够保持其持久性。闭包就是能够读取其他函数内部变量的函数。在本质上，闭包是将函数内部和函数外部连接起来的桥梁
>
> 用比较容易懂的人话说，就是当某个函数被当成对象返回时，夹带了外部变量，就形成了一个闭包,例如:
>
> ```python
> def parent():
>     msg = '局部变量'
>     def child():
>         print(msg)  # 外部变量
>     return child  # 返回的是函数，带外部变量的
>
> if __name__ == '__main__':
>     p = parent()
>     p()
>
> ```

### 2、闭包的用途

> 包可以用在许多地方。它的最大用处有两个，一个是可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中，不会在父调用后被自动清除。
>
> 为什么会这样呢？原因就在于parent是child的父函数，而child被赋给了一个全局变量，这导致child始终在内存中，而child的存在依赖于parent，因此parent也始终在内存中，不会在调用结束后，被垃圾回收机制（garbage collection）回收。

### 3 举个栗子

1. 栗子1\(惰性求值\)

   \`\`\`  
   def foo\(msg\):  
       def say\(\):  
           print\("hello" + str\(msg\)\)  
       return say  
   say = foo\("志玲"\)  
   say\(\)

    2. 栗子2(使用闭包保持状态)

       ```python
       def count_down(num):
           def next():
               nonlocal num
               temp = num
               num -= 1
               return temp
           return next

       if __name__ == '__main__':
           n = count_down(10)
           while True:
               # 每调用一次就会减少一次计数
               value = n()
               print(value)
               if value == 0:
                   break
       ```

   3. 栗子3

      ```python
      """
      比如，如果你希望函数的每次执行结果，都是基于这个函数上次的运行结果。我以一个类似棋盘游戏的例子来说明。假设棋盘大小为50*50，左上角为坐标系原点(0,0)，我需要一个函数，接收2个参数，分别为方向(direction)，步长(step)，该函数控制棋子的运动。棋子运动的新的坐标除了依赖于方向和步长以外，当然还要根据原来所处的坐标点，用闭包就可以保持住这个棋子原来所处的坐标。
      """

      origin = [0, 0]  # 坐标系统原点  
      legal_x = [0, 50]  # x轴方向的合法坐标  
      legal_y = [0, 50]  # y轴方向的合法坐标  
      def create(pos=origin):  
          def player(direction,step):  
              # 这里应该首先判断参数direction,step的合法性，比如direction不能斜着走，step不能为负等  
              # 然后还要对新生成的x，y坐标的合法性进行判断处理，这里主要是想介绍闭包，  
              new_x = pos[0] + direction[0]*step  
              new_y = pos[1] + direction[1]*step  
              pos[0] = new_x  
              pos[1] = new_y  
              #注意！此处不能写成 pos = [new_x, new_y]，  
              return pos  
          return player  

      player = create()  # 创建棋子player，起点为原点  
      print player([1,0],10)  # 向x轴正方向移动10步  
      print player([0,1],20)  # 向y轴正方向移动20步  
      print player([-1,0],10)  # 向x轴负方向移动10步
      ```

### 5、使用闭包的注意点

1. 由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。
2. 闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。

## 四、装饰器\(Decorator\)

### 1、前期基础

#### 1.1、高阶函数

1. 说明

2. 把一个函数名当做形实传给另外一个函数\(不修改被装饰的函数源代码的情况下为其添加功能\)

3. 返回值中包含函数名\(返回值中包含函数名（不修改函数的调用方式）\)

4. 举个栗子

   1. 把函数作为参数传递

      ```python
      def fun():
          print("这个是一个函数")

      def test1(func):
          print(func)

      test1(fun)
      ```

   2. 在函数前面添加代码

      ```python
      def fun():
          print("核心代码")

      def test1(func):
          print('在原始核心代码之前添加功能')
          func()
          print('在原始核心代码之后添加功能')
      if __name__ == '__main__':
          test1(fun)

      #缺点调用方式发生改变，不能像原来的方法去调用被修饰的函数
      ```

   3. 返回值中包含函数名\(不修改函数的调用方式\)

      ```python
      def bar():
          print("核心代码")
      def test3(func):
          print('在原始核心代码之前添加功能')
          return func
      if __name__ == '__main__':
          bar = test3(bar)
          bar()
      ```

#### 1.2、嵌套函数

1. 说明

   在一个函数体内，用def去声明一个函数

2. 举个栗子

   * 栗子1\(函数嵌套\)

     ```python
     def foo():
         print("在核心代码之前调用")
         def bar():
             print("核心代码")
         bar()
     if __name__ == '__main__':
         foo()
     ```

   * 栗子2\(函数调用\)

     ```python
     #注意两者之间的区别
     def foo():
         print("in the foo")
     def bar():
         print("in the bar")
         bar()
     if __name__ == '__main__':
         foo()
     ```

### 2、什么是装饰器

> 装饰器本质上是一个Python函数，它可以让其他函数在不需要做任何代码变动的前提下增加额外功能，装饰器的返回值也是一个函数对象。它经常用于有切面需求的场景，比如：插入日志、性能测试、事务处理、缓存、权限校验等场景。装饰器是解决这类问题的绝佳设计，有了装饰器，我们就可以抽离出大量与函数功能本身无关的雷同代码并继续重用。概括的讲，装饰器的作用就是为已经存在的对象添加额外的功能,也是闭包的一种应用场景
>
> 装饰器 = 高阶函数 + 嵌套函数

### 3、作用

> 为其他函数添加附加功能

### 4、原则

> 不能修改被装饰的函数的源代码，不能修改被装饰的函数的调用方式。
>
> 即：装饰器对待被修饰的函数是完全透明的。

### 5、定义装饰器

1. 定义

   ```python
   def strong(fun):  # fun 将来就是被替换的 hello
       def new_hello():
           print("我是装饰器中的代码, 在 hello 之前执行的")
           fun()
           print("我是装饰器中的代码, 在 hello 之后...执行的")

       return new_hello

   @strong
   def hello():
       print("我是 hello 函数中的代码")   

   if __name__ == '__main__':
       # 这里调用的其实是装饰器返回的函数.
       hello()
   ```

2. 说明
   * 在需要添加的装饰函数上面一行使用`@`来添加装饰器
   * `@`后面紧跟中装饰器名`strong`, 当然你可以定于任何的名字.
   * `strong`是装饰器, 本质上是一个函数. 他接收函数`hello`作为参数, 并返回一函数来替换掉`hello`\(当然也可以不替换\).
   * `hello`使用装饰器之后, 相当于`hello`函数使用下面的代码被替换掉了`hello = strong(hello)`
   * 在调用`hello`的时候, 其实是调用的`strong()`返回的那个函数.
3. 满足以下条件
   * 装饰器函数运行在函数定义的时候 
   * 装饰器需要返回一个可执行的对象 
   * 装饰器返回的可执行对象要兼容函数的参数

## 五、附

1. 语法糖

   就相当于汉语里的成语。即，用更简练的言语表达较复杂的含义。指计算机语言中添加的某种语法，这种语法对语言的功能并没有影响，但是更方便程序员使用。通常来说使用语法糖能够增加程序的可读性，从而减少程序代码出错的机会，例如5\*5等同于5+5+5+5+5

## 



