# 面向对象进阶

## 一、类与类之间的关系

### 1、概念

> 一个类被定义后，目标就是把它当成一个模块来使用，并把这些对象嵌入到你的代码中去，同其他数据类型及逻辑完成一个大的功能。
>
> 有几种方法可以在你的代码中利用类。这里主要说几种比较常见
>
> 1. 关联\(Association\) : 对象之间一种引用关系，比如客户类与订单类之间的关系。这种关系通常使用类的属性表达。关联又分为一般关联、聚合关联与组合关联。可以是单向和双向。
> 2. 聚合关系\(Aggregation\)：指的是整体与部分的关系。通常在定义一个整体类后，再去分析这个整体类的组成结构；较强于一般关联,有整体与局部的关系,并且没有了整体,局部也可单独存在。如公司和员工的关系，公司包含员工，但如果公司倒闭，员工依然可以换公司。
> 3. 组合关系\(Composition\)：是整体与部分的关系，没有公司就不存在部门组合关系是关联关系的一种，是比聚合关系还要强的关系，它要求普通的聚合关系中代表整体的对象负责代表部分的对象的生命周期；如公司和部门的关系，没有了公司，部门也不能存在了
> 4. 派生\(继承关系\): 通过子类从基类继承核心属性，不断地派生扩展功能实现

## 二、关联关系

### 1、概念

> 关系是类与类之间的联接，它使一个类知道另一个类的属性和方法。**关联可以是双向的，也可以是单向的**。关联关系一般使用实例变量,方法参数来实现

### 2、举例说明

1. 栗子1

   ```python
   class Car(object):
       def __init__(self, name, type):
           # self.name = '保时捷911'
           # self.type = '2017款 GT3 4.0L'
           self.name = name
           self.type = type
       def run(self):
           print(self.name + 'running')
   class Driver(object):
       def __init__(self, name, age, car):
           self.name = name
           self.age = age
           self.car = car
       def driver_car(self):
           print(self.name + '驾驶着' + self.car.name)
   if __name__ == '__main__':
       porsche = Car('保时捷911', '2017款 GT3 4.0L')
       driver = Driver('小明', 18, porsche)
       driver.driver_car()
   ```

   说明

   * 使用方法参数形式表示关联关系。
   * 使用实例变量表达这个意思：车是我自己的车，我“拥有”这个车。
   * 使用方法参数表达：车不是我的，我只是个司机，别人给我什么车我就开什么车，我使用这个车。

## 三、聚合

### 1、说明

> 聚合\(Aggregation\) 关系是关联关系的一种，是**强的关联关系。聚合是整体和个体之间的关系。**例如，汽车类与引擎类、轮胎类，以及其它的零件类之间的关系便整体和个体的关系。与关联关系一样，聚合关系也是通过实例变量实现的。但是关联关系所涉及的两个类是处在同一层次上的，而在聚合关系中，两个类是处在不平等层次上的，一个代表整体，另一个代表部分。

### 2、举例说明

1. 栗子1

   ```python
   class Car(object):
       def __init__(self, name, type):
           # self.name = '保时捷911'
           # self.type = '2017款 GT3 4.0L'
           self.name = name
           self.type = type
       def run(self):
           print(self.name + 'running')

   class Driver(object):
       def __init__(self, name, age, car):
           self.name = name
           self.age = age
           self.car = car

       def driver_car(self):
           print(self.name + '驾驶着' + self.car.name)

        def __str__(self):
           return self.name

   if __name__ == '__main__':
       porsche = Car('保时捷911', '2017款 GT3 4.0L')
       driver = Driver('小明', 18, porsche)
       driver.driver_car()
   ```

## 四、组合

### 1、说明

> 组合关系是关联关系的一种，表示类之间整体和部分的关系，但是组合关系中部分和整体具有统一的生存期。一旦整体对象不存在，部分对象也将不存在。部分对象与整体对象之间具有共生死的关系，比如我们经常说的**国家,没有国哪有家**，还有比如人跟心脏的关系,人死了心脏也就不存在了\(前提死者不捐献心脏,如果捐献了心脏,那就是聚合关系\)等等

### 2、举例说明

1. 栗子1

   ```python
   class Car(object):
       def __init__(self, name, type):
           # self.name = '保时捷911'
           # self.type = '2017款 GT3 4.0L'
           self.name = name
           self.type = type

       def run(self):
           print(self.name + 'running')

       def __del__(self):
           print('汽车被砸了!')

   class Driver(object):
       def __init__(self, name, age):
           self.name = name
           self.age = age
           self.car = Car('保时捷911', '2017款 GT3 4.0L')

       def driver_car(self):
           print(self.name + '驾驶着' + self.car.name)

        def __str__(self):
           return self.name

   if __name__ == '__main__':
       driver = Driver('小明', 18, porsche)
       driver.driver_car()
       # 车在人在,车毁人亡 
       del driver
   ```

2. 栗子2

   ```python
   class Cpu(object):

       def __init__(self):
           self.type = 'I7'

       def __del__(self):
           print ("cpu被销毁")

   class Computer(object):

       def __init__(self):
           self.cpu = Cpu()  # 包含Cpu类的实例对象

   if __name__ == '__main__':
       computer = Computer()
       del computer
   ```

### 3、总结

1. 关联、聚合、组合只能配合语义，结合上下文才能够判断出来，而只给出一段代码让我们判断是关联，聚合，还是组合关系，则是无法判断的
2. 组合强调同生共死,聚合强调大难临头各自飞



