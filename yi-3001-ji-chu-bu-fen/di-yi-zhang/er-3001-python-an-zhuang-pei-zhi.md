# 安装配置

## 一、概要

> 目前，Python 有两个版本，一个是 2.x 版，一个是 3.x 版，这两个版本 是不兼容的。由于 3.x 版越来越普及，我们的课程将以最新的 Python 3.6 版本为基础。

## 二、Python下载

> Python最新源码，二进制文档，新闻资讯等可以在Python的官网查看到：
>
> Python官网：[http://www.python.org/](http://www.python.org/)
>
> 你可以在以下链接中下载 Python 的文档，你可以下载 HTML、PDF 和 PostScript 等格式的文档。
>
> Python文档下载地址：www.python.org/doc/

## 二、安装

### 1、在 Windows上安装

1. 首先，根据你的 Windows 版本（64 位还是 32 位）从 Python 的官方网 站下载 Python 3.6 对应的版本然后，运行下载的 EXE 安装包

   ![](http://opzv089nq.bkt.clouddn.com/17-12-13/76254487.jpg)

2. 双击下载包

   ![](http://opzv089nq.bkt.clouddn.com/17-12-13/26132237.jpg)

3. 安装界面

   ![](http://opzv089nq.bkt.clouddn.com/17-12-13/92373377.jpg)

4. 安装完成关闭

   ![](http://opzv089nq.bkt.clouddn.com/17-12-13/85088225.jpg)

5. 测试是否安装成功

   ![](http://opzv089nq.bkt.clouddn.com/17-12-13/35660557.jpg)

6. 自定义安装

   ![](http://opzv089nq.bkt.clouddn.com/17-12-13/8132322.jpg)

   ![](http://opzv089nq.bkt.clouddn.com/17-12-13/47614326.jpg)

7. 如果add python to path忘记勾选了可以用命令或者图形化界面配置

   命令方式

   ```
   path=%path%;C:\Python\Python3
   ```

   图形化界面配置

   ![](http://opzv089nq.bkt.clouddn.com/17-12-13/9159529.jpg)

### 2、在mac上安装

Python有两个版本，一个是2.x版，一个是3.x版，这两个版本是不兼容的，现在 Mac 上默认安装的 python 版本为  2.7 版本，若 安装 新版本需要 通过 该地址进行下载：

[https://www.python.org/downloads/mac-osx/](https://www.python.org/downloads/mac-osx/) 下载相应的版本,双击安装

如果安装了 Homebrew，直接通过命令 brew install python3 安 装即可

测试命令

![](http://opzv089nq.bkt.clouddn.com/17-12-13/19474570.jpg)

### 3、在Linux上安装

首先不管你当前在哪个目录下，输入以下命令。

```
[root@localhost /]# cd /
[root@localhost /]#
```

默认Centos7中是有python安装的，但是是2.7版本，我们需要安装py3。我们去看一下默认的py2.7在哪里。

```
[root@localhost bin]# cd /usr/bin
[root@localhost bin]# ls python*
python  python2  python2.7 
[root@localhost bin]#
```

三个显示结果中最后一个是python2.7，实际上这几个文件之间是有依赖关系的。在ls 后面加个 -al参数，如下：

依赖关系很明显就可以看到。我们要安装版本3，首先要把刚才显示的三个python文件中的第一个python给备份一下（不保留源文件，仅保留备份文件就可以）

使用如下命令：

```
[root@localhost bin]# mv python python.bak
```

python文件变成了python.bak文件，bak文件就放这里吧，再也不用管它了。避免以后麻烦，就留在这里不用删除。系统准备好了，接下来，我们要去下载了。

比较推荐下面这种方式，我们在linux上找一个目录，然后使用wget命令下载到这个目录，然后解压-&gt;安装。如下：

[https://www.python.org/ftp/python/](https://www.python.org/ftp/python/)   这个是所有的python版本存放的地方。我们想使用哪个版本就用哪个。

![img](http://images2017.cnblogs.com/blog/929887/201710/929887-20171021135301021-899974983.png)

很多版本，这里选择的是比较新的3.6.3，点进去，找到下面这个文件。Python-3.6.3.tgz

![img](http://images2017.cnblogs.com/blog/929887/201710/929887-20171021135423615-303118480.png)

然后根据地址栏的链接拼接成如下链接：（如果是其他版本道理与这个是一样的）

[https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tgz](https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tgz)

链接准备好了，我们在Centos 7上创建一个目录吧。一般选择的是/usr/local里面的，如下命令（当前我们依然还在之前的/usr/bin目录下面，先不要动，还在这里）：

```
[root@localhost bin]# mkdidr /usr/local/python3
```

目录创建好了，我们就cd切换进去就好了。

```
[root@localhost bin]# cd /usr/local/python3
[root@localhost python3]# ll
total 0
[root@localhost python3]#
```

接下来我们要用刚才的网址，把源码下载到这个目录下就OK，命令如下：

```
[root@localhost python3]# wget https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tgz
```

等待下载完成之后会在当前目录下出现一个tgz包，命令解压这个包到当前目录就可以：

```
#解压命令
[root@localhost python3]# tar -xvf Python-3.6.3.tgz
```

```
#解压完成后，查看目录下文件
[root@localhost python3]# ll
total 22148
drwxr-xr-x. 17  501  501     4096 Oct 21 12:22 Python-3.6.3
-rw-r--r--.  1 root root 22673115 Oct  3 15:47 Python-3.6.3.tgz
```

就要开始安装了，因为下载的包是未编译的，我们需要编译一下。

进入文件目录：

```
[root@localhost python3]# cd Python-3.6.3/
[root@localhost Python-3.6.3]#
```

然后如下命令（执行完这句命令之后，不要切换到别的目录，不然会非常懵逼，因为执行完之后如果去/usr/local/下面的看的话是没有python3Dir目录的）：

```
[root@localhost Python-3.6.3]# ./configure --prefix=/usr/local/python3Dir
```

稍微解释上面这句命令，这句话的大致目的就是把python的安装目录指定一下，这样的话，里面的一些bin目录、lib目录就都会存放在这个目录下面。如果不指定这个安装目录的话，最后python的安装文件将分散到linux的默认目录，不在一块。我们指定安装目录，以后卸载的话直接删除目录就可以干净卸载了。

现在我们当前目录还是在/usr/local/python3/Python-3.6.3，执行如下命令：

```
[root@localhost Python-3.6.3]# make
```

然后出来一大堆代码，等它执行完毕。接着输入以下命令：

```
[root@localhost Python-3.6.3]# make install
```

又是一大堆代码，执行完毕之后，我们就可以切换到/usr/local/python3Dir目录下去查看了

```
[root@localhost Python-3.6.3]# cd /usr/local/python3Dir/
[root@localhost python3Dir]# ll
total 0
drwxr-xr-x. 2 root root 245 Oct 21 12:26 bin
drwxr-xr-x. 3 root root  24 Oct 21 12:26 include
drwxr-xr-x. 4 root root  63 Oct 21 12:26 lib
drwxr-xr-x. 3 root root  17 Oct 21 12:26 share
[root@localhost python3Dir]#
```

接下来我们还有一点善后工作。切换到 /usr/bin目录下面吧：

```
[root@localhost python3Dir]# cd /usr/bin
#然后输入以下命令 ，创建一个软链接
[root@localhost bin]# ln -s /usr/local/python3Dir/bin/python3 /usr/bin/python
```

软链接创建完毕之后。再说个事情，就是centos的yum命令是需要python支持的，我们贸然把当期的版本更换了，万一yum出错怎么办，还是让yum依然用原来的2.7版本吧。好吧我们帮它改一下吧：

注意：下面这个操作用vi操作，不熟悉vi的同学一定要按照我的指示来，不然你一脸懵逼连修改后的文件怎么保存退出都不知道。

首先输入命令，然后回车：

```
[root@localhost bin]# vi /usr/bin/yum
```

接下来出现一个全新的界面。此时任何按键都不要动。听我指示。

首先，切换到英文输入法，再输入字符 i    是aeiou的i

然后就可以开始编辑这个文件了。

把文件开头第一行的

\#!/usr/bin/python改成\#!/usr/bin/python2.7  这样就可以了。

然后，下面保存退出。注意步骤。

首先按下ESC，然后 输入： 这个符号（需要shift组合键的）。然后输入wq  细心的同学看左下角。

![img](http://images2017.cnblogs.com/blog/929887/201710/929887-20171021144053834-1682974620.png)

然后回车就可以保存退出，回到终端界面了。

我们查看一下链接情况：

```
[root@localhost bin]# ll -a python*
lrwxrwxrwx. 1 root root   33 Oct 21 12:30 python -> /usr/local/python3Dir/bin/python3
lrwxrwxrwx. 1 root root    9 Oct 19 23:55 python2 -> python2.7
-rwxr-xr-x. 1 root root 7136 Aug  4 08:40 python2.7
lrwxrwxrwx. 1 root root    7 Oct 19 23:55 python.bak -> python2
[root@localhost bin]#
```

然后查看一下当前的python版本

```
[root@localhost bin]# python -V
Python 3.6.3
[root@localhost bin]#
```



