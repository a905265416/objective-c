## 1. 沙盒是什么

每个 iOS 应用都有自己的应用沙盒，就是文件系统目录，每个应用都只能在自己的沙盒内活动，不能随意跨越自己的沙盒去访问别的应用程序沙盒中的内容，iOS8 部分开放访问 extension，访问别人沙盒内的数据需要访问权限。

+ 一种安全体系的表现
+ 非代码文件都要保存在沙盒内
+ **APP 之间不能相互同，只能通过 URL Scheme 通信**

## 2. 沙盒的内容和作用

![](https://tva1.sinaimg.cn/large/008i3skNgy1gudymj11mij610m07imxn02.jpg)

——Document：保存应用运行时生成的需要持久化的数据，iTunes 会自动备份该目录，苹果建议将应用程序浏览到的文件数据保存在该目录下。

——Library：

Caches：一般存储缓存文件，图片视频等，此目录下的文件不会在程序退出时删除

Preferences：保存应用程序的所有偏好设置，通过 NSUserDefault 这个类访问应用程序的偏好设置，iTunes 会自动备份该文件目录下的内容

——tmp：临时文件目录，在程序重新运行的时候，会清空 tmp 文件夹

## 3. 通过代码获取沙盒路径

```objective-c
// 获取根目录
NSString *homePath = NSHomeDirectory();
// 获取沙盒的 Documents 目录
NSString *filePath =[[NSSearchPathForDirectoriesInDomains(NSDocumentDirectory,
NSUserDomainMask,YES)firstObject]stringByAppendingPathComponent:@"test.txt"];
// 获取 Library 文件路径
NSString filePath = [[NSSearchPathForDirectoriesInDomains(NSLibraryDirectory,
NSUserDomainMask, YES)firstObject]stringByAppendingPathComponent:@"test.txt"];
```

