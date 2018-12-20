> 这里是可以提高iOS开发效率的NSAttributedString类相关的技巧。

## 给UILabel、UITextField、UITextView、UIButton等设置富文本时必须知道的一点


在给UILabel、UITextField、UITextView、UIButton等设置富文本时，它的font和textColor属性会被富文本的第一个字符的font和textColor给覆盖掉。设置富文本之后如果再设置text，可以看到发生的改变。


```
NSDictionary *dic = @{NSFontAttributeName:[UIFont boldSystemFontOfSize:50],
                      NSForegroundColorAttributeName:[UIColor redColor],
                     };
NSMutableAttributedString *attrStr = [[NSMutableAttributedString alloc]initWithString:@"https://github.com/apestalk" attributes:dic];
[attrStr addAttribute:NSForegroundColorAttributeName value:[UIColor greenColor] range:NSMakeRange(0, 1)];
self.textView.attributedText = attrStr;
self.textView.text = @"ApesTalk";

[self.testBtn setAttributedTitle:attrStr forState:UIControlStateDisabled];
[self.testBtn setTitle:@"ApesTalk" forState:UIControlStateDisabled];
```

有时候为了偷懒，可能会像下面这样用，这就会造成问题了：

```
- (void)reloadWithContent:(NSString *)content keywords:(NSString *)keywords
{
    NSDictionary *attributes = @{NSFontAttributeName:_nameLabel.font,
                                 NSForegroundColorAttributeName:_nameLabel.textColor,//get textColor
                                 };
    NSMutableAttributedString *attributedStr = [[NSMutableAttributedString alloc]initWithString:content attributes:attributes];
    NSRange keyRange = [content rangeOfString:keywords];
    if(keyRange.location != NSNotFound){
        [attributedStr addAttribute:NSForegroundColorAttributeName value:[UIColor redColor] range:keyRange];
        [attributedStr addAttribute:NSFontAttributeName value:[UIFont systemFontOfSize:20] range:keyRange];
    }
    _nameLabel.attributedText = attributedStr;
}
```

详细请看：[使用NSAttributedString富文本踩到的坑](https://www.jianshu.com/p/943d5c0ae7b8)
