# 什么是Block

Block是带有自动变量值的匿名函数。

## 如何定义一个Block

和定义一个函数差不多，但是不需要写明走。

完整语法： <font color=red>^ 返回值类型 参数列表 表达式</font>

```objective-c
^int (int count){return count + 1;}
```

若没有返回值，可以省略返回值类型： <font color=red>^ 参数列表 表达式</font>

```objective-c
^void (int count){return count + 1;}
```

若不使用参数，参数列表也可以省略。

```objective-c
^void (void){printf("hello world");}
```

也可省略为如下形式：

```objective-c
^{printf("hello world");}
```

## block 的基本使用

**无参无返回值**

```objective-c
void (^MyBlockOne)(void) = ^{
  NSLog(@"无参无返回值");
};

// 调用
MyBlockOne();
```

**无参有返回值**

```objective-c
int (^MyBlockTwo)(void) = ^{
  NSLog(@"无参有返回值");
  return 2;
};

// 调用
int res = MyBlockTwo();
```

**有参无返回值**

```objective-c
void (^MyBlockThree)(int a) = ^(int a){
  NSLog(@"有参无返回值 a = %@", a);
};

// 调用
MyBlockThree(10);
```

**有参有返回值的定义和使用**

```objc
int (^MyBlockFour)(int a) = ^(int a){
  NSLog(@"有参有返回值 a = %@", a);
  return a * 2;
};

// 调用
MyBlockFour(4);
```

## 如何声明一个Block类型的变量

 <font color=red>返回值类型（^变量名称）参数列表</font>

```objc
int (^blk)(int);
```

## 用Block作为回调

在这里请求网络

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gizeq2aukzj30uu07xjtv.jpg)

在这里回调

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gizet0jr1mj30wd0aljuh.jpg)

利用Block做回调，可以先请求网络（需要耗费很多时间），先去做别的，然后再用请求得到的数据做事情。

```objectivec
- (void)querNetworkDataWithCallBack:(void(^)(id))callBack {
    id result = nil;
    
    //这里从网络中获取数据，给result赋值
    //通常较耗时，需要开子线程
    
    if (callBack) {
        callBack(result);
    }
}

- (void)test {
    [self querNetworkDataWithCallBack:^(id data) {
        //使用网络返回的数据
        //NSLog(@"%@", data);
    }];
}
```

## 截取自动变量

```objectivec
- (void)test {
    int val = 10;
    NSString *str = @"hello";
    void (^blk)() = ^ {
        NSLog(@"%@:%d", str, val);
    };
    val = 50;
    str = @"good";
    blk();
}
```

这里的运行结果是：<font color=red>hello:10</font>

而不是：<font color=red>good:50</font>

说明在Block中，Block表达式截获所使用的自动变量的值，保存了该变量的瞬间值。所以在执行Block语法后，即使改写自动变量的值也不影响执行变量的值。

# _block标识符的用法

想在Block里面改变在Block以外的变量值：

```objective-c
int a = 0;
void (^blk)(void) = ^{ a = 1;}; //这里会报错:Variable is not assignable (missing __block type specifier)
blk();
printf("a = %d", a);
```

需要加_block说明符，就能实现Block内赋值：

```objc
__block int a = 0;
void (^blk)(void) = ^{ a = 1;};
blk();
printf("a = %d", a);
```

执行结果，a=1

