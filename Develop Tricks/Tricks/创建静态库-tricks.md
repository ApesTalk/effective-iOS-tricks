> 这里是可以提高iOS开发效率的创建静态库相关的配置与技巧。


## 静态库概念



静态库分为.a和.framework两种

区别：

- .framework文件默认是动态库，可以手动修改成静态库。

- .a是二进制文件，.a不能直接使用，必须借助.h文件才能使用。.framwork可以包含图片等资源在里面，可以直接使用。



-----

## 目前iOS移动设备指令集


**arm64**：iPhone5S｜ iPad Air｜ iPad mini2(iPad mini with Retina Display)

**armv7s**：iPhone5｜iPhone5C｜iPad4(iPad with Retina Display)

**armv7**：iPhone3GS｜iPhone4｜iPhone4S｜iPad｜iPad2｜iPad3(The New iPad)｜iPad mini｜iPod Touch 3G｜iPod Touch4

**armv6**： iPhone, iPhone2, iPhone3G, 第一代、第二代 iPod Touch（一般不需要去支持）


**i386**是针对intel通用微处理器32位处理器 **x86_64**是针对x86架构的64位处理器 模拟器32位处理器测试需要i386架构， 模拟器64位处理器测试需要x86_64架构， 真机32位处理器需要armv7,或者armv7s架构， 真机64位处理器需要arm64架构。



-----





## 打.a文件

1.新建项目->选择Cocoa Touch Static Library。

2.把项目的Build Archive Arcitecture Only设置为NO。

3.新建必须的文件。

4.设置暴露的头文件：target->build phases->+ new headers phases，把要暴露的头文件移动到public下。

5.选择一个模拟器，build之后，把xxx.a show in finder，保存一下。

6.选择真机，build之后，把yyy.a show in finder，保存一下。

7.通过lipo -info xxx.a 查看支持的架构。

8.合并两个.a：lipo -create xxx.a yyy.a -output path/zzz.a 。

9.使用时引入暴露的.h文件和.a文件。



-----



## 创建.bundle文件



新建一个文件夹 -> 放入需要包含的资源 -> 给文件夹添加.bundle后缀名。
