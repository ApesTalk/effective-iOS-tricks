> 这里是可以提高iOS开发效率的NSArrayl类相关的技巧。

## 用语法糖创建实例对象

```
NSArray *array = @[@"ApesTalk", @1, @YES];
```


## 让数组中的对象执行指定方法

```
[array makeObjectsPerformSelector:@selector(description)];
[array makeObjectsPerformSelector:@selector(test:) withObject:nil];
```

## 批量删除数组中的对象

```
removeObjectsInArray:
```

**这里要注意**：数组中如果是自定义对象，那么对象必须实现``isEqual:``和``hash``方法，否则，会出现部分对象不会被删除的现象。``hash``方法在对象将被作为“唯一性”时调用，比如设置为字典的key，比如被加入到NSSet中，都会检查对象的唯一性，所以，会调用对象的``hash``方法。
