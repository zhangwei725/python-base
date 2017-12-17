# Python 解释器

## 一、什么是解释

> 当我们编写Python代码时，我们得到的是一个包含Python代码的以`.py`为扩展名的文本文件。要运行代码，就需要Python解释器去执行`.py`文件。由于整个Python语言从规范到解释器都是开源的，所以理论上，只要水平够高，任何人都可以编写Python解释器来执行Python代码。所以存在多种Python解释器。

## 二、CPython

> CPython是Python的参考实现，用C编写的。它把Python代码编译成中间态的字节码，然后由虚拟机解释。CPython为Python包和C扩展模块提供了最大限度的兼容。如果你正在写开源的Python代码，并希望有尽可能广泛的用户，用CPython是最好的。用依赖于C扩展的包，CPython是你唯一的选择。所有版本的Python语言都用C实现，因为CPython是参考实现

## 三、IPython

> IPython是基于CPython之上的一个交互式解释器，也就是说，IPython只是在交互方式上有所增强，但是执行Python代码的功能和CPython是完全一样的。好比很多国产浏览器虽然外观不同，但内核其实都是调用了IE。CPython用`>>>`作为提示符，而IPython用`In [序号]:`作为提示符。

## 四、PyPy

> PyPy是另一个Python解释器，它的目标是执行速度。PyPy采用JIT技术，对Python代码进行动态编译（注意不是解释），所以可以显著提高Python代码的执行速度。
>
> 绝大部分Python代码都可以在PyPy下运行，但是PyPy和CPython有一些是不同的，这就导致相同的Python代码在两种解释器下执行可能会有不同的结果。如果你的代码要放到PyPy下执行，就需要了解[PyPy和CPython的不同点。

## 五、Jython

> Jython是运行在Java平台上的Python解释器，可以直接把Python代码编译成Java字节码执行。

## 六、IronPython

> IronPython和Jython类似，只不过IronPython是运行在微软.Net平台上的Python解释器，可以直接把Python代码编译成.Net的字节码。

## 七、小结

> Python的解释器很多，但使用最广泛的还是CPython。如果要和Java或.Net平台交互，最好的办法不是用Jython或IronPython，而是通过网络调用来交互，确保各程序之间的独立性。