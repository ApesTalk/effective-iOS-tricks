> 这里是可以提高iOS开发效率的NSDictionary类相关的技巧。

## 用语法糖创建实例对象

```
NSDictionary *dict = @{@"mame" : @"ApesTalk", @"github" : @"https://github.com/ApesTalk"};
```

## NSMutableDictionary防止setObject:forKey: object cannot be nil奔溃的写法

NSMutableDictionary *dic = [NSMutableDictionary dictionary];
[dic setObject:nil forKey:@"key1"];//crash
dic[@"key1"] = nil;//no crash
[dic setValue:nil forKey:@"key2"];//no crash
