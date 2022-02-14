在Objective-C里面，调用一个方法，其实在runtime层的时候会翻译成

```objective-c
objc_msgSend(receiver, SEL)
```

在继承关系中，一个比较深度的子类去调用祖先类的方法的时候，如果没有缓存，每次都会用isa指针去挨个搜索，查找链是非常长的，如果类中的方法比较多，费时费力。

在类的定义中就有方法缓存；

方法缓存的实现可以到runtime源码中看，为了优化性能，objc_msgSend是用汇编来实现的，在objc-msg-arm.s文件中，具体的实现步骤是：

1、判断receiver是否为nil

2、从缓存里面寻找SEL，找到就分发，否则进行第三步

3、跳转到_objc_msgSend_uncached，利用_class_lookupMethodAndLoadCache3方法（objc-class.mm中，具体可以看下面）寻找SEL。

