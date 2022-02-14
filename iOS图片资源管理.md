

# iOS图片资源管理

## 1.Assets.cxassets

一般是以蓝色的Assets.cxassets的文件夹形式在工程中，以Image Set的形式管理。当一组图片放入的时候同时会生成描述文件Contents.json。且在打包后以Assets.car的形式存在。

<img src="/Users/pengyuhui/Library/Application Support/typora-user-images/image-20200819174744951.png" alt="image-20200819174744951" style="zoom:67%;" />

iOS开发中一般在工程内导入两个到三个同内容不同像素的图片文件。

三张图片都是相同内容，而且图片名称的前缀相同，区别在于图片名以及图片的分辨率，开发者将这三张图片拉入ImageAssets后，Xcode会以图片前缀创建一个图片组，然后在代码中写：

使用
UIImage *image = [UIImage imageNamed:@"cover_newfunction_temp5"];

1.特性： ImageAssets 也是从图片文件中读取图片数据转为 UIImage, 只不过这些图片数据都打包在 ImageAssets 中. 还有一个最大的区别就是图片缓存. 相当于有一个字典, key 是图片名, value是图片对象. 调用imageNamed:方法时候先从这个字典里取, 如果取到就直接返回, 如果取不到再去文件中创建, 然后保存到这个字典后再返回. 由于字典的key和value都是强引用, 所以一旦创建后的图片永不销毁.

2. 优势: 性能好，节省Disk。Asset Catalogs会用一个高度优化的特殊格式来存所有图片，而不是一个一个的单独的图片资源，会更少的涉及频繁Disk I/O操作，且会按需下载适合你机型的合适分辨率的图片资源； 安全性。图片资源得到一定程度保护（Asset,car不易打开）

当一个 icon 在多个地方需要被显示的时候, 其对应的UIImage对象只会被创建一次, 而且多个地方的 icon 都将会共用一个 UIImage 对象. 减少沙盒的读取操作.

 1. ImageAssets 的使用场景
ImageAssets 最主要的使用场景就是 icon 类的图片, 一般 icon 类的图片大小在 3kb 到 20 kb 不等, 都是一些小文件.

## Resource

1.Resource 的使用方式
将文件直接拖入到工程目录下, 并告诉Xcode打包项目时候把这些图片文件打包进去. 这样在应用的".app"文件夹中就有这些图片. 在项目中, 读取这些图片可以通过以下方式来获取图片文件并封装成UIImge对象:
NSString *path = [NSBundle.mainBundle pathForResource:@"image@2x" type:@"png"];

UIImage *image = [UIImage imageWithContentsOfFile:path];

2. Resource 的特性
在 Resource 的图片管理方式中, 所有的图片创建都是通过读取文件数据得到的, 读取一次文件数据就会产生一次NSData以及产生一个UIImage, 当图片创建好后销毁对应的NSData, 当UIImage的引用计数器变为0的时候自动销毁UIImage. 这样的话就可以保证图片不会长期地存在在内存中.

3. Resource 的常用情景
由于这种方法的特性, 所以 Resource 的方法一般用在图片数据很大, 图片一般不需要多次使用的情况. 比如说引导页背景(图片全屏, 有时候运行APP会显示, 有时候根本就用不到).

4. Resource 的优点

图片的生命周期可以得到管理无疑是 Resource 最大的优点, 当我们需要图片的时候就创建一个, 当我们不需要这个图片的时候就让他销毁. 图片不会长期的保存在内存当中, 所以不会有很多的内存浪费. 同时, 大图一般不会长期使用, 而且大图占用内存一般比小图多了好多倍, 所以在减少大图的内存占用中, Resource 做的非常好.

## 把图片资源打包成bundle文件（资源猫）

1、Bundle文件，资源文件包。我们将许多图片，XIB，文本文件组织在一起，打包成一个Bundle文件；

2、Bundle文件是静态的；

## 沙盒文件目录下

1、预处理把图片复制

把需要预处理的图片打包放在zip文件里面，把zip文件放入工程，把图片存在沙盒里面

2、查找图片

先从沙盒文件查找->再从bundle查找->最后从主bundle查找。