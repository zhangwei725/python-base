# 类的组成详解

## 一、字段

### 1、概念

> 字段包括：普通字段和静态字段，他们在定义和使用中有所区别，而最本质的区别是内存中保存的位置不同。字段名一般是名词

### 2、分类

#### 1、静态字段\(静态变量,类变量\)。

1. 定义

   它随着这个程序的执行产生，随着程序的结束而消失，这样和程序‘共存亡’的字段，我们就叫它静态字段

   在方法外面定义的字段统统称为静态字段

2. 特点

   1、这个类所有对象共享一个内存地址

   2、直接可以通过 **类名.字段名**调用

3. 调用方式

   类名.类变量

   对象.类变量

#### 2、普通字段\(实例变量\)。

1. 定义

   类定义内部`__init__`函数内以self开头定义的变量

2. 特点

   1、属于对象

3. 调用方式

   对象.普通字段

#### 3、举个栗子\(类变量\)

1. 栗子1

   ```python
    class Person:
          money = 10000

          def __init__(self, name, age, gender):
              self.name = name
              self.age = age
              self.gender = gender

          def say(self):
              print(self.name + ':在说话!!!')

      if __name__ == '__main__':
            '''测试开始'''
          #打印类的属性
          print(Person.__dict__.keys())
          #通过类调用
          print(Person.money)
          #通过类操作类变量
          Person.money += 1
          print(Person.money)

          xm = Person('小明', 18, '男')
          #通过对象操作类变量
          xm.money += 1
          #通过对象调用
          print(xm.money)
   ```

   说明:

   1、将类加载进内存

   2、将类变量加载进类的内存

   3、将`__init__()`方法的地址加载进类的内存

   4、将普通方法方法的地址加载进类的内存

   5、实例化对象分配对象内存地址

   6、将实例变量初始化加载进对象内存

2. 案例2

   ```python
   if __name__ == '__main__':
       # 通过类修改类变量
       person = Person('小明', 18, '男')
       Person.money += 10000
       print('通过类修改后的值:' + str(Person.money))
       # 通过对象修改变量
       person.money += 10000
       print('通过对象修改后类变量:' + str(Person.money))
       print('通过对象调用修改后的类变量:' + str(person.money))
   ```

   打印结果

   ![](http://opzv089nq.bkt.clouddn.com/18-1-25/93925068.jpg)

   内存结构图

   ![](http://opzv089nq.bkt.clouddn.com/18-1-25/91835083.jpg)

   说明

   * 当我们类的内存中有一个类变量的时候，我们使用类去调用这个字段，自然找到的是类变量，当我们使用对象去调用的时候，这个对象指针先在自己的内存里找了找，发现没找到，于是就用对象中维护的类指针到类的内存中去找，果然找到了money,然后打印出来
   * 当我们使用对象去第一次调用并改变一个类的类变量的时候，它们自己的内存中并没有money字段，所以还是通过类指针到类内存中去找，但是当它们找到之后，就会在自己的内存空间开辟一块空间来存储对这个类变量修改后的结果。所以，这个时候类中的类变量就不会被改变，而两个对象中的money字段也就不会互相影响

   **注意事项:我们只需要记住，在使用类的静态变量的时候，**

   **必须要用类名来调用和修改。它才会永远被类和对象共享**

#### 4、self

> self不是一个关键字，而是约定的写法
>
> 学过其他语言的人都知道, python 的 self 其实就是在其他语言的`this`.
>
> 那么`self`到底指代哪个对象?
>
> 通过哪个对象调用的这个实例方法, 那么这个实例方法中的`self`就指代谁
>
> **而且 python 的**`self`**一朝绑定, 终身不变. **(不像 javascript 中的那个 `this` 小婊砸随着调用方式的不同而而更改绑定对象, 让你眼花缭乱到怀疑人生)

## 二、方法

### 1、概念

> 方法包括：普通方法、静态方法和类方法，三种方法在**内存中都归属于类**，区别在于调用方式不同,方法名称一般以动词开头

### 2、分类

#### 2.1、按作用分

1. 构造方法(`__init__(self)`)
2. 析构函数(`__del__(self)`)

#### 2.2、按类型

1. **普通方法(实例方法)**
2. 私有方法（方法前面加两个下划线）
3. 静态方法
4. 类方法
5. 属性方法

### 3、普通方法\(实例方法\)

1. 说明

   由**对象**调用；至少一个`self`参数；执行普通方法时，自动将调用该方法的**对象**赋值给`self`

2. 语法格式

   ```python
   class 类名:
      def 普通方法名(self,参数列表):
         print('普通方法名')

      def 普通方法名(self,参数列表)
             return '返回值'
   ```

3. 调用方式

   obj.普通方法()

4. 注意事项

   1. 通过类的实例去调用
   2. 可以使用类变量,和实例变量

5. 举个栗子

   * 不带参数的普通方法

     ```python  
     class Person:  
       def **init**(self, name, age, gender):  
         self.name = name  
         self.age = age  
         self.gender = gender

     ```
       def say(self):
       print(self.name + ':今天天气挺好的!!!')
     ```

     if __name__ == '__main__':
           '''测试开始'''
         xm = Person('小明', 18, '男')
         xm.say()

     ```

     ```

     ```

* 带参数的普通方法

  ```python  
  class Person:  
      def **init**(self, name, age, gender):  
          self.name = name  
          self.age = age  
          self.gender = gender

  def say(self):                                
      print(self.name + ':今天天气挺好的!!!')          

  def say1(self, content):                      
      print(self.name + content)  
      
  if __name__ == '__main__':  
        '''测试开始'''                                    
    	  xm = Person('小明', 18, '男')
        #带参数的
   	  xm.say1(':阿红我想你!!!')                 
  ```



* 带返回值

  ```python
  class Person:                                     
      def __init__(self, name, age, gender):        
          self.name = name                          
          self.age = age                            
          self.gender = gender                      

      def say(self):                                
          print(self.name + ':今天天气挺好的!!!')          

      def get_name(self):
          return self.name

  if __name__ == '__main__':                        
      '''测试开始'''                                    
      xm = Person('小明', 18, '男')
        print(xm.get_name())
  ```

* 不要在实例方法里绑定实例变量

  ```python
  class  Person:
    #推荐放在init方法中
    def set_name(self, name):
        self.name = name
  ```

### 4、静态方法

1. 说明

   由**对象**调用；至少一个`self`参数；执行普通方法时，自动将调用该方法的**对象**赋值给`self`

2. 语法格式

   ```python
   class 类名:
       @staticmethod
       def 静态方法名():
           pass
   ```

3. 调用方式

   类名.静态方法名()

   对象.静态方法名()

4. 优点

   第一点当某个类里的函数不需要`self` 或者`cls`等实例或类参考时,使用静态方法就可以比较简明且有效率的完成工作。

   * 简明指的是不需要多接受一个无关的参数
   * 效率在与一般的实例方法,需要生成对象才能去使用,会分配内存空间,而静态方法就不需要

   第二点与实例无关但又属于类的,客观的来讲有能为类提供一下服务,这点优点难理解

5. 注意事项

   * 要在类中使用静态方法，需在类成员函数前面加`上@staticmethod`标记符，以表示下面的成员函数是静态函数。
   * 静态方法不能使用实例变量
   * 使用静态方法的好处是，不需要定义实例即可使用这个方法。
   * 另外，多个实例共享此静态方法，一般在工具类中使用的比较多

6. 特点

   静态方法单独属于一个类,不能重写,不能被继承

7. 举个栗子

   * 栗子1

     ```python

     ```

### 5、类方法

1. 说明

   类方法是将类本身作为对象进行操作的方法。类方法使用@classmethod装饰器定义，其第一个参数是类，约定写为cls。类对象和实例都可以调用类方法，且只能操作类变量

2. 语法格式

   ```python
   class 类名:
       def 类方法(cls):
           pass
   ```

3. 调用方式

   类.类方法
   * 一个类方法就可以通过类或它的实例来调用的方法, 不管你是用类来调用这个方法还是类实例调用这个方法,该方法的第一个参数总是定义该方法的类对象。 类方法的第一个参数都是类对象而不是实例对象
   * 类方法能实现的功能都可以通过定义一个普通函数来实现,只要这个函数接受一个类对象做为参数就可以了

4. 举个栗子

   ```python

   ```

### 6、总结

1. 定义不同

   python中实现静态方法和类方法都是依赖于python的修饰器来实现的。而普通方法不需要

2. 传递的必要参数不同

   实例方法有self参数，类方法有cls参数，静态方法是不需要这些附加参数的

3. 调用方式不同

   静态方法和类可以被类和对象调用,实例方法只能被通过对象调用

4. 使用变量

   实例方法能使用类变量,实例变量,类方法能使用类变量,不能使用实例变量,静态方法两者都不能使用

5. 相互调用不同

   实例方法可以调用静态方法,类方法,而类方法跟静态方法不能调用实例方法

6. 其它

   类方法是可以替代静态方法的。静态方法不能在继承中修改

## 三、属性\(属性函数\)

### 1、概念

> Python中的属性其实是**普通方法**的变种,就是通过@property把一个方法变成一个静态变量,实质就是**函数**转变成**类变量**

### 2、作用

1. 内部进行一系列的逻辑计算，最终将计算结果返回,例如计算年纪,计算商品的价格,计算当前的时间等等
2. 对数据进行验证

### 3、定义方式

1. **装饰器方式在：类的普通方法上应用@property装饰器**
2. **静态方法：在类中定义值为property对象的静态字段**

### 4、注意事项

1. **经典类：**只有一种
   1. `@property`
   2. 定义时，在普通方法的基础上添加 `@property` 装饰器；
   3. 定义时，属性**仅有一个**`self`参数
2. **新式类：**具有三种``装饰器
   1. `@property`(获取)
   2. `@方法名.setter`(修改)
   3. `@方法名.deleter`(删除)

### 5、调用方式

1. 调用时，无需括号
   * 方法：`obj.fun()`
   * 属性：`obj.prop`

### 6、提供getter,setter方法

1. 这两个方法可以方便增加额外功能（比如验证）。
2. 内部存储和外部表现不同。可以保持外部接口不变的情况下，修改内部存储方式和逻辑
3. 动态地计算值，getter/setter提供了一些属性读取的封装，可以让代码更便捷，例如存储first_name和last_name字段，但是提供full_name属性的getter

### 7、举个栗子

1. 输出用户全名(经典类)

   ```python  
   class Person(object):  
       def __init__(self, first_name,last_name,age):  
             self.first_name = first_name  
           self.last_name  = last_name  
           self.age = age
           
      @property
      def full_name(self):
            return "%s %s" % (self.first_name, self.last_name)
   if __name__ == '__main__': 
         person = Person('丽颖', '赵', 18)  
         print(person.full_name)  
     	  '''  
      	  思考 带了一系列的问题  
      	  '''  
         person = Person('丽颖', '赵', -15)  
         person = Person('丽颖', '赵', 1000)
         #年龄-15岁 或者 1000岁,显然不符合我们日常的习惯
         print(person.age)
   ```


2. 计算商品打折后的价格(经典类)

   ```python
   class Goods:
       def __init__(self, current_price, dis_price):
           self.current_price = current_price
           self.discount_price = dis_price
    
       @property
       def price(self):
         '''计算折扣后的商品价格'''
           return self.current_price - self.dis_price
    
   if __name__ == '__main__':
       goods = Goods(1000.00, 100)
       print(goods.price)
   ```

3. 分页功能(新式类)

   ```python
   class Pager(object):

       def __init__(self, page, page_size):
           # 用户当前请求的页码（第一页、第二页...）
           self.page = page
           # 每页默认显示10条数据
           self.page_size = page_size if page_size < 0 else 10

       @property
       def start(self):
           val = (self.page - 1) * self.page_size
           return val

       @property
       def end(self):
           val = self.page * self.page_size
           return val

   if __name__ == '__main__':
       '''' ############### 调用 ############### '''
       pager = Pager(1, 10)
       print(pager.start)
       print(pager.end)
   ```

4. 提供getter,setter方法\(新式类\)

   ```python
   class Goods(object):
       def __init__(self):
           """  构造方法 """
           self._price = None

       @property
       def price(self):
           '''提供getter方法'''
           print(self._price)

       @price.setter
       def price(self, value):
           '''提供setter方法'''
            # 三元运算  为真的值 if 条件 else 条件为假的值
           self._price = float(value) if isinstance(value, str) else value

       # 删除(了解)
       @price.deleter
       def price(self):
           del self._price

   if __name__ == '__main__':
       goods = Goods()
       goods.price = 1.00
       print(goods.price)
   ```

   注：

   - 经典类中的属性只有一种访问方式，其对应被 `@property` 修饰的方法。

   - 新式类中的属性有三种访问方式，并分别对应了三个被`@property`、`@方法名.setter`、`@方法名.deleter`修饰的方法；

### 8、举个栗子2\(静态方法\)

1. 静态字段方式

   ```python
   class User(object):

       def get_name(self):
           return self._name

       def set_name(self, name):
           self._name = name

       def del_name(self):
           del self._name
           """
           property的构造方法中有个四个参数。
           第一个参数是方法名，调用 对象.属性时自动触发执行方法；
           第二个参数是方法名，调用 对象.属性 ＝ XXX时自动触发执行方法；
           第三个参数是方法名，调用 del 对象.属性时自动触发执行方法；
           第四个参数是字符串，调用 对象.属性.__doc__，此参数是该属性的描述信息。
           """
       UNAME = property(get_name, set_name, del_name)

   if __name__ == '__main__':
       user = User()
       # 调用set_name()方法
       user.UNAME = '小明'
       # 调用get_name()方法
       print(user.UNAME)
       # 删除属性
       del user.UNAME
   ```

2. django框架源码

   ```python
   class BaseForm(StrAndUnicode):

       def _get_errors(self):
           "Returns an ErrorDict for the data provided for the form"
           if self._errors is None:
               self.full_clean()
           return self._errors

       errors = property(_get_errors)
   ```


   注意:

   ​    当使用静态字段的方式创建属性时，经典类和新式类无区别




