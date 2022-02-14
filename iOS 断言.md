# NSAssert

NSAssert() 是一个宏，用于开发阶段调试程序中的BUG，通过NSAssert() 传递表达式来判定是否属于BUG，**满足条件返回真值，程序继续运行，否则抛出异常。**

```objective-c
 #define NSAssert(condition, desc)
```

condition 是条件表达式，值为YES或NO；desc为异常描述，通常为NSString。

NSAssert() 可以出现在程序的任何一个位置。



## NSAssert 和 assert 区别

两者都是断言，主要差别是assert 在断言实在的时候只是简单的终止程序，而NSAssert 会报告出错误信息并且打印出来，所以只是用NSAssert就好。



## NSAssert 和NSCAssert

iOS中，用的最多的两对断言，NSAssert/NSCASsert 和 NSParameterAssert/NSCparameterAssert。

前者适用OC ，后者适用C 语言。所以，只用前者就好。



## NSAssert 用法

```objectivec
 int a = 1;
 NSCAssert(a == 2, @"a must equal to 2"); //第一个参数是条件,如果第一个参数不满足条件,就会记录并打印后面的字符串
```

Xcode 已经默认将release环境下的断言取消了, 免除了忘记关闭断言造成的程序不稳定. 所以不用担心 在开发时候大胆使用。



# 自定义NSAssertionHandler

NSAssertionHandler 实例是自动创建的，用于处理错误断言。如果NSAssert 和NSCAssert 条件评估为错误，会向NSAssertionHandler 实例发送一个表示错误的字符串。每个线程都有它自己的NSAssertionHandler实例。 我们可以**自定义处理方法**，从而使用断言的时候，控制台输出错误，但是程序不会直接崩溃。

给线程添加处理类

```objective-c
NSAssertionHandler *myHandler = [[MyAssertHandler alloc] init];//给当前的线程[[[NSThread currentThread] threadDictionary] setValue:myHandler forKey:NSAssertionHandlerKey];
```

自定义NSAssertionHandler后,程序能够获得断言失败后的信息,但是程序可以继续运行,不会强制退出程序