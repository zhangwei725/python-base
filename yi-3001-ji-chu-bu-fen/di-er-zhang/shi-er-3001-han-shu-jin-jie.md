# 函数进阶

## 一、作用域

### 1、概要

> 有了函数之后，我们必须要面对一个作用域的问题。比如：你现在访问一个变量，那么 python 解析器是怎么查找到这个变量，并读取到这个变量的值的呢？ 依靠的就是作用域规则！

### 2、概念

#### 2.1、命名空间（namespace）

1. 定义

> A *namespace* is a mapping from names to objects
>
> 命名空间是名字和对象的映射。也就是可以把一个namespace理解为一个字典，实际上很多当前的Python实现namespace就是用的字典。各个命名空间是独立的，没有任何关系的，所以一个命名空间中不能有重名，但不同的命名空间是可以重名而没有任何影响。
>
> 命名空间表示变量的可见范围，一个变量名可以定义在多个不同的命名空间，相互之间并不冲突，但同一个命名空间中不能有两个相同的变量名。比如：两个叫“张三”的学生可以同时存在于班级A和班级B中，如果两个张三都是一个班级，那么带来的麻烦复杂很多了，在Python中你不能这么干。

1. 命名空间的种类(2.2以前三种,2.2四种)

   - 局部，函数内的命名空间就是局部的(函数内部声明但没有使用global的变量)—>local；
   - 全局，模块内(.py文件内)的命名空间就是全局的—>global；
   - 内置，包括异常类型、内建函数和特殊方法，可以代码中任意地方调用—>built-in；
   - 闭包，嵌套的父级函数的局部作用域，即包含此函数的上级函数的局部作用域，但不是全局的(闭包函数外的函数中 )—>enclosing

2. 作用范围结构图

   ![](http://opzv089nq.bkt.clouddn.com/18-1-13/23830955.jpg)

3. 举个栗子1

   - 局部

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

   - 全局

     ```python
     #demo1.py
     txt = '大吉大利,今晚吃鸡'
     print(txt)

     #demo2.py
     print(txt)#程序出错
     ```

   - 系统内置

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

   - 闭包

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

   - 栗子1

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

   - 栗子2

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

      2、执行函数ex_global()在本地作用域声明又声明了一个name的变量值是'小花'

      3、调用函数print(),根据上面说的作用域的查找顺序可以知道先从本地作用域查找,所以第一次输出结果是小花

      4、此时方法执行完毕,执行第二个print(name)由于前面学过的作用域可以知道第二个name变量只会在全局作用域中查找,所以输出小明


1. 总结
   - 在局部命名空间处，全局命名空间的同名变量是不可见的（只有变量不同名的情况下，可使用 global关键字让其可见）
   - 闭包函数外的函数中
   - 全局命名空间和局部命名空间中， 如果有同名变量，在全局命名空间处，局部命名空间内的同名变量是不可见的
   - 内置命名空间在代码所有位置都是可见的，所以可以随时被调用

#### 2.2、作用域（scope）

> A *scope* is a textual region of a Python program where a namespace is directly accessible.
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

   - 如果在函数内调用一个变量，先在函数内（局部命名空间）查找，如果找到则停止查找。否则在函数外部（全局命名空间）查找，如果还是没找到，则查找内置命名空间。如果以上三个命名都未找到，则抛出NameError 的异常错误。

- 如果在函数外调用一个变量，则在函数外查找（全局命名空间，局部命名空间此时不可见），如果找到则停止查找，否则到内置命名空间中查找。如果两者都找不到，则抛出异常。只有当局部命名空间内，使用global 关键字声明了一个变量时，查找顺序则是上面的查找顺序

#### 2.4、其它

##### 1、块级作用域(语法块)

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

   代码执行成功，没有问题；在Java/C#中，执行上面的代码会提示name，age没有定义，而在Python中可以执行成功，这是因为在Python中是没有块级作用域的，代码块里的变量，外部可以调用，所以可运行成功；

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

   - 栗子1

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

- 栗子2

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

   2、执行函数ex_global()在本地作用域声明又声明了一个name的变量值是'小花'

   3、调用函数print(),根据上面说的作用域的查找顺序可以知道先从本地作用域查找,所以第一次输出结果是小花

   4、此时方法执行完毕,执行第二个print(name)由于前面学过的作用域可以知道第二个name变量只会在全局作用域中查找,所以输出小明

#### 2、nonlocal(Python3.2引入的)

1. 说明

   用来在函数或其他作用域中使用外层(非全局)变量

2. 举个栗子

   - 栗子1

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

      1、outer()函数执行

      2、定义一个局部变量 num 并且赋值1

      3、执行inner函数，把 num 绑定到外部函数的局部变量 num 上

      4、赋值num为2,所以第一个print()函数在控制台输出2,函数执行完毕

      5、执行第二个print()方法，由于上一步可以知道,num=2，所以也是输出2，代码执行完毕

### 4、综合栗子

1. 栗子1

   ```python
   def scope_complex():
       def ex_local():
           var = "本地作用域2"  # 此函数定义了另外的一个spam字符串变量，并且生命周期只在此函数内。此处的spam和外层的spam是两个变量，如果写出spam = spam + “local spam” 会报错

       def ex_nonlocal():
           nonlocal var  # 使用外层的var变量
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

      1、执行函数 scope_complex() ，定义局部变量 var = "局部作用域1"

      2、执行函数ex_local() ，定义局部变量var = "本地作用域2" ，作用范围仅仅ex_local函数中

      3、执行函数print(var) ，输出的第一步定义的局部变量,而不是第二步定义的局部变量

      4、执行函数ex_nonlocal()，将var变量绑定在第一步定义的变量上，讲var的值改为"闭包作用域"

      5、执行函数print(var)，输出"闭包作用域"

      6、执行函数ex_global()，声明全局变量var赋值"全局作用域"

      7、执行函数print(var)，先从本地函数作用域查找,所有输出还是"闭包作用域",

      8、scope_complex()  执行完成

      9、执行函数print(var),从本地作用域中查找,由于在第七步声明了var，所以输出"全局作用域"

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

变量会由内到外找，先去自己作用域去找，自己没有再去上级去找，直到找不到报错,形成一条链

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
       
   if name == 'main':    
      fun1()
      #输出老王
   ```


1. 栗子2

   ```python
   name = "小明"
   def fun1():
       print(name)
       
   def fun2():   
       name = "小花"
       return fun1 

   chain = fun2()

   if name == 'main':
   	chain()
   ```

   代码分析

   1、chain()相当执行fun2()函数返回的fun1()的内存地址,即chain=f1执行chain()相当于执行fun1()

   2、执行fun1()时与fun2()没有任何关系，name = "小明"与fun1在一个作用域链，所以输出的是"小明"

   ​	

## 二、lambda表达式(匿名函数)

### 1、概念

> lambda函数也叫匿名函数，即，函数没有具体的名称	
>
> ```python
> def multip(x):  
>     return x * 2  
>
>
> lam = lambda x : x * 2  
>
> print(multip(2))
> print(lam(2))
>
> ```
>
> 运行完成之后的结果都是6,通过结果我们可以知道，lambda在Python这种动态的语言中确实没有起到什么特别大的作用，因为有很多别的方法能够代替lambda，所以python对 ambda有比较简单有限的支持

### 2、为什么要使用lambda

> 通过上面的代码，我们会发现
>
> 1. lambda简化了函数定义的书写形式。是代码更为简洁，但是使用函数的定义方式更为直观，易理解。
>
> 2. 对于一些抽象的，不会别的地方再复用的函数，有时候给函数起个名字也是个难题，使用lambda不需要考虑命名的问题
>
>    ​

　

### 3、语法格式

> ```python
> lambda 形参列表 : 表达式
> ```
>
> 说明
>
> 1. 关键字`lambda`后面紧跟着形参列表. 注意形参列表不能用圆括号括起来
> 2. 形参列表后面紧跟着一个冒号(`:`)
> 3. 冒号后面是唯一的表达式. 注意:此表达式必须是合法的表达式.
> 4. `lambda`会自动返回表达式的运算结果.
>
> 注意事项
>
> 1. lambda 表达式只是对简单到只有一行代码的函数的语法糖(简写), 如果有多行代码, 则无法使用 lambda 表达式
> 2. lambda用来编写简单的函数，而def用来处理更强大的任务



Python中，也有几个定义好的全局函数方便使用的，filter, map, reduce　　



## 附:

1. 能改变作用域的

   - python能够改变变量作用域的代码段是def、class、lamda.
   - if/elif/else、try/except/finally、for/while 并不能涉及变量作用域的更改，也就是说他们的代码块中的变量，在外部也是可以访问的

2. 语法糖

   就相当于汉语里的成语。即，用更简练的言语表达较复杂的含义。指计算机语言中添加的某种语法，这种语法对语言的功能并没有影响，但是更方便程序员使用。通常来说使用语法糖能够增加程序的可读性，从而减少程序代码出错的机会，例如5*5等同于5+5+5+5+5

##  



