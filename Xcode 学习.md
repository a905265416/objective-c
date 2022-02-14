# 文件夹

在 Xcode 中，有黄色的文件夹和蓝色文件夹。**蓝色文件夹是资源文件夹，不参与编译**。在这些文件夹下编写的逻辑代码是不参与编译的，其他文件也不能直接引用他们，若引用其中文件需要全路径。

![](https://tva1.sinaimg.cn/large/0081Kckwgy1gl3rja4vixj307h03awei.jpg)

将文件复制到 Xcode 中，会出现如下提示。

## ① Copy items if needed

勾选后，会自动复制一份相同的文件到工程中，引用的是复制后在工程目录中的位置。若不勾选，文件的引用位置则是文件的原位置。

## ② Create groups/Create folder references

Create groups：创建黄色文件夹

Create folder references：创建蓝色文件夹

![](https://tva1.sinaimg.cn/large/0081Kckwgy1gl3rin9z2lj30lk0d8wga.jpg)

