# ViewController生命周期

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghyiv4k5zbj311k090ac4.jpg)

## 1、init

相关数据初始化

## 2、loadView

视图控制器自带的视图并不是视图控制器一创建就马上创建的，而是被访问时才创建自动调用loadView，方法返回时，视图就创建好了。

- (void)loadView{
    //self.view.backgroundColor = [UIColor greenColor];//这时候view还没创建，程序会崩
    [super loadView];
    //loadView返回之后，view创建好了
    self.view.backgroundColor = [UIColor greenColor];
}

## 3、viewDidLoad

view创建完，在这里添加子控件、初始化数据。这里是执行任何其他初始化操作的入口。

**在整个生命周期内只被调用一次**

## 4、viewWillAppear（页面即将显示）

当视图将要添加到窗口中并且还不可见的时候或者上层视图移除本视图变成顶级视图时调用该方法。一般在view被添加到superview之前，切换动画之前调用。在这里可以进行一些现实钱的处理，比如键盘弹出、特殊动画、改变视图方向等。

**该方法被调用意味着控制器将一定会显示；在控制器生命周期中，该方法可能被多次调用**

## 5、viewWillLayoutSubviews（将要布局子控件时调用）

一般用于显示前，对子控件进行布局。

通知控制器将要布局view的子控件时调用；

每当视图的bounds改变，view将调整其子控件位置。

## 6、viewDidLayoutSubviews（布局子控件完成时调用）

对子控件进行初始化

## 7、viewDidapper（出现）

视图添加到窗口中或者上层视图移出图层变成顶级视图时调用，用于放置那些需要在视图显示后执行的代码。

## 8、viewWillDisappear（即将消失）

## 9、viewDidDisappear（已经消失）

## 10、dealloc（页面销毁）

## 11、didReceiveMemoryWarning

默认做法是，当控制器的view不在窗口上显示时，就会直接销毁，并调用viewDidUnload方法。

  