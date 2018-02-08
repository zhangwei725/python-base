# 面向对象三大特性

## 一、继承

### 1、概念

> ![](http://opzv089nq.bkt.clouddn.com/18-2-6/62696232.jpg)
>
> 继承是一种创建类的方法，在python中，一个类可以继承来自一个或多个父类。那这个类我们通常叫子类（Sub class），原始类称为基类或超类（Base class、Super class）。

### 2、什么时候用继承

> 假如已经有几个类，而类与类之间有共同的字段和方法，那就可以把这几个字段和方法提取出来作为基类的属性。而特殊的字段和方法，则在本类中定义，这样只需要继承这个基类，就可以访问基类的变量属性和函数属性。可以提高代码的可扩展性。

### 3、语法

1. 单继承

   ```python
   class 类名 (父类名)
   ```

2. 多继承

   ```
   class 类名 (父类1，父类2，父类n...)
   ```

### 4、特点\(作用\)

1. 减少代码量和灵活指定型类
2. 子类具有父类的方法和属性
3. 子类不能继承父类的私有方法或属性\(注意\)
4. 子类可以添加新的方法
5. 子类可以修改父类的方法\(重写\)

### 6、举例说明\(单继承\)

1. 栗子1

   ```python
    """
    生命值582.24(+100 / 每级)
    魔法值263(+37.5 / 每级)
    护甲30(+4 / 每级)
    射程175
    攻击速度0.625(+1 / 每级)
    移动速度340
    攻击力56(+5 / 每级)
    生命回复9.845(+0.95 / 每级)
    法力回复6.585(+0.35 / 每级)
    魔法抗性32.1(+1.25 / 每级)
    """
   class Jinx(object):
       """
       nickname      昵称
       grade         等级
       hp            血量
       mp            魔法值
       hero_range    应用射程
       agg  攻击力
       speed         速度
       """
       camp = 'Demacia'

       def __init__(self, nickname, grade,
                    hp, mp, hero_range,
                    agg, speed,physical_resistance):
           self.nickname = nickname
           self.grade = grade
           self.hp = hp
           self.mp = mp
           self.hero_range = hero_range
           self.agg = agg
           self.speed = speed
           self.physical_resistance = physical_resistance

       def attack(self, enemy):
           enemy.hp -= self.agg

   class Garen(object):
       camp = 'Demacia'
       """
       nickname      昵称
       grade         等级
       hp            血量
       mp            魔法值
       hero_range    应用射程
       agg  攻击力
       speed         速度
       spell_resistance魔法抗性
       """
       def __init__(self, nickname, grade,
                    hp, mp, hero_range,
                    agg, speed,spell_resistance):
           self.nickname = nickname
           self.grade = grade
           self.hp = hp
           self.mp = mp
           self.hero_range = hero_range
           self.agg = agg
           self.speed = speed
           self.spell_resistance = spell_resistance

       def attack(self, enemy):
           enemy.hp -= self.agg

   if __name__ == '__main__':
       # 暴走萝莉初始化
       jinx = Jinx('快扶我起来,我还能送', 1, 1000, 300, 175, 56, 300)
       # 盖伦初始化
       garen = Garen('泉水有妹子', 1, 1000, 300, 175, 56, 300)
       jinx.attack(garen)
       print(garen.hp)
   ```

   分析,发现这两个类有很多相同的属性 这个时候我们就可以使用继承的方式去写了

   ![](http://opzv089nq.bkt.clouddn.com/18-2-5/14598835.jpg)

2. 栗子2\(继承方式\)

   ```python
   class Hero(object):
       def __init__(self, nickname, grade, hp, mp, hero_range, agg, speed):
           self.nickname = nickname
           self.grade = grade
           self.hp = hp
           self.mp = mp
           self.hero_range = hero_range
           self.agg = agg
           self.speed = speed
       def attack(self, enemy):
           enemy.hp -= self.agg

   class Jinx(Hero):
       def __init__(self, nickname, grade, hp, mp, hero_range, agg, speed, physical_resistance):
           Hero.__init__(self, nickname, grade,hp, mp, hero_range, agg, speed)
           self.physical_resistance = physical_resistance
       # 不调用父类的方法
       def attack(self, enemy):
           print(self.nickname + '--->正在攻击敌人!!!')
       # 子类添加自己的新方法
       def skill(self):
           self.hp += 500

   if __name__ == '__main__':
       jinx = Jinx('快扶我起来,我还能送', 1, 1000, 300, 175, 56, 300, 35.1)
       print(jinx.nickname)  # 调用父类的字段
       jinx1 = Jinx('快扶我起来,我还能送', 1, 1000, 300, 175, 56, 300, 35.1)
       # 输出 快扶我起来,我还能送--->正在攻击敌人!!!
       jinx.attack(jinx1)  
       # 输出 1000
       print(jinx1.hp)
       jinx.skill()
        # 输出  1500
       print(jinx.hp)
   ```

   说明:

   * 第一步：抽象父类,把公共的变量和方法写在父类里
   * 第二步：写一个子类继承父类
   * 第三步：重写`__init()__`\(构造方法\),添加子类扩展的字段,在方法里调用父类的`__init()__`方法\(非必要\)
   * 第四步：重写父类非私有化的方法\(非必要\)
   * 第五步：子类扩展方法

   示例图

   * ![](http://opzv089nq.bkt.clouddn.com/18-2-5/53047598.jpg)

   注意: 通过上面的attack\(\)方法发现敌人的血量并没有减少

### 6 、继承中的一些特点

1. 在继承中父类的构造（`__init__`\(\)方法）不会被自动调用，它需要在其派生类的构造中亲自专门调用。
2. 在调用父类的方法时，需要加上基类的类名前缀，且需要带上self参数变量。区别于在类中调用普通函数时并不需要带上self参数
3. Python总是首先查找对应类型的方法，如果它不能在派生类中找到对应的方法，它才开始到基类中逐个查找。（先在本类中查找调用的方法，找不到才去基类中找

## 二、多重继承\(multiple-inheritance\)

### 1、概念

> 很多人觉得多重继承得不偿失.不支持多重继承的 Java 显然没有什么损失,C++ 对多重继承的滥用伤害了很多人,这可能还坚定了使用 Java 的决心.然而,Java的巨大成功和广泛影响,也导致很多刚接触Python的程序员没怎么见过真实的代码使用多重继承。概念很简单,**一个类可以从Python中的多个基类派生出来。这被称为多重继承。**但是困难的工作是如果子类调用一个自身没有定义的属性，它是按照何种顺序去到父类寻找呢，尤其是众多父类中有多个都包含该同名属性。开发时，应该尽量避免这种容易产生混淆的情况。如果父类之间存在同名的属性或者方法，应该尽量避免使用多继承

### 2、举个栗子

1. 简单实例

   ```python
   class Mother(object):
       pass
   class Father(object):
       pass
   # 多重继承
   class Child(Mother, Father):
       pass
   ```

   ![](http://opzv089nq.bkt.clouddn.com/18-2-6/87412651.jpg)

2. 栗子

   ```python
   class Father(object):
       def __init__(self, name, age, sex, height):
         self.name = name
         self.age = age
         self.sex = sex
         self.__height = height

        def work(self):
           print('Father')
           print('s% 在辛勤的劳动!!!' %self.name)

   class Monter(object):
       def __init__(self, name, age, sex, height):
         self.name = name
         self.age = age
         self.sex = sex
         self.__height = height
       def work(self):
          print('Monter')
          print('s% 在辛勤的劳动!!!' %self.name)

       def make_baby(self)
           print('能生小孩')

   class Child(Mother, Father):
       def __init__(self, name, age, sex):
           super().__init__(name, age, sex)
       def work(self):
          print('Child')
          print('s% 在辛勤的劳动!!!' %self.name)

   if __name__ == '__main__':
       child = Child('小明', 18, 'man')
       print(child.name)
       child.work()
   ```

3. 栗子

   ```python
   class Vehicle(object):
       """
       engine 引擎
       seat   座位
       weight=0 重量
       """
       def __init__(self, engine, seat, weight=0):
           self.weight = weight
           self.engine = engine
           self.seat = seat

       def show_weight(self):
           print(self.weight)

       def move(self):
           pass

   class Car(Vehicle):
       """
       color 颜色
       wheel 轮子
       tp 型号 0:未定义 1:轿车 2:卡车 3越野车
       """
       def __init__(self, engine, seat, color, wheel, tp=0, weight=0):
           Vehicle.__init__(self, engine, seat, weight)
           self.color = color
           self.type = tp
           self.wheel = wheel

       def show_type(self):
           if self.type == 1:
               print('轿车')
           elif self.type == 2:
               print('卡车')
           elif self.type == 3:
               print('越野车')
           else:
               print('汽车型号未定义')

       def move(self):
           print('小汽车在公路上移动!!!')

   class Boat(Vehicle):
       """
       tonnage 吨位
       """
       def __init__(self, engine, seat, tonnage, weight=0):
           Vehicle.__init__(self, engine, seat, weight)
           self.tonnage = tonnage

       def move(self):
           print('轮船在水里移动!!!')

   class AmphibianCar(Car, Boat):

       def __init__(self, engine, seat, tonnage, weight=0):
           super().__init__(self, engine, seat, weight, tonnage)

       def move(self):
           print('111')
           super().move()

   if __name__ == '__main__':
       ac = AmphibianCar('', 4, 5, 1000)
       ac.move()
   ```

   ![](http://opzv089nq.bkt.clouddn.com/18-2-7/33611019.jpg)

4. 栗子\(综合\)

   从大学在册人员产生学生和教职工。

   再从学生派生研究生。如果考虑到研究生可以当助教，那么他们又有了教职工的特性。

   教职工可分为教师和行政人员，但行政人员也可以去授课，兼有教师的特点等。这就是多继承，

   ![](http://opzv089nq.bkt.clouddn.com/18-2-6/22858806.jpg)

   ```python
   class  Person(object):
     def __init__(self, id, name):
       self.id = id
       self.name = name
   ```

### 处理多继承的原则

继承有很多用途,而多重继承增加了可选方案和复杂度.使用多重继承容易得出令人费解和脆弱的设计.我们还没有完整的理论,根据上面的内容,下面是总结的避免把类图搅乱的一些建议:

1. 把接口继承和实现继承区分开 使用多重继承时,一定要明确一开始为什么创建子类。主要原因可能有:

   * 继承接口,创建子类型,实现“是什么”关系

   * 继承实现,通过重用避免代码重复

     其实这两条经常同时出现,不过只要可能,一定要明确意图。通过继承重用代码是实现细 节,通常可以换用组合和委托模式。而接口继承则是框架的支柱.

2. 使用抽象基类显式表示接口

   Python 中,如果类的作用是定义接口,应该明确把它定义为抽象基类.Python 3.4及以上的版本中,我们要创建`abc.ABC`或其他抽象基类的子类.

3. 通过混入重用代码

   如果一个类的作用是为多个不相关的子类提供方法实现,从而实现重用,但不体现“是什么”关系,应该把那个类明确地定义为混入类\(mixin class\)。从概念上讲,混入不定义新类型,只是打包方法,便于重用.混入类绝对不能实例化,而且具体类不能只继承混入类.混入类应该提供某方面的特定行为,只实现少量关系非常紧密的方法.

4. 在名称中明确指明混入

   因为在Python中没有把类声明为混入的正规方式,所以强烈推荐在名称中加入 `xxxMixin`后缀.

5. 抽象基类可以作为混入,反过来则不成立

   抽象基类可以实现具体方法,因此也可以作为混入使用.不过,抽象基类会定义类型,而混入做不到.此外,抽象基类可以作为其他类的唯一基类,而混入决不能作为唯一的超类,除非继承另一个更具体的混入——真实的代码很少这样做.

   抽象基类有个局限是混入没有的:抽象基类中实现的具体方法只能与抽象基类及其超类中的方法协作.这表明,抽象基类中的具体方法只是一种便利措施,因为这些方法所做的一切,用户调用抽象基类中的其他方法也能做到.

6. 不要子类化多个具体类

   具体类可以没有,或最多只有一个具体超类.也就是说,具体类的超类中除了这一个具体超类之外,其余的都是抽象基类或混入.例如,在下述代码中,如果 `Alpha` 是具体类,那么 `Beta` 和 `Gamma` 必须是抽象基类或混入:

   ```
    class MyConcreteClass(Alpha, Beta, Gamma):
        """这是一个具体类,可以实例化。"""
        # ......更多代码......
   ```

7. 为用户提供聚合类

   如果抽象基类或混入的组合对客户代码非常有用,那就提供一个类,使用易于理解的方式把它们结合起来.Grady Booch把这种类称为聚合类\(aggregate class\). 例如,下面是 tkinter.Widget 类的完整代码:

   ```
    class Widget(BaseWidget, Pack, Place, Grid):
        """Internal class.
        Base class for a widget which can be positioned with the
        geometry managers Pack, Place or Grid.
        """
        pass
   ```

8. 优先使用对象组合,而不是类继承

   这句话引自"设计模式:可复用面向对象软件的基础"一书.

   熟悉继承之后,就太容易过度使用它了。出于对秩序的诉求,我们喜欢按整洁的层次结构放置物品,程序员更是乐此不疲.然而,优先使用组合能让设计更灵活。例如,对 tkinter.Widget 类来说,它可以不从全部几何管理器中继承方法,而是在小组件实例中维护一个几何管理器引用,然后通过它调用 方法。毕竟,小组件“不是”几何管理器,但是可以通过委托使用相关的服务。这样,我 们可以放心添加新的几何管理器,不必担心会触动小组件类的层次结构,也不必担心名称 冲突。即便是单继承,这个原则也能提升灵活性,因为子类化是一种紧耦合,而且较高的 继承树容易倒.组合和委托可以代替混入,把行为提供给不同的类,但是不能取代接口继承去定义类型层次结构.

## 三、覆盖\(Override\)

### 1、什么是重写

> 当子类和父类有同名成员的时候，子类的成员会覆盖父类的同名成员

### 2、什么时候重写

> 当父类的方法不满足子类的需求的时候就需要重写

### 3、举个栗子

上面的代码, 如果去掉继承父类的构造方法那一行

1. 栗子\(重写初始化方法\)

   ```python
   class Hero(object):
       def __init__(self, nickname, grade, hp, mp, hero_range, agg, speed):
           self.nickname = nickname
           self.grade = grade
           self.hp = hp
           self.mp = mp
           self.hero_range = hero_range
           self.agg = agg
           self.speed = speed
           print('父类方法的init')

       def attack(self, enemy):
           enemy.hp -= self.agg

   class Jinx(Hero):
       def __init__(self, nickname, grade, hp, mp, hero_range, agg, speed, physical_resistance):
              Hero.__init__(self, nickname, grade,hp, mp, hero_range, agg, speed)
           print('子类方法中的init方法')
           self.physical_resistance = physical_resistance
       # 不调用父类的方法
       def attack(self, enemy):
           print(self.nickname + '--->正在攻击敌人!!!')
       # 子类添加自己的新方法
       def skill(self):
           self.hp += 500

   if __name__ == '__main__':
       jinx = Jinx('快扶我起来,我还能送', 1, 1000, 300, 175, 56, 300, 35.1)
       print(jinx.nickname) 
        '''
        如果注释掉 Hero.__init__(self, nickname, grade,hp, mp, hero_range, agg, speed)
        AttributeError: 'Jinx' object has no attribute 'nickname'
        '''
       print(jinx.physical_resistance)
   ```

   说明

   既然父类方法和子类方法都有相同的方法,那他是如何查找的呢?

   当我们调用子类的`__init__`\(\)方法时，优先在子类中查找, 子类查找不到再去父类中查找，父查找不到再去父类的父类中查找，依次内推，直到最顶层的对象\(多重继承中子类优先调用最先继承的父类\)

   ![](http://opzv089nq.bkt.clouddn.com/18-2-5/44645869.jpg)

2. 栗子

   ```python
   class Hero(object):
       def __init__(self, nickname, grade, hp, mp, hero_range, agg, speed):
           self.nickname = nickname
           self.grade = grade
           self.hp = hp
           self.mp = mp
           self.hero_range = hero_range
           self.agg = agg
           self.speed = speed
        # 重写普通方法
       def attack(self, enemy):
           enemy.hp -= self.agg

   class Jinx(Hero):
       def __init__(self, nickname, grade, hp, mp, hero_range, agg, speed, physical_resistance):
           self.physical_resistance = physical_resistance
       # 不调用父类的方法
       def attack(self, enemy):
           print(self.nickname + '--->正在攻击敌人!!!')
       # 子类添加自己的新方法
       def skill(self):
           self.hp += 500

   if __name__ == '__main__':
       jinx = Jinx('快扶我起来,我还能送', 1, 1000, 300, 175, 56, 300, 35.1)
   ```

3. 栗子\(重写字段\)

   ```python
   class Parent(object):
       NAME = 'PARENT'
       def print(self):
           print(Parent.NAME)

   class Child(Parent):
       NAME = 'CHILD'
       def print(self):
           print(Child.NAME)

   if __name__ == '__main__':
       parent = Parent()
       parent.print()
       #
       child = Child()
       child.print()
   ```

### 4、重写父类方法的两种情况

#### 4.1、完全覆盖父类的方法

> 父类的方法实现和子类的方法实现，完全不同，子类可以重新编写父类的方法实现。具体的实现方式，就相当于在子类中定义了一个和父类同名的方法并且实现

#### 4.2、对父类方法进行扩展

> 子类的方法实现中包含父类的方法实现。\(也就是说，父类原本封装的方法实现是子类方法的一部分\)。
>
> 具体的实现方式，在子类中重写父类的方法，在需要的位置使用`super().父类方法`来调用父类的方法或者**父类名.父类方法**，代码其他的位置针对子类的需求，编写子类特有的代码实现。比较常用的应用场景比如`__init__`\(\)方法

#### 4.3、举个栗子

1. 栗子1

   ```python
   class Parent(object):
       def print(self):
           print('这个是父类的输出方法')

   class Child(Parent):
       def print(self):
           print('这个是子类的输出方法')

   if __name__ == '__main__':
       child = Child()
       # 完全重写父类的方法
       child.print()
   ```

2. 栗子2

   ```python
   class Parent(object):
       def print(self):
           print('这个是父类的输出方法')

   class Child(Parent):
       def print(self):
           print('先调用子类的方法')
           Parent.print()

   if __name__ == '__main__':
       child = Child()
       # 完全重写父类的方法
       child.print()
       '''
       先调用子类的方法
       这个是父类的输出方法
       '''
   ```

## 四、super

### 5.1、说明

> 在Python中super是一个特殊的类\(其它面向对象语言中是关键字\)，super\(\)就是使用super类创建出来的对象，最常使用的场景就是在重写父类方法时，调用在父类中封装的方法实现。
>
> 是用来解决多重继承问题的，直接用类名调用父类方法在使用单继承的时候没问题，但是如果使用多继承，会涉及到查找顺序（MRO）、重复调用（钻石继承）等种种问题。
>
> MRO 就是类的方法解析顺序表, 其实也就是继承父类方法时的顺序表。

### 5.2、语法结构

1. 语法格式

   ```python
   super(type[, object-or-type])
   super()
   ```

2. 参数说明

   * type — 类名
   * bject-or-type -- 类对象，一般是 self

3. 注意事项

   * Python 3 可以使用直接使用 super\(\).xxx 

4. Python2.x super\(Class, self\).xxx

### 5.3、举个栗子

1. 栗子

   ```python
   class Person:
       def __init__(self,name,sex,age):
           self.name=name
           self.age=age
           self.sex=sex

       def walk(self):
           print('%s :在走路'%self.name)

       def speak(self): 
           print('%s:在说话'%self.name)

   class China(Person):
       country='China'
       def __init__(self,name,sex,age,language='Chinese'):
           super().__init__(name,sex,age)  #super() 绑定 调用父类方法
           self.language=language

       def walk(self,postural):
           # python3语法(推荐)
           super().walk() 
           # python2语法
           # super(China,self).walk() 
           print(self)
   ```

### 5.3、深入 super\(\)

#### 1、问题

> Python中既然可以直接通过父类名调用父类方法为什么还会存在super函数？比如
>
> ```python
> class Child(Parent): 
>     def __init__(self):     
>         Parent.__init__(self)
>         super().__init__(self)
> ```
>
> 这两种方式有啥区别
>
> 注意:
>
> **super 不是父类！super 不是父类！super 不是父类！ super 指的是 MRO 中的下一个类！**

#### 2、实现原理

1. 源代码

   ```python
   def super(cls, inst):
       mro = inst.__class__.mro()
       return mro[mro.index(cls) + 1]
   ```

2. 说明

   * inst

     生成 MRO 的 list

   * cls

     定位当前 MRO 中的 index, 并返回 mro\[index + 1\]

#### 3、MRO

##### 3.1、概念

> MRO（Method Resolution Order）：方法解析顺序
>
> 多继承是Python语言的一个重要特性，但是多继承会引发很多问题，比如二义性，Python中一切皆引用，这使得他不会像C++一样使用虚基类处理基类对象重复的问题，但是如果父类存在同名函数的时候还是会产生二义性，Python中处理这种问题的方法就是MRO
>
> **注:**
>
> **二义性:**在派生类中对基类成员的访问应该是唯一的.但是,在多继承情况下,可能造成对基类中某个成员的访问出现了不一致的情况,这时就称对基类成员的访问产生了二义性
>
> * 原因一：派生类在访问基类成员函数时，由于基类存在同名的成员函数，导致无法确定访问的是哪个基类的成员函数，因此出现了二义性错误。
>
> * 原因二：当一个派生类从多个基类派生时，而这些基类又有一个共同的基类，当对这个共同的基类中说明的成员进行访问时，可能出现二义性问题
>
> **C++虚基类:**如果一个派生类有多个直接基类，而这些直接基类又有一个共同的基类，则在最终的派生类中会保留该间接共同基类数据成员的多份同名成员。在引用这些同名的成员时，必须在派生类对象名后增加直接基类名，以避免产生二义性，使其惟一地标识一个成员，

##### 3.2、经典类（classic class）\(Python2.2以前的版本\)

1. 概要

   经典类是一种没有继承的类，实例类型都是type类型，如果经典类被作为父类，子类调用父类的构造函数时会出错。

   这个时候Python语言解决二义性的MRO的算法为DFS\(Depth-first search， 一直往深处走，直到找到方法和者变量或者走不下去为止\)（深度优先搜索（子节点顺序：从左到右））

   搜索，顾名思义，搜索就是...搜索。搜索就是从某个点开始，不停的搜索与他相连的所有的点，然后以此接连下去，直到所有的点都被搜索到了。

2. 经典类示例1

   ```python
   class E: 
       pass
   class D:
       pass
   class C(E):
       pass
   class B(D):
       pass
   class A(B, C):
       pass
   if __name__ == '__main__':
       print(A.__mro__)
       # print(A().mro())
   ```

   ![](http://opzv089nq.bkt.clouddn.com/18-2-7/35177547.jpg)

3. 经典类示例2

   ```python
   class D:
       pass
   class C(D):
       pass
   class B(D):
       pass
   class A(B, C):
       pass

   if __name__ == '__main__':
       # 备注: 可以通过 A.mro() (Python 2 使用 A.__mro__ ) 来查看 A的 MRO 信息
       print(A.__mro__)
       print(A.mro())
   ```

   ![](http://opzv089nq.bkt.clouddn.com/18-2-7/90601037.jpg)

4. 两种继承模式DFS分析

   * 第一种，我称为一般继承模式，两个互不相关的类的多继承，这种情况DFS顺序正常，不会引起任何问题；
   * 第二种，棱形继承模式，存在公共父类（D）的多继承，这种情况下DFS必定经过公共父类（D），这时候想想，如果这个公共父类（D）有一些初始化属性或者方法，但是子类（C）又重写了这些属性或者方法，那么按照DFS顺序必定是会先找到D的属性或方法，那么C的属性或者方法将永远访问不到，导致C只能继承无法重写（override）。这也就是为什么新式类不使用DFS的原因，因为他们都有一个公共的祖先object。

5. 备注:DFS算法

   ```
      dfs(deep, ...):
        if 匹配到 or 走不下去:
          return
        elif 下一种情况 deep+1:
   ```

##### 3.3、新式类（classic class）\(Python2.2\)

1. 概要

   为了使类和内置类型更加统一，引入了新式类。新式类的每个类都继承于一个基类，可以是自定义类或者其它类，默认承于object。子类可以调用父类的构造函数。

   **这时有两种MRO的算法**  
      **1、如果是经典类MRO为DFS（深度优先搜索（节点顺序：从左到右））。**  
      **2、如果是新式类MRO为BFS（广度优先搜索（节点顺序：从左到右））。**

2. 新式类示例1

   ```
   class C(obj):
       pass
   class B(obj):
       pass
   class A(B, C):
       pass
   ```

   ​

3. 两种继承模式DFS分析

   * 第一种，正常继承模式，看起来正常，不过实际上感觉很别扭，比如B明明继承了D的某个属性（假设为name），C中也实现了这个属性name，那么BFS明明先访问B然后再去访问C，但是为什么name这个属性会是C？这种应该先从B和B的父类开始找的顺序，我们称之为单调性。
   * 第二种，棱形继承模式，这种模式下面，BFS的查找顺序虽然解了DFS顺序下面的棱形问题，但是它也是违背了查找的单调性。

   因为违背了单调性，所以BFS方法只在Python2.2中出现了，在其后版本中用C3算法取代了BFS。

[参考](http://python.jobbole.com/85685/)

## 附

### 1、重载和覆盖的区别

1. 重载（overload）和覆盖（override），在C++，Java，C\#等静态类型语言类型语言中，这两个概念同时存在。前者是为了让同一个函数名（方法名）匹配不同的参数（个数不同，类型不同）;后者是为了实现多态，在相同名称的函数（方法）和参数，在不同的类中（父类，子类），有不同的实现。
2. Python是动态类型语言，不能简单地说它支持或者不支持重载，重载仍然存在，只是以不同的方式呈现。原来我们理解的重载，都是在静态类型语言中，关心参数个数以及参数类型;在动态类型语言里的重载根本不需要关心参数类型，只需要关心参数个数。而在Python里，关心参数个数的重载是由默认参数和传递参数名称来实现的。这样，程序员就没有必要自己来写两个名称一样而参数不同的函数了！事实上，在同一个模块或者同一个类中，写两个名称相同的方法的时候（参数个数是否相同不重要），后面的那个方法会简单覆盖前面的方面;其次，在子类继承父类时，同名（不同参）的方法也会简单覆盖（子类覆盖父类）。但是，这不说明Python没有重载，它只是不需要程序员自己来实现重载（如果说程序员还需要做什么的话，那就仅仅是要定义默认参数和参数名称）。如果你需要重载的话，”默认参数+参数名传递“就能达到你想要的重载了！
3. 有贴子会说，默认参数和重载是两回事，但是我觉得，C++里不允许同时定义默认参数和重载函数是有道理的，Java里干脆取消默认参数，只有重载方法也是有道理的，这个道理，就是”默认参数和基于参数个数的重载是一回事“。只是默认参数太不好控制了，特别是遇到中间一个参数是默认参数的情况，Python提供的解决办法是：参数名传递！好牛叉的思想



