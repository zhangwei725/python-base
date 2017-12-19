# Python流程控制

## 一、什么是流程控制

> 在进行程序设计的时候，我们会经常进行逻辑判断，根据不同的结果做不同的事，或者重复做某件事，我们对类似这样的工作称为流程控制

## 二、分类

1. 顺序控制

   > 就是从头到尾依次执行每条语句操作

2. 条件控制\(选择控制\)

   > 基于条件选择执行语句，比方说，如果条件成立，则执行操作A，或者如果条件成立，则执行操作A，反之则执行操作B

3. 循环控制

   > 循环控制，又称为回路控制，根据循环初始条件和终结要求，执行循环体内的操作

## 三、选择控制 if语句\(决策\)

### 1、if\(单一条件\)\)

1. 语法格式

   ```python
   if <条件表达式>:
       #若干语句块
   ```

2. 执行流程图

   ![](http://opzv089nq.bkt.clouddn.com/17-12-18/87739188.jpg)

3. 说明

   * 条件表达式可以是任何一种逻辑表达式

4. 如果表达式值为true，则执行 : 后的代码，再执行后面的语句

5. 如果表达的值为false，则直接执行后面的语句

6. 示例代码

   ```
   #假设有整型变量x，判断x是否为偶数，若为偶数，则在控制台上打印“输入的数值是偶数”。
   #无论x是否为偶数，最后都要在控制台上输出x的值
   ```

### 2、if...else..

1. 语法格式

   ```python
   if <条件1>：
     执行语句块1
   else:
     执行语句块2
   ```

2. 说明

   * else子句是可选项
   * 若有,则布尔表达式的值为true,执行语句1，否则，执行语句2
   * 若无,则布尔表达式的值为true,执行语句1，否则，执行if语句的后续语句
   * 语句1或语句2可以是单语句，也可以是复合语句等

3. 执行流程图

   ![](http://opzv089nq.bkt.clouddn.com/17-12-18/70881642.jpg)

4. 示例代码

   ```python
   x = 2;
   if x<2:
      x++
   else:
      x--
   ```

### 3、if...elif…else...

1. 语法格式

   ```python
   if <条件1>：
     <语句1>
   elif <条件2>：
     <语句2>
   elif <条件3>：
     <语句3>
   ...
   else:
     <语句n>
   ```

2. 执行结构图

   ![](http://opzv089nq.bkt.clouddn.com/17-12-18/17528730.jpg)

3. 说明

   * 如果"条件1"为 True，将执行"语句1"
   * 如果"条件1"为False，将判断"条件2"
   * 如果"条件2"为 True，将执行"语句2"
   * 如果"条件2"为False，将执行"条件3"，依次内推
   * ...
   * 如果所有条件都不满足则执行else语句块

4. 示例代码

   ```python
   name = input('请输入用户名:\n')
   if name == "admin"：
       print "超级管理员"
   elif name == "user":
       print "普通用户"
   elif name == "guest":
       print "客人"
   else:
       print "黑名单"
   ```

### 4、if 嵌套

1. 语法格式

   ```python
   if 表达式1:
       语句
       if 表达式2:
           语句
       elif 表达式3:
           语句
       else
           语句
   elif 表达式4:
       语句
   else:
       语句
   ```

2. 示例代码

   ```
   num = int(input("输入一个数字："))
   if num % 2 == 0:
           if num % 3 == 0:
                   print('输入的数字既能整除2也能整除3')
           else:
                   print('输入的数字只能整除2，不能整除3')
   else:
           if num % 3 ==  0:
                   print('输入的数字只能整除3，不能整除2')
           else:
                   print('输入的数字既不能整除3，也不能整除2')
   ```

### 5、三元操作符

> 在python中没有传统的?:运算符，但有相应的处理方式

1. 语法格式

   ```python
   variable = a if exper else b
   variable = (exper and [b] or [c])[0]
   variable = exper and b or c
   ```

2. 示例代码

   ```python
   num1 = int(input('请输入第一个数字：'))
   num2 = int(input('请输入第二个数字：'))
   num3 = int(input('请输入第三个数字：'))
   max_num = 0
   max_num = num1 if num1 > num2 else num2
   max_num = num3 if num3 > max_num else max_num
   print(max_num)

   a,b=1,2  
   max = (a > b and [a] or [b])[0] #list  
   max = (a > b and a or b)
   ```

### 6、常用的操作符

> | 操作符 | 描述 |
> | --- | --- |
> | `<` | 小于 |
> | `<=` | 小于或等于 |
> | `>` | 大于 |
> | `>=` | 大于或等于 |
> | `==` | 等于，比较对象是否相等 |
> | `!=` | 不等于 |

## 四、循环 while

### 1、说明

> Python 编程中 while 语句用于循环执行程序，即在某条件下，循环执行某段程序，以处理需要重复处理的相同任务

### 2、语法格式

> ```python
> while 条件：  
>     #执行语句
>       ...
> [else:
>   #执行语句
>   ...]
> ```
>
> ![](http://opzv089nq.bkt.clouddn.com/17-12-19/27279145.jpg)

### 3、执行流程图

> ![](http://opzv089nq.bkt.clouddn.com/17-12-18/81115167.jpg)

### 4、说明

1. 判断条件可以是任何表达式，任何非零、或非空（null）的值均为true。
2. 执行流程：先判断 `while` 后的条件，如果是 `True` 则开始执行循环体，执行完毕后，再去判断 条件，如果`True` 继续执行循环体...
3. `while` 中的 `else` 是可选的。这和其他语言的很大的区别，其他的语言中 `while` 中没有 `else`。  当 `while` 中的条件为 `False` 时，开始执行 `else` 中语句。
4. 如果提供了 `else` 语句，则 `else` 语句一定执行。除非你是通过 `break` 语句退出的循环。

### 5、示例代码

1. 输出小于5的数

   ```python
   count = 0
   while count < 5:
      print (count, " 小于 5")
      count = count + 1
   else:
      print (count, " 大于或等于 5")
   ```

2. 计算 1 到 100 的总和

   ```python
   i = 0
   sun = 0
   while i < 100:
           sun+=i
           ++i
           i+=1
   print(sun)
   ```

3. 猜幸运数字游戏\(while 配合if else\)

   ```python
   lucky_num = 10
   input_num = -1
   guess_num = 0
   while lucky_num != input_num and guess_num < 3:
       print('Number:',guess_num)
       input_num = int(input('请输入一个数字:'))
       if input_num > lucky_num:
           print("这个数有点大")
       elif input_num < lucky_num:
                 print("这个数有点小")
       guess_num += 1
   if lucky_num == input_num:
        print('恭喜你')
   else:
       print('在试一次')
   ```

## 五、循环 for…in…

### 1、说明

> for循环常常使用in对序列化对象（如列表、元祖等）进行遍历
>
> 在Python中，最基本的数据结构是序列（sequence）。序列中的每个元素被分配一个序号——即元素的位置，也称为索引。第一个索引是 0，第二个则是 1，以此类推。序列中的最后一个元素标记为 -1，倒数第二个元素为 -2，一次类推。Python包含 6 中内建的序列，包括列表、元组、字符串、Unicode字符串、buffer对象和xrange对象

### 2、语法格式

1. 格式

   ```python
   for 元素 in 序列: 
       #语句块
   ```

   ![](http://opzv089nq.bkt.clouddn.com/17-12-19/34233700.jpg)

### 3、示例代码

1. 基础使用

   ```python
   s = 'hello world 666'
   for i in s:
       print(i)
   ```

2. 结合if…else...使用

   ```python
   for letter in 'laowang':     # 第一个实例
      if letter == 'o':         # 字母为 o 时跳过输出
         continue
      print ('当前字母 :', letter)
   ```

3. 使用rang函数

   ```python
   for n in range(2, 10):
       for x in range(2, n):
           if n % x == 0:
               print(n, '等于', x, '*', n//x)
               break
       else:
           # 循环中没有找到元素
           print(n, ' 是质数')
   ```

   ```python
   #如果你需要遍历数字序列，可以使用内置range()函数。它会生成数列
   range()语法：
   range(start,end,step=1):顾头不顾尾
   range(10):默认step＝1，start＝0,生成可迭代对象，包含[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
   range(1,10):指定start＝1，end＝10，默认step＝1，生成可迭代对象，包含[1, 2, 3, 4, 5, 6, 7, 8, 9]
   range(1,10,2):指定start＝1，end＝10，step＝2，生成可迭代对象，包含[1, 3, 5, 7, 9]
   ```

### 4、小结

1. for循环为迭代循环
2. 可遍历序列成员（字符串，列表，元组）
3. 可遍历任何可迭代对象（字典，文件等）
4. 可以用在列表解析和生成器表达式中

## 六、循环控制语句

### 1、break

1. 说明

   **python**中的**break语句用法**，常用在满足某个条件，需要立刻退出当前循环时\(跳出循环\)，break语句可以用在for循环和while循环语句中。简单的说，break语句是会立即退出循环，在其后边的循环代码不会被执行

2. 配合for循环使用

   ```python
   for letter in 'Python': 
     if letter == 'h':
      break
     print (letter),
   ```

3. 配合while循环使用

   ```python
   var = 10
   while var > 0:
       print(var)
       var -= 1
       if var == 5:#当var是5的时候跳出循环执行下面的代码
           break
   print("循环结束")
   ```

### 2、continue

1. 说明

   使循环跳过其主体的剩余部分，并立即进入下一次循环

2. 配合while循环使用

   ```python
   var = 10                    # 第二个实例
   while var > 0:              
      var -= 1
      if var == 3:             # 变量为 5 时跳过输出,继续循环
         continue
      print ('当前变量值 :', var)
   print ("循环结束")
   ```

3. 配合for循环使用

   ```python
   for letter in 'Python':    
       if letter == 'h':
           continue
           print ('continue语句之后...')
       print ('当前字符:', letter)
   ```

### 3、 pass

1. 说明

   当语法需要但不需要执行任何命令或代码时，Python中就可以使用`pass`语句，此语句什么也不做，用于表示“占位”的代码，

2. 基础使用

   ```python
   for letter in 'Python': 
       if letter == 'h':   
           pass            #什么都不做
           print ('pass') 
       print ('当前字母 :', letter)
   print ("循环结束...")
   ```

## 七、循环总结

> 循环是让计算机做重复任务的有效的方法，有些时候，如果代码写得有问题，会让程序陷入“死循环”，也就是永远循环下去。这时可以用 Ctrl+C 退出程序，或者强制结束 Python 进程。



