[className new]基本等同于[[className alloc] init]

区别只在于alloc分配内存的时候使用了zone。

zone是给对象分配内存的时候，把关联的对象分配到一个相邻的内存区域，以便于调用时消耗很少的代价，提升了程序处理速度；

为什么不推荐使用new？

如果使用new的话，初始化方法被固定死只能用init，没有办法调用initXXX

因此采用alloc的方法可以用其他定制的初始化方法。

