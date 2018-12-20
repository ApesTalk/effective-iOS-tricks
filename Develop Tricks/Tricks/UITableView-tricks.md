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

## UITableView常见crash原因及解决方案

- beyond bounds 数组越界
数据源发生改变之后没有及时刷新tableView。

- UITableView dataSource is not set
在执行UITableViewDataSource协议中的方法，比如cellForRow中突然tableView的dataSource变成了nil。

- failed to obtain a cell from its dataSource
在cellForRow方法中返回了nil。

