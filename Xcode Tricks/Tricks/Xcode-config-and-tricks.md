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


## 禁止Xcode打印杂七杂八的系统日志


在Xcode -> Edit Scheme -> Arguments -> Environment Variables中添加OS_ACTIVITY_MODE并设置为Disable。



## 打印App启动时间信息


在Xcode -> Edit Scheme -> Arguments -> Environment Variables中添加DYLD_PRINT_STATISTICS并设置为YES。
通过这个设置，你可以查看你的App启动时间都消耗在哪些方面，如果你的App启动时间过长，可以做针对性的优化。

![DYLD_PRINT_STATISTICS](https://github.com/ApesTalk/effective-iOS-tricks/Xcode Tricks/Images/DYLD_PRINT_STATISTICS.png)

￼