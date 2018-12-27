> 这里是可以提高iOS开发效率的NSDictionary类相关的技巧。

## 用语法糖创建实例对象

```
NSDictionary *dict = @{@"mame" : @"ApesTalk", @"github" : @"https://github.com/ApesTalk"};
```

## NSMutableDictionary防止setObject:forKey: object cannot be nil奔溃的写法

```
NSMutableDictionary *dic = [NSMutableDictionary dictionary];
[dic setObject:nil forKey:@"ApesTalk"];//crash
dic[@"ApesTalk"] = nil;//no crash
[dic setValue:nil forKey:@"ApesTalk"];//no crash

```

``dic[@"key1"]=obj ``这种方式，当obj不等于nil时实际上会调用``setObject:forKey:``方法，当obj等于nil时实际上会调用``removeObjectForKey:``方法。有点纳闷，这种语法糖写法都支持这种操作，为什么``setObject:forKey:``方法内部不能支持这种操作呢？

``setValue:forKey:``这种写法属于KVC的写法，当object不为nil时会调用``setObject:forKey:``方法，当object为nil时会调用``removeObjectForKey:``方法。
