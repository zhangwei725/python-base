## 五、类

### 1、什么是类

> 在 python 中所有类型的数据都可以看成对象, 包括我们我们以前学习的所有的内置类型`int`, `float`等.
>
> 像这些 `int`, `float`, `list`这些数据类型, 就是我们**面向对象中的类**
>
> 我们可以根据需要自定义很多类型出来, 这些自定义的类型**也是我们面向对象中的类**

### 2、分类

1. 经典类
2. 新式类

### 3、自定义类的组成

![](http://opzv089nq.bkt.clouddn.com/18-1-22/56885859.jpg)

### 4、语法

1. 经典类格式

   ```python
   class 类名:
   #静态字段
   属性=值
   #私有静态字段(外部无法访问)
   _属性=值
    #私有静态字段且子类无法覆盖
   __属性=值
   def __init__(self,参数1,参数2,...):
       """"初始化方法(构造方法)"""
       #普通字段
       self.字段 = 参数1
       self.字段 = 参数2

   def 方法名(self,参数1,参数2,...):
       '''无返回值的方法'''
   def 方法名(self,参数1,参数2,...):
       '''有返回值的方法'''
       retrun 返回值
       
    @property  
    def 属性名(self):
       return obj
   ```

2. 新式类格式

   ```python
   class 类名(object):
   #静态变量
   属性=值
   #私有变量
   _属性=值
    #用来避免子类覆盖其内容
   __属性=值
   def __init__(self,参数1,参数2,...):
   """"初始化方法(构造方法)"""
   self.变量名 = 参数1
   self.变量名 = 参数2

   def 方法名(self,参数1,参数2,...):
   	pass

   ```

### 4、举个栗子

1. 栗子1

   ```python
   class Person():
       def __init__(self, name):
           self.name = name
       def say(self):
           print(self.name + ":在说话")
           
       def run(self):
           print(self.name + ':带着小姨子跑路了')

   if __name__ == '__main__':
       person = Person('小明')
      	print(person.name)
       person.say()
       person.run()
   ```

2. 说明

   ![](http://opzv089nq.bkt.clouddn.com/18-1-23/95330704.jpg)

3. 内存分析图

   ![](http://opzv089nq.bkt.clouddn.com/18-1-24/47760191.jpg)

4. 执行步骤

   1、将类加载进内存 

   2、将类变量加载进类的内存 

   3、将__init__方法的地址加载进类的内存

   4、将普通方法方法的地址加载进类的内存

   5、实例化对象分配对象内存地址

   6、将实例变量初始化加载进对象内存

5. self：

   在实例化时自动将对象/实例本身传给__init__的第一个参数，你也可以给他起个别的名字，但是正常人都不会这么做。
   因为你瞎改别人就不认识