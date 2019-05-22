> 这里是可以提高iOS开发效率的Debug技巧。

## 查看dSYM和.ipa文件的uuid

- 查看dSYM文件的uuid

```
xcrun dwarfdump --uuid <dSYM文件路径>
```

- 查看.ipa文件的uuid

```
//把.ipa文件后缀名改成.zip并解压
$ cp Example.ipa Example.zip 
$ unzip Example.zip
$ cd Payload
$ xcrun dwarfdump --uuid Example.app/Example
```

## Xcode常用调试命令

- 打印命令：p或po，不能打印宏定义。
- call：执行一段代码，对点语法不敏感（输入过程中不自动提示）。如： ``call (void)([[self view] setBackgroundColor:[UIColor redColor]]])``或``call (void)(self.view.backgroundColor = [UIColor redColor])``
- bt：打印堆栈信息。
- bt all：打印所有堆栈信息。
- watchpoint：
    - ``watchpoint set variable son->_name`` 一定得是instance->_xx这种格式，不能用于点语法，因为这里不接受方法。用于检测变量的值发生改变。
    - ``watchpoint set expression 地址`` 观察某个地址。
- Debug Memory Graph检测内存泄漏

![Debug Memory Graph](https://github.com/ApesTalk/effective-iOS-tricks/blob/master/Images/Debug_Memory_Graph.png)

程序运行过程中点击Debug Memory Graph，可以看到当前没有释放的对象，点击绿色的对象可以看到当前有哪些类正在引用它。要看调用栈信息，在Edit Scheme -> Diagnostics 下勾选Malloc Stack -> Live Allocations Only。

![Debug Memory Graph](https://github.com/ApesTalk/effective-iOS-tricks/blob/master/Images/Not_Released_Object.png)

- 断点查看方法返回值

如果方法的最后一行代码是```return xxx;```，在该行加个断点，当程序断到这里的时候，点一下Step out，然后就可以在Variables View中看到一个Return Value和一些其他信息，选中Return Value，按下空格键就可以预览返回值的内容。

- x命令查看内存地址中的值

LLDB 调试中，可以使用examine命令（简写x）来查看内存地址中的值。x命令的语法如下所示：
x/n、f、u可选的参数。
n ：是一个正整数，表示显示内存的长度，也就是说从当前地址向后显示几个地址的内容。
f ：表示显示的格式，参见上面。如果地址所指的是字符串，那么格式可以是s，如果地十是指令地址，那么格式可以是 i。
u：表示从当前地址往后请求的字节数，如果不指定的话，GDB默认是4个bytes。u参数可以用下面的字符来代替，b表示单字节，h表示双字节，w表示四字节，g表示八字节。当我们指定了字节长度后，GDB会从指内存定的内存地址开始，读写指定字节，并把其当作一个值取出来。
