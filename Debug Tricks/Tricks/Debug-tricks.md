> 这里是可以提高iOS开发效率的Debug技巧。

## 查看dSYM文件的uuid

xcrun dwarfdump --uuid <dSYM文件路径>

## Xcode常用调试命令

- 打印命令：p或po，不能打印宏定义。
- call：执行一段代码，对点语法不敏感。如： call (void)([[self view] setBackgroundColor:[UIColor redColor]]])
- bt：打印堆栈信息，bt all：打印所有堆栈信息。
