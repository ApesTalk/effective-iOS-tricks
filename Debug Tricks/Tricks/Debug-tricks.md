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
! [Debug Memory Graph](https://github.com/ApesTalk/effective-iOS-tricks/blob/master/Images/Debug Memory Graph.png)
程序运行过程中点击Debug Memory Graph，可以看到当前没有释放的对象，点击绿色的对象可以看到当前有哪些类正在引用它。要看调用栈信息，在Edit Scheme -> Diagnostics 下勾选Malloc Stack -> Live Allocations Only。
! [Debug Memory Graph](https://github.com/ApesTalk/effective-iOS-tricks/blob/master/Images/Not Released Object.png)

