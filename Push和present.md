push与present都可以推出新的界面。

present与dismiss对应，push和pop对应。

present只能逐级返回，push所有视图由视图栈控制，可以返回上一级，也可以返回根VC，其他VC。

present一般用于不同业务界面的切换，push一般用于统一业务不同界面之间的切换。

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gi5j6astrjj30hs02qdg1.jpg)

UIApplication调用cerrentNavigationController类来生成一个UINavigationController

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gi5j83fyazj30ep04eaap.jpg)

最后调用UINavigationController的pushViewController方法



