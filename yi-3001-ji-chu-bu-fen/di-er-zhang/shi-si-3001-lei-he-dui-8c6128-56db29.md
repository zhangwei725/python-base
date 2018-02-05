# 面向对象其它

## 一、访问限制\(修饰符\)

### 1、说明

> 在class内部，可以有属性和方法，而外部代码可以通过直接调用实例变量的方法来操作数据，这样，就隐藏了内部的复杂逻辑，对于每一个类的成员\(属性,字段,方法\)的修饰符有两种
>
> * 公开成员，在任何地方都能访问，即可在类外面和对象调用方法进行访问；
> * 私有成员，只有在类的内部才能访问；

### 2、为什么要有修饰符

1. 我们在一个类当中会产生很多的变量、属性、方法。其中有些是只能这个类自己用的，某些是可以允许其他程序使用的。如果在别的程序在调用当中对类的对象当中某些关键属性进行了改动，可能会导致这个对象无法正常工作。这是相当危险的。
2. 而且把应该提供出去的方法属性和不能提供出去的方法属性相区别出，也体现了这个类的封装性。一个类模块只向外提供应该提供的功能而把其他无关紧要的内容屏蔽掉。因为一个工程可能不只有一个人在做，有的时候有多个人在做，这个时候就要求各个模块要有一定的封装性，其他程序员在做的时候不至于误操作，而且一看就明白了这个模块可以提供哪些功能。

### 3、语法格式

1. `object`\(公开成员\)

   上面所讲的都是公开的成员

2. `_object`\(私有成员\)

   Python中没有真正的私有字段或方法, 为了实现类似于c++中私有方法，

   可以在你想声明为私有的方法和属性前加上单下划线,以提示该属性和方法不应在外部调用。

   如果真的调用了也不会出错,但不符合规范

3. `__object`\(私有成员\)

   * 私有成员命名时，前两个字符是下划线，只有自己的类内部能访问,继承的父类,子类均不能访问
   * 真正作用是用来避免子类覆盖其内容\(后面继承具体举例\)

4. `__object__`

   私有成员，系统专用。特殊成员除外，例如：`__init__`、`__call__`、`__dict__`等

### 4、举个栗子

#### 4.1 、修饰普通字段

1. 公有字段

   ```python
   class Person(object):
       def __init__(self, name):
           self._name = name

   if __name__ == '__main__':
       person = Person('小明')
       print(person.name)
   ```

2. 私有字段单下划线 "\_"

   ```python
   class Person(object):
       def __init__(self, name):
           self._name = name

   if __name__ == '__main__':
       '''测试代码'''
       person = Person('小明')
       # ====能正常访问,但会出现语法警告 
       print(person._name)
   ```

3. 私有字段 双下划线 "\_\_"

   ```python
   class Person(object):
       def __init__(self, name):
           self.__name = name
        # 通过方法内部调用 self.__name
       def get_name(self):
           return self.__name

   if __name__ == '__main__':
       '''测试代码'''
       person = Person('小明')
       # ====能正常访问,但会出现语法警告 ====
       # print(person.__name)
       print(person.get_name())

       # 外部无法访问
       print(person.__name)  #程序出错
       # 强制调用私有变量,通过 对象._类名__私有变量名(注意:请不要在开发中这么去使用)
       print(person._Person__name)
   ```

#### 4.2 、修饰静态字段

1. 栗子1

   ```python
   class Test(object):
       __static_var = '私有的静态变量'

       def show(self):
           print(Test.__static_var)

   if __name__ == '__main__':
       '''测试代码'''
       #Test.__name  # 类访问            ==> 错误
       obj = Test()
       # 通过对象强制调用(注意:请不要在开发中这么去使用)
       print(obj._Test__static_var)
       obj.show()  # 类内部可以访问     ==> 正确
   ```

#### 4.3、修饰方法

1. 栗子1

   ```python
   class Test(object): 
       def __method(self): 
           print("私有普通方法") 

   if __name__ == '__main__':
       # 报错
       obj.__method() 
       # 强制调用(注意:请不要在开发中这么去使用)
       obj._Test__method()
   ```

#### 4.4、其它成员类似

#### 4.5、`__xx__`

​    此种写法为Python内建属性方法，不要去使用这种方式命名

## 二、类的特殊成员

### 1、概要

> 在 Python 中，我们可以经常看到以双下划线`__`包裹起来的方法，比如最常见的`__init__，这些方法被称为`魔法方法（magic method）或特殊方法（special method）。简单地说，这些方法可以给 Python 的类提供特殊功能，方便我们定制一个类，
>
> ```python
> __init__ :      构造函数，在生成对象时调用
> __del__ :       析构函数，释放对象时使用
> __repr__ :      打印，转换
> __setitem__ :   按照索引赋值
> __getitem__:    按照索引获取值
> __len__:        获得长度
> __cmp__:        比较运算
> __call__:       调用
> __add__:        加运算
> __sub__:        减运算
> __mul__:        乘运算
> __div__:        除运算
> __mod__:        求余运算
> __pow__:        幂
> ```
>
> 需要注意的是，这些成员里面有些是方法，调用时要加括号，有些是属性，调用时不需要加括号。下面将一些常用的介绍一下，：

### 2、常用的特殊成员

#### 1、`__doc__`

1. 说明

   说明性文档和信息。Python自建，无需自定义。

2. 栗子

   ```python
   class Foo:
       """ 描述类信息，可被自动收集 """

       def func(self):
           pass

   # 打印类的说明文档 
   print(Foo.__doc__)
   ```

#### 2、 `__init__()`

1. 说明

   实例化方法，通过类创建实例时，自动触发执行。

2. 栗子

   ```
   class Foo:

       def __init__(self, name):
           self.name = name
           self.age = 18

   obj = Foo(jack') # 自动执行类中的 __init__ 方法
   ```

#### 3、 `__module__` 和 `__class__`

1. 说明

   `__module__` 表示当前操作的对象在属于哪个模块。

   `__class__` 表示当前操作的对象属于哪个类。

   这两者也是Python内建，无需自定义。

2. 栗子

   ```python
   class Foo:
       pass

   obj = Foo()
   print(obj.__module__)
   print(obj.__class__)

   ------------
   运行结果：
   __main__
   <class '__main__.Foo'>
   ```

#### 4、`__del__()`

1. 说明

   析构方法，当对象在内存中被释放时，自动触发此方法。

   注：此方法一般无须自定义，因为Python自带内存分配和释放机制，除非你需要在释放的时候指定做一些动作。析构函数的调用是由解释器在进行垃圾回收时自动触发执行的。

2. 栗子

   ```python
   class Foo:

       def __del__(self):
           print("我被回收了！")

   obj = Foo()
   del obj
   ```

#### 5、`__call__()`

1. 如果为一个类编写了该方法，那么在该类的实例后面加括号，可会调用这个方法。

   注：构造方法的执行是由类加括号执行的，即：`对象 = 类名()`，而对于`__call__()` 方法，是由对象后加括号触发的，即：`对象()`或者 `类()()`

2. 栗子

   ```python
   class Foo:

       def __init__(self):
           pass

       def __call__(self, *args, **kwargs):

           print('__call__')

   obj = Foo()     # 执行 __init__
   obj()       # 执行 __call__
   ```

   那么，怎么判断一个对象是否可以被执行呢？能被执行的对象就是一个Callable对象，可以用Python内建的callable\(\)函数进行测试，我们在前面的章节已经介绍过这个函数了。

   ```
   >>> callable(Student())
   True
   >>> callable(max)
   True
   >>> callable([1, 2, 3])
   False
   >>> callable(None)
   False
   >>> callable('str')
   False
   >>> callable(int)
   True
   >>> callable(str)
   True
   ```

   ### 6、 `__dict__`

3. 说明

   列出类或对象中的所有成员！非常重要和有用的一个属性，Python自建，无需用户自己定义。

4. 栗子

   ```python
   class Province:
       country = 'China'
       def __init__(self, name, count):
           self.name = name
           self.count = count

       def func(self, *args, **kwargs):
           print（'func'）

   # 获取类的成员
   print(Province.__dict__)

   # 获取 对象obj1 的成员 
   obj1 = Province('湖北',10000)
   print(obj1.__dict__)

   # 获取 对象obj2 的成员 
   obj2 = Province('武汉', 3888)
   print(obj2.__dict__)
   ```

#### 7、`__str__()`

1. 说明

   如果一个类中定义了`__str__()`方法，那么在打印对象时，默认输出该方法的返回值。这也是一个非常重要的方法，需要用户自己定义。

2. 栗子

   下面的类，没有定义`__str__()`方法，打印结果是：`<__main__.Foo object at 0x000000000210A358>`

   ```python
   class Foo:
       pass

   obj = Foo()
   print(obj)
   ```

   定义了`__str__()`方法后，打印结果是：'jack'。

   ```python
   class Foo:
       def __str__(self):
           return 'jack'
   obj = Foo()
   print(obj)
   ```

   ### 8、`__getitem__()`、`__setitem__()`、`__delitem__()`

3. 说明

   取值、赋值、删除这“三剑客”的套路，在Python中，我们已经见过很多次了，比如前面的`@property`装饰器。

   Python中，标识符后面加圆括号，通常代表执行或调用方法的意思。而在标识符后面加中括号\[\]，通常代表取值的意思。Python设计了`__getitem__()`、`__setitem__()`、`__delitem__()`这三个特殊成员，用于执行与中括号有关的动作。它们分别表示取值、赋值、删除数据。

4. 栗子

   ```
   a = 标识符[]　： 　　执行__getitem__方法
   标识符[] = a  ： 　　执行__setitem__方法
   del 标识符[]　： 　　执行__delitem__方法
   ```

5. 如果有一个类同时定义了这三个魔法方法，那么这个类的实例的行为看起来就像一个字典一样，如下例所示：

   ```python
   class Foo:

       def __getitem__(self, key):
           print('__getitem__',key)

       def __setitem__(self, key, value):
           print('__setitem__',key,value)

       def __delitem__(self, key):
           print('__delitem__',key)

   obj = Foo()

   result = obj['k1']      # 自动触发执行 __getitem__
   obj['k2'] = 'jack'      # 自动触发执行 __setitem__
   del obj['k1']           # 自动触发执行 __delitem__
   ```

### 9、 `__iter__()`

1. 说明

   这是迭代器方法！列表、字典、元组之所以可以进行for循环，是因为其内部定义了 `__iter__()`这个方法。如果用户想让自定义的类的对象可以被迭代，那么就需要在类中定义这个方法，并且让该方法的返回值是一个可迭代的对象。当在代码中利用for循环遍历对象时，就会调用类的这个`__iter__()`方法。

2. 栗子1\(普通的类\)

   ```python
   class Foo:
       pass

   if __name == '__main__'
       obj = Foo()    
       for i in obj:
         print(i)
   ```

   报错：TypeError: 'Foo' object is not iterable \# 原因是Foo对象不可迭代

3. 添加一个`__iter__()`，但什么都不返回：

   ```python
     class Foo:

         def __iter__(self):
             pass

     obj = Foo()

     for i in obj:
         print(i)
     # 报错：TypeError: iter() returned non-iterator of type 'NoneType'
     #原因是 __iter__方法没有返回一个可迭代的对象
   ```

4. 返回一个个迭代对象：

   ```python
   class Foo:

       def __init__(self, sq):
           self.sq = sq

       def __iter__(self):
           return iter(self.sq)

   obj = Foo([11,22,33,44])

   for i in obj:
       print(i)

   # 这下没问题了！
   ```

5. 最好的方法是使用生成器：

   ```python
   class Foo:
       def __init__(self):
           pass

       def __iter__(self):
           yield 1
           yield 2
           yield 3

   obj = Foo()
   for i in obj:
       print(i)
   ```

10、`__len__()`

1. 说明

   在Python中，如果你调用内置的len\(\)函数试图获取一个对象的长度，在后台，其实是去调用该对象的`__len__()`方法，所以，下面的代码是等价的：

2. 栗子

   ```python
   >>> len('ABC')
   3
   >>> 'ABC'.__len__()
   3
   ```

   Python的list、dict、str等内置数据类型都实现了该方法，但是你自定义的类要实现len方法需要好好设计。

### 11、 `__repr__()`

1. 说明

   这个方法的作用和`__str__()`很像，两者的区别是`__str__()`返回用户看到的字符串，而`__repr__()`返回程序开发者看到的字符串，也就是说，`__repr__()`是为调试服务的。通常两者代码一样。

2. 栗子

   ```python
   class Foo:

       def __init__(self, name):
           self.name = name

       def __str__(self):
           return "this is %s" % self.name

       __repr__ = __str__
   ```

### 12、`__add__`: 加运算 `__sub__`: 减运算 `__mul__`: 乘运算 `__div__`: 除运算 `__mod__`: 求余运算 `__pow__`: 幂运算

1. 说明

   这些都是算术运算方法，需要你自己为类设计具体运算代码。有些Python内置数据类型，比如int就带有这些方法。Python支持运算符的重载，也就是重写。

2. 栗子

   ```python
   class Vector:
      def __init__(self, a, b):
         self.a = a
         self.b = b

      def __str__(self):
         return 'Vector (%d, %d)' % (self.a, self.b)

      def __add__(self,other):
         return Vector(self.a + other.a, self.b + other.b)

   v1 = Vector(2,10)
   v2 = Vector(5,-2)
   print (v1 + v2)
   ```

### 13、 `__author__`

1. 说明

   `__author__`代表作者信息！类似的特殊成员还有很多，就不罗列了。

2. 栗子

   ```python
   #!/usr/bin/env python
   # -*- coding:utf-8 -*-

   """
   a test module
   """
   __author__ = "Jack"

   def show():
       print(__author__)

   show()
   ```

### 14、`__slots__`

1. 说明

   Python作为一种动态语言，可以在类定义完成和实例化后，给类或者对象继续添加随意个数或者任意类型的变量或方法，这是动态语言的特性。例如：

2. 栗子

   ```python
   def print_doc(self):
       print("haha")

   class Foo:
       pass

   if __name__ == '__main__'
     obj1 = Foo()
     obj2 = Foo()
     # 动态添加实例变量
     obj1.name = "jack"
     obj2.age = 18
     # 动态的给类添加实例方法
     Foo.show = print_doc
     obj1.show()
     obj2.show()
   ```

   但是！如果我想限制实例可以添加的变量怎么办？可以使`__slots__`限制实例的变量，比如，只允许Foo的实例添加name和age属性。

   ```
   def print_doc(self):
       print("haha")

   class Foo:
       __slots__ = ("name", "age")
       pass

   obj1 = Foo()
   obj2 = Foo()
   # 动态添加实例变量
   obj1.name = "jack"
   obj2.age = 18
   obj1.sex = "male"       # 这一句会弹出错误
   # 但是无法限制给类添加方法
   Foo.show = print_doc
   obj1.show()
   obj2.show()
   ```

#### 15、综合

1. 栗子

   ```python
   class  doges(object):
   　　""" 类的描述信息 """
   　　 def  __init__(self,name,food):
   　　self.name=name
   　　self.food=food
   　　self.data={}# 定义一个类的字典
   　　 def  __call__(self, *args, **kwargs):# 对象后面加括号解执行
   　　print(*args)
   　　 def  __str__(self):# 默认输出返回值
   　　 return self.name
   　　 def  __getitem__(self):# 可以获取类的的字典
   　　 return self.data
   　　 def  __setitem__(self, key, value):# 可以设置类的的字典
   　　self.data[key]=value
   　　 def  __delitem__(self, key):# 可以删除类的字典的内容
   　　 del self.data[key]
   　　dog=doges('xxx','iii')
   　　print(dog.__doc__)
   　　b=a()
   　　print(b.__module__)# 操作的对象的那个模块
   　　print(dog.__class__)# 当前操作的对象的类是什么
   　　dog('111')#
   　　print(doges.__dict__)# 查看类或对象的成员  类只打印类的成员不打印对象的成员
   　　print(dog.__dict__)# 查看类或对象的成员 对象只打印对象的成员不打印类的成员
   　　print(dog)# 打印  __str__ 的返回值
   　　print(dog.__str__())# 打印返回值
   　　dog['1']=1000# 触发 .__setitem__()
   　　dog['2']=1000# 触发 .__setitem__()
   　　print(dog.__getitem__())
   　　print(dog.__delitem__('1'))# 删除类中字典
   　　print(dog.__getitem__())
   　　# 设置类的特殊方法 def  func(self):
   　　print('hello word%s'%self.name)
   　　print()
   　  def  __init__(self,name,age):
   　　self.name=name
   　　self.age=age##type 参数  1: 类名  2. 类的基类  3. 类的成员 , 字典格式
   　　CAT=type('CAT',(object,),{'func':func,'__init__':__init__})
   　　cat=CAT(' 喵喵 ',3)
   　　cat.func()
   　　print(cat.name,cat.age)
   ```

## 总结

1. 栗子

   ```python
   class Animal(object):
       """ 这个是类的注释信息 """
       name = 'tom'

       def __init__(self, name):
           self.name = name
           # 加了两个下划线后的变量名，此时变为了私有属性，也就是私有变量
           self.__num = 'private'

       def talk(self):
           print("%s are talking" % self.name)

       # 类方法，不能够访问实例变量,把walk方法变成了类方法，可以直接类名.方法名调用，但是要注意的是walk里
       # 面的代码块的变量或者其他的对象都应该是类可以访问的。
       @classmethod
       def walk(cls):
           # 由于添加了类方法的装饰器，所以这里的%s只能用类属性（animal.name，也叫类变量）去赋值给%s，
           print("\t\t%s are talking" % cls.name)

       # 静态方法，不再传self参数进去。所以不能够访问类变量以及实例变量，如果添加了self,那么就要在调用的时候把实例名传进去
       @staticmethod
       def habit():
           print("%s's habit : walking" % Animal.name)

       @property  # 把方法变成属性，那么调用的时候可以不用加括号()，一般是为了隐藏该方法
       def runing(self):
           print("%s is running" % self.name)

       def r_private(self):
           return self.__num

       @property
       def total_players(self):
           return self.__num

       # 这样可以修改添加了@property里面的值
       @total_players.setter
       def total_players(self, num):
           self.num = num
           print("total players:", self.num)

   if __name__ == '__main__':

       Animal.walk()
       d = Animal('jack')

       d.walk()
       d.habit()
       d.runing
       # 咱们访问私有变量一般都是写个方法，通过方法返回私有变量
       d.r_private()  
       # 下面的直接加两个下划线来访问私有属性是错误的方法
       # print(d.__num)

       d.__num = 'hh'  # 通过下面的赋值的方法，等于新建了一个__num的变量。这个和私有变量__num是两码事
       print(d.__num)

       print(d._Animal__num)  # 强制访问私有变量,实例名._类名__私有变量名

       print(d.total_players)
   ```

作业

1. 首先定义一个描述银行账户的Account类，包括成员变 量“账号”和“存款余额”，成员方法有“存款”、“取款”和“余额查询”。其次测试Account类的功能
2. 义一个时钟类——Clock，它包括三个int型 成员变量分别表示时、分、秒，一个构造方法用于对三个成员变量（时、分、秒） 进行初始化，还有一个成员方法show\(\)用于显示时钟对象的时间

附录:

1. 强类型语言\(静态类型语言\)是指需要进行变量/对象类型声明的语言，一般情况下需要编译执行。例如C/C++/Java/C\#
2. 弱类型语言\(动态类型语言\)是指不需要进行变量/对象类型声明的语言，一般情况下不需要编译\(但也有编译型的\)。例如PHP/ASP/Ruby/Python/Perl/ABAP/SQL/JavaScript/Unix Shell等等。



