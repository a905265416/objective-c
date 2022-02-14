# 背景介绍

UICollectionView 类是 iOS6 新引进的 API，布局更加灵活，简单来说就是多列的 UITableView，所以也是存在 DataSource 和 delegate 的，其中 DataSource 为 view 提供数据源，告诉 view 要显示什么东西以及如何显示他们。delegate 提供一些样式的小细节以及用户交互的相应。

# 布局

`UICollectionViewFlowLayout`

# 代理

```objc
self.delegate = self;
self.dataSource = self;
```

把代理对象设置为自己，省去了引入第三方代理，但是这么写不是很规范，苹果官方提供的例子（UITableView）是实现了MVC模式。

一般来说应该是在 ViewController 作为控制器

```objc
# xxxViewController.m
self.xxxView.delegate = self;
self.xxxView.dataSource = self;
```

# __kindof

![](https://tva1.sinaimg.cn/large/008i3skNgy1gqmu1zqijwj31my08ejve.jpg)

一般用在方法的返回值

加了 __kindof 后，方法的返回值可以返回本类和子类，调用时也可以使用本类或者子类去接收方法的返回值。

# 重用

重用和 UITableView 类似

UITableViewCell 有个 NSString *reuseIdentifier 属性

可以在初始化 UITableViewCell 的时候传入一个特定的字符串标识来设置 reuseIdentifier（一般用 UITableViewCell 的类名）。

当 UITableView 要求 dataSource 返回 UITableViewCell 时，先通过字符标识识别到对象池中查找对应类型的 UITableViewCell 对象，如果有，就重用，如果没有，就传入这个字符串标识来初始化一个 UITableViewCell 对象。

```objective-c
 [self.tableView registerClass:[TagCell class] forCellReuseIdentifier:@"tgID"];
```

