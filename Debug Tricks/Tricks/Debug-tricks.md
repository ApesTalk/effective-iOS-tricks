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
- call：执行一段代码，对点语法不敏感。如： call (void)([[self view] setBackgroundColor:[UIColor redColor]]])
- bt：打印堆栈信息，bt all：打印所有堆栈信息。
