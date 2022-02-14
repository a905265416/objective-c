# 属性 Property和特性 Attribute

在 OC 开发中，类里面的属性使用`@property`关键字来定义的，然后加上若干特性。如：

```objective-c
@property (nonatomic, copy) NSString *name;
```

# 为什么要有property

在远古时期，没有`property`的时候，定义实例变量需要在 .h 文件里声明 setter 和 getter 方法，再在 .m 文件里实现 setter 和 getter，这样就可以封装起来，供其他类访问（取值，赋值）了。

如果不用 setter 和 getter，其他类可以通过`->`来直接访问：

```objective-c
personA->name = @'peng'
```

## 既然这样，那么为什么要用 setter 和 getter？

主要是有三个原因：

+ 可以在 setter 和 getter 中添加额外的代码，实现特定的目的。比如赋值前，需要实现一些特定的内部计算，或者更新状态，缓存数据等等；
+ KVC和KVO基于此实现；
+ 在非 ARC 时代，可以在 setter 和 getter 中进行内存管理。

**为了偷懒，有了`@property`**

`@property`括号后面跟着的就是特性

```objectivec
# 以下两种方法是一样的，苹果默认
@property () NSString *name;// 或者@property NSString *name;
@property (atomic, strong, readwrite) NSString *name;
```

# Property的关键字分三类：

一、表示原子性（线程安全），有atomic和nonatomic，默认是atomic，线程安全。但是一般使用nonatomic，因为atomic线程安全开销太大，影响性能。即使需要保证线程安全，也可以通过代码控制，而不用atomic。

二、表示引用计数，有assign，strong，weak，copy。

**assign：**用于非指针变量，一般用于基础类型和C数据类型，这些类型不是对象，统一由系统栈进行管理。

**weak：**对对象的弱引用，不增加对象的引用计数，也持有对象，当对象消失时自动指向nil，防止野指针的存在。

**strong：**对对象的强引用，会增加对象的引用计数，如果指向了一个空对象，会造成野指针，平常用的多的就是strong。

**copy：**建立一个引用计数为1的新对象，赋值时对传入值进行一份拷贝，所以使用copy关键字时，将一个对象复制给这个属性，但是这个属性不会持有那个对象，而是对创建一个新对象，并将那个对象的值拷贝给它。而使用copy关键字的对象必须要实现NSCopying协议。

**unsafe_unretained：**与weak相似，声明一个弱饮用，但是当引用计数为0时，变量不会自动设置为nil，现在基本都用weak了。

三、表示读写权限的，默认是readwrite（可读可写），还有就是readonly。



# 怎么用 copy 关键字

用途：

1. NSString、NSArray、NSDictionary 等经常使用 copy 关键字，因为他们有对应的可变类型，他们之间可能进行赋值操作，为确保对象中的字符串值不会无意间变动，应该在设置新属性值时拷贝一份。

2. block 也经常使用 copy 关键字

   ```objective-c
   NSString *a = "abc";
   NSMutableString *b = a;
   ```

## 如果 NSString、NSArray、NSDictionary 不用copy，而用 strong 关键字，可能造成什么问题？

1. 因为父类指针可以指向子类对象,使用 copy 的目的是为了让本对象的属性不受外界影响,使用 copy 无论给我传入是一个可变对象还是不可对象,我本身持有的就是一个不可变的副本.
2. 如果我们使用是 strong ,那么这个属性就有可能指向一个可变对象,如果这个可变对象在外部被修改了,那么会影响该属性.

```objective-c
@property (nonatomic, strong) NSString *name1;
@property (nonatomic, strong) NSString *name2;

NSMutableString *str1 = [NSMutableString]
```

## 如果一个 mutable 类型用了 copy 不用 strong 会怎么样？

如果一个 mutable 类型用了 copy

那么在赋值的时候，其实调用了 [NSString copy] 方法。因为 mutable 类型其实是继承不可变类型，这个时候可变类型会变成不可变类型，容易引起报错。

**对不可变类型，用 copy；对可变类型，用 strong**

在非集合类对象中：对 immutable 对象进行 copy 操作，是指针复制，mutableCopy 操作时内容复制；对 mutable 对象进行 copy 和 mutableCopy 都是内容复制。用代码简单表示如下：

- [immutableObject copy] // 浅复制
- [immutableObject mutableCopy] //深复制
- [mutableObject copy] //深复制
- [mutableObject mutableCopy] //深复制

**注意⚠️**

* 可变对象 copy 后产生不可变类型，mutableCopy 后产生可变类型
* 可变对象 copy 后昌盛新的对象，mutableCopy 后产生了新的对象
* 不可变对象 copy 后还是不可变类型，mutableCopy 后生成的是可变类型
* 不可变对象 copy 后没有产生新的对象，mutableCopy 后产生新的对象

