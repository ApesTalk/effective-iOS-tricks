> 这里是可以提高iOS开发效率的Document相关的配置与技巧。

## 禁止iCloud同步Document目录下的某文件

我们可以在SDWebImage这个优秀的第三方库中看到以下代码：

```
// disable iCloud backup
if (self.config.shouldDisableiCloud) {
    [fileURL setResourceValue:@YES forKey:NSURLIsExcludedFromBackupKey error:nil];
}    
```

如果要考虑到老版本的兼容性问题，可以先判断再设值：

```
NSURL *downloadsUrl = [NSURL fileURLWithPath:downloadsDir];
NSDictionary *dic = [downloadsUrl resourceValuesForKeys:@[NSURLIsExcludedFromBackupKey] error:nil];
if(!dic || ![[dic objectForKey:NSURLIsExcludedFromBackupKey] boolValue]){
    [downloadsUrl setResourceValue:@YES forKey:NSURLIsExcludedFromBackupKey error:nil];
}    
```
