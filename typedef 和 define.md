# typedef 类型定义

作用：给类型起别名，常用于简化类型，变量类型意义化等。

```objectivec
typedef double NSTimeInterval;  //给double取别名为NSTimeInterval（变量类型意义化）
typedef NSTimeInterval MyTime;  //给NSTimeInterval取别名为MyTime
typedef char * MyString;  //给char *取别名为MyString
```

# typedef 定义 block

实际开发中，经常需要把 block 作为一个属性，我们可以定义一个 block

例如，可以定义一个有参有返回值的 block

```objective-c
typedef int (^Myblock)(int a, int b);
```

定义属性的时候，如下即可持有这个 block

```objective-c
@property (nonatomic, copy) MyBlock myBlockOne;
```

block 的实现

```objective-c
self.myBlockOne = ^int(int a, int b) {
  return a+b;
};
```

调用

```objc
self.muBlockOne(2, 5);
```



# define 宏定义

作用：文本替换

```objc
#define MyString @"Hello World !"  //MyString替换后面的文本
#define MyString2 MyString  //MyString2替换MyString
```



# 使用注意

1. define 是文本替换，属于预编译指令，本身不参与编译，除非替换的文本中有 `;`
2. Typedef 是类型替换，语句的一种，结尾必须有 `;`