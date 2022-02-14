在跟快影 “模板” 页相册拉起的时候看到了这段代码。

![](https://tva1.sinaimg.cn/large/0081Kckwgy1gkvhvx7b9fj30ko0ch0wu.jpg)

**红线的这段代码，自己调用自己的方法，为啥不会死循环？？？**

这就要谈及iOS黑魔法了。 Method Swizzling

在介绍黑魔法之前，需要补充一些iOS runtime里的一些基础知识。

# Runtime中 实例（Object）类（Class）和对象（id）

# 以及方法（SEL）        

## obj为Object实例对象

**1、obj为Object实例对象**

在Object-C中，Object本质上是一个struct，在这个struct中会保存一个名为isa的指针，该指针会指向该Object的类

```cpp
    typedef struct objc_object {  
         Class isa;  
    } *id;  
```

测试代码：

```objectivec
    //obj为实例变量
    id obj = [TestObject new];

    Class cls = object_getClass(obj);
    
    Class cls2 = [obj class];
    
    NSLog(@"%p" , cls);
    NSLog(@"%p" , cls2);
```

输出结果

```css
    2015-12-17 14:08:32.196 TestProject[658:29503] 0x100001140
    2015-12-17 14:08:32.197 TestProject[658:29503] 0x100001140
```

结论：当obj为实例变量时，object_getClass(obj) 与[obj class] 输出结果一致，均获得isa指针，即指向类对象的指针。

**2、obj为Class类对象**

在OC中，任何类的定义都是对象。类和类的实例没有任何本质上的区别，任何对象都有isa指针。

```cpp
    typedef struct objc_class *Class;
    struct objc_class {
          Class isa;
          Class super_class;
         /* followed by runtime specific details... */
   };
```

测试代码：

```objectivec
    //obj为实例变量
    id obj = [TestObject new];
    //classObj为类对象
    Class classObj = [obj class];
   
    Class cls = object_getClass(classObj);
    
    Class cls2 = [classObj class];
    
    NSLog(@"%p" , cls);
    NSLog(@"%p" , cls2);
```

输出结果：

```css
2015-12-17 14:25:48.785 TestProject[813:38336] 0x100001118
2015-12-17 14:25:48.786 TestProject[813:38336] 0x100001140
```

结论：当obj为类对象时，object_getClass(obj) 返回类对象中的isa 指针，即指向元类对象的指针；[obj class] 返回的则是其本身。

## SEL

SEl 是系统在编译过程中，会根据方法的名字以及参数序列生成一个用来区分这个方法的唯一ID 编号，这个ID 就是SEL类型的。

只要方法的名字和参数序列完全相同，那么他们的ID 编号就是相同的。

## Method

Method 其实就是objc_method 的结构体指针

## IMP

IMP 即 Implementation 指向函数实现的指针，如果我们能够获取这个指针，则可以直接调用该方法。

---

回到最开始的问题。

![](https://tva1.sinaimg.cn/large/0081Kckwgy1gkvhvx7b9fj30ko0ch0wu.jpg)

先看看这个方法在干嘛 

+(void)swizzleSEL:(SEL)originalSEL withSEL:(SEL)swizzledSEL

![](https://tva1.sinaimg.cn/large/0081Kckwgy1gkvnsw6x8vj30hj0gm77c.jpg)

这里实现两个方法在运行时，交换了方法。originalMethod 和 swizzledMethod 方法交换了





参考文献：

[1] https://www.jianshu.com/p/ae5c32708bc6

[2] https://www.jianshu.com/p/37e1b71ad03a