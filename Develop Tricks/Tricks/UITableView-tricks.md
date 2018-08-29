> 这里是可以提高iOS开发效率的UITableView类相关的技巧。

## UITableViewStyleGrouped类型的UITableView的使用技巧

使用UITableViewStyleGrouped类型的UITableView的时候，还在为头部和底部间距问题而头大？

```
table = [[UITableView alloc]initWithFrame:CGRectZero style:UITableViewStyleGrouped];
table.backgroundColor = [UIColor clearColor];
table.separatorColor = kLineColor;
table.delegate = self;
table.dataSource = self;
//这句和上面两行位置对调效果明显不一样
table.tableFooterView = [UIView new];

-(CGFloat)tableView:(UITableView*)tableView heightForHeaderInSection:(NSInteger)section
{
     return 10.f;
}

-(CGFloat)tableView:(UITableView*)tableView heightForFooterInSection:(NSInteger)section
{
     return 0.01f;
}
```

详情请看：[UITableViewStyleGrouped类型的UITabelView使用技巧](https://www.jianshu.com/p/6597b51e6098)
