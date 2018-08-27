> 这里是可以提高iOS开发效率的NSURL类相关的技巧。

## 从NSURL中获取键值对

还在用字符串截取和匹配的方式取得NSURL中的键值对？还在判断NSURL的合法性？该试试NSURLComponents和NSURLQueryItem了：

```
//get keys and values from NSURL
NSURL *url = [NSURL URLWithString:@"https://github.com/ApesTalk/effective-iOS-tricks/search?q=NSURL+Tricks&unscoped_q=NSURL+Tricks"];
NSURLComponents *urlComponents = [NSURLComponents componentsWithURL:url resolvingAgainstBaseURL:nil];
NSMutableDictionary *params = [NSMutableDictionary dictionary];
for (NSURLQueryItem *item in urlComponents.queryItems) {
    [params setValue:item.value forKey:item.name];
}
```
