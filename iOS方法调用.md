**在iOS中调用一个方法，基本上有三种调用方式。**

# 1、直接用对应类调用对应类方法，类对象调用对象方法。

iOS最常用的方法，消息机制

自定义类：SomeObject

 [SomeObject Test]; // 类方法的调用
SomeObject *someOb = [[SomeObject alloc] init]; 
 [someOb test];  // 对象方法的调用

这种调用方式外界在调用的时候必须要引入对应的类，其方法必须在该类的.h文件中声明。

# 2、使用performSelector方法调用



# 3、使用NSInvocation调用方法

