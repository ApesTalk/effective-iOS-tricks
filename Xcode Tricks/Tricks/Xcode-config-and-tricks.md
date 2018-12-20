> 这里是可以提高iOS开发效率的Xcode配置与技巧。

## 提升Xcode编译速度


Xcode默认使用跟系统CPU核数相同的线程数，我们可以通过修改允许XCode使用的线程数量来提高Xcode编译速度。

查看当前系统的CPU核数和线程数：``sysctl machdep.cpu``其中：
machdep.cpu.core_count 表示核数
machdep.cpu.thread_count 表示线程数

读取Xcode当前可以使用的最大线程数：

```
defaults read com.apple.Xcode PBXNumberOfParallelBuildSubtasks
```


设置允许Xcode使用的最大线程数：
```
defaults write com.apple.Xcode PBXNumberOfParallelBuildSubtasks 8
```


其他配置，可以参考：[如何提高XCode编译速度、Xcode卡顿解决方案](https://www.jianshu.com/p/c805949c2d33)


## 禁止Xcode打印杂七杂八的系统日志


在Xcode -> Edit Scheme -> Arguments -> Environment Variables中添加OS_ACTIVITY_MODE并设置为Disable。



## 打印App启动时间信息


在Xcode -> Edit Scheme -> Arguments -> Environment Variables中添加DYLD_PRINT_STATISTICS并设置为YES。
通过这个设置，你可以查看你的App启动时间都消耗在哪些方面，如果你的App启动时间过长，可以做针对性的优化。

![DYLD_PRINT_STATISTICS](https://github.com/ApesTalk/effective-iOS-tricks/Xcode Tricks/Images/DYLD_PRINT_STATISTICS.png)

￼
## Xcode无法注释（注释快捷键不能使用）问题

某些情况下，Xcode的注释失效了，也就是Toggle Comments和Add Documentation不能使用。解决办法：
在应用程序中把Xcode改个名字，然后再改回来。

## 通过模拟器给你的APP录制一个视频（模拟器录屏功能）

在终端中执行``xcrun simctl io booted recordVideo filename.mov ``，然后在模拟器中进行操作，操作完了之后再执行``Ctrl+C``终止录屏，然后filename.mov就保存在user主目录下了。

-- 该条收集自：[Record a video of your app running in the iOS simulator](http://iosdevelopertips.com/tools/video-ios-simulator.html)


## 关于dSYM不得不说的一件事

符号表是内存地址与函数名、文件名、行号的映射表。符号表元素如下所示：
<起始地址> <结束地址> <函数> [<文件名:行号>]

**简单点说就是同一份代码，编译之后的符号表文件的uuid是一样的。** 看到uuid，大家可能已经形成思维定式了，认为每次它都会创建一个新的唯一的起到标识的作用。

很惭愧，以前由于本人思维定式（估计很多人跟我一样吧，我发现网上很多文章也是这么讲的），一直认为每次打包都会生成一个新的dSYM并生成一个新的uuid，所以有时候如果打包后忘记上传符号表到bugly，线上出现奔溃，解析不出来源代码，会很无奈地认为没有什么补救办法。其实这个时候我们只需要找到上一次打包的那个时间点（代码相同），再重新archive一下，导出dSYM文件，这个dSYM文件的uuid跟之前打包生成的app的uuid是一致的。
