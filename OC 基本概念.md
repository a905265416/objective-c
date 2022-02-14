# Xcode

## 基本名词

workspace：包含一个或多个Project

Project：包含一个或者多个Target，可以为Target提供Configurations和基础BuildSettings

Configurations：一组Build Setting的集合，提供了文件导入Build Setting的机制，即XCConfig

Target：代码的集合，不同类型有静态库、动态库、APP可执行文件

---

## Xcode打包流程

1、Build Phase 的步骤顺序执行

2、拖拽可以调整顺序

3、可以新建其他过程

![image-20200812154113996](/Users/pengyuhui/Library/Application Support/typora-user-images/image-20200812154113996.png)

## 编译执行流程

预处理->编译->链接->应用加载->延迟加载->执行

1、预处理：预处理又称预编译，是做代码的文本替换工作。#include（引用系列） #define（定义系列） #if（条件编译）

#include 首先查找头文件，然后无条件拷贝代码（存在不安全的风险） iOS用#import进行保护

宏：在当前行进行文本替换，反复的替换，直到不能替换。

2、编译：转为汇编再到机器码

3、链接：确认各种符号，应该如何真正的调用；没用的代码被优化掉了（不包含OC的代码）；如果是动态库，没用的代码全部保留

4、延迟加载：主要指动态库在非启动阶段加载（快手app的拍摄功能，并不是所有用户都有这个需求，启动的时候不启动，等需要的时候再加载）



OC文件拓展名

| 扩展名 | 内容类型                                                     |
| ------ | ------------------------------------------------------------ |
| .h     | 头文件。头文件包含类，类型，函数和常数的声明。               |
| .m     | 源代码文件。这是典型的源代码文件扩展名，可以包含 Objective-C 和 C 代码。 |
| .mm    | 源代码文件。带有这种扩展名的源代码文件，除了可以包含Objective-C和C代码以外还可以包含C++代码。仅在你的Objective-C代码中确实需要使用C++类或者特性的时候才用这种扩展名。 |

# 基本名词

**对象和类**

**对象：**是现实生活中的一个具体存在，看得见、摸得着，拿过来可以直接用。

**类：**物以类聚、人以群分。类是对一群具有相同特征或行为的事物的统称。抽象的，不能直接使用。例：晓东，给我找个”学生“来。

1、类和对象之间的关系：

类是模板，类的对象是根据这个模板创建出来的。类模板中有什么，对象中就有什么，绝不可能多，也绝不可能少。

2、如何设计一个类：

类的作用用来描述一群具有相同特征和行为的事物的。

设计类的三要素：

->类的名字。需要描述这类事物的名字；

->这类事物具有的相同特征，这类事物拥有什么；

->这类事物具有的共同行为，这类事物会做什么。

3、如何找到类：

名次提炼法：分析整个业务流程，分析出现了哪些名词，这些名词就是要找的类。



3辆坦克发射了6枚炮弹打中了3架飞机。

坦克类

​		特征：型号、大小、颜色、重量、材质、射程。

​		行为：行驶、发射。

炮弹类

​		特征：型号、大小、威力、颜色、重量。

​		行为：飞、爆炸。

飞机类

​		特征：型号、座位数量。

​		行为：飞、爆炸。

**几点注意**

a.类必须要有声明和实现

b.类名用描述的事物的名称命名，首字母必须大写

c.用来表示类事物的共同的特征变量必须要定义在@interface大括弧之中

d.为类定义属性的时候，属性的名词必须以_开头 下划线开头

**如何创建一个类的对象**

语法：类名 *对象 = [类名 new];

Person *p1 = [Person new];

根据Person这个类的模板，创建了一个对象名字叫做p1.

如何访问对象的属性：

1). 默认情况下，对象的属性是不允许被外界直接访问的。

如果要允许对象的属性可以被外界访问，那么就在声明属性的时候加@public关键字。

2).fan访问对象属性的方法

对象名->属性名 ;

(*对象名).属性名;

****



OC实例方法和类方法区别：

类方法（Class Method），有时被称为工厂方法或方便方法。工厂方法的称谓明显和一般意义上的工厂方法不同，从本质上来说，类方法可以独立于对象而执行，所以在其他的语言里面类方法有的时候被称为静态方法。

注意点一：类方法

1、类方法可以调用类方法。

2、类方法不可以调用实例方法，但是类方法可以通过创建对象来访问实例方法。

3、类方法不可以使用实例变量。类方法可以使用self，因为self不是实例变量。

4、类方法作为消息，可以被发送到类或者对象里面去。（实际上，就是可以通过类或者对象调用类方法的意思）

注意点儿

注意点二：类方法和实例方法

1、实例方法是- 类方法是+ 实例方法是用实例对象访问，类方法的对象是类而不是实例，通过创建对象或者工具类。

在实例方法里，根据继承原理发送消息给self和super其实都是发送给self

在类方法里面self是其他类的类方法，在类方法中给self发送消息只能发送类方法

2、类方法（class method）和实例方法（instance method）。类方法被限定在类范围内，不能被类的实例调用（即脱离实例运行）。alloc就是一种类方法。实例方法，限定在对象实例的范围内（即实例化之前不能运行）。init就是一种实例方法，被alloc方法返回的对象实例调用。

**使用场景**

1、如果需要访问或者修改某个实例的成员变量时，将该方法定义成实例变量（-）；

2、类方法正好相反，它不需要访问或者修改某个实例的成员变量；

3、类方法一般用于实现一些工具方法，比如对某个对象进行拓展，或者实现单例。

**单例模式**

保证一个类只有一个实例，并且提供一个全局的访问入口访问这个实例。

消息传递Message Passing

对象之间互相传递消息

在Objective-C，类别与消息的关系比较松散，调用方法视为对对象发送消息，所有方法都被视为对消息的回应。所有消息处理直到运行时（runtime）才会动态决定，并交由类别自行决定如何处理收到的消息。也就是说，一个类别不保证一定会回应收到的消息，如果类别收到了一个无法处理的消息，程序只会抛出异常，不会出错或崩溃。

```objective-c
[obj method: argument];
```

参数 argument 通过 method方法 传给 obj

```objective-c
[car fly];
```

Objective-C里，我们应当解读为"发提交一个fly的消息给car对象"，fly是消息，而car是消息的接收者。

字符串：

```objective-c
NSString* myString = @"My String\n";
NSString* anotherString = [NSString stringWithFormat:@"%d %s", 1, @"String"];
```

类：

如同所有其他的面向对象语言，类是 Objective-C 用来封装数据，以及操作数据的行为的基础结构。对象就是类的运行期间实例，它包含了类声明的实例变量自己的内存拷贝，以及类成员的指针。

包括 interface 和 implementation

interface 在头文件 包含类的声明和实例变量的定义；

implementation包含了类方法的实际代码。

Interface：

```objective-c
@interface MyObject : NSObject {
    int memberVar1; // 实体变量
    id  memberVar2;
}

+(return_type) class_method; // 类方法

-(return_type) instance_method1; // 实例方法
-(return_type) instance_method2: (int) p1;
-(return_type) instance_method3: (int) p1 andPar: (int) p2;
@end
```

Objective-C定义一个新的方法时，名称内的冒号（:）代表参数传递

```objective-c
- (void) setColorToRed: (float)red Green: (float)green Blue:(float)blue; /* 宣告方法*/

[myColor setColorToRed: 1.0 Green: 0.8 Blue: 0.2]; /* 呼叫方法*/
```

Implementation：

实现区块则包含了公开方法的实现，以及定义私有（private）变量及方法。 以关键字@implementation作为区块起头，@end结尾。

```objective-c
@implementation MyObject {
  int memberVar3; //私有变量
}

+(return_type) class_method {
    .... //method implementation
}
-(return_type) instance_method1 {
     ....
}
-(return_type) instance_method2: (int) p1 {
    ....
}
-(return_type) instance_method3: (int) p1 andPar: (int) p2 {
    ....
}
@end
```

@autoreleasepool 自动释放池

可以将代码放在自动释放池

## ARC

自动管理引用计数，依赖clang+runtime

编译器会在编译期通过强弱指针自动插入合适的代码，进行编译。

强指针：strong 需要持有该对象

弱指针：weak不持有对象，不会+1，当对象被销毁时也会跟着被销毁。

在ARC中，如果一个对象没有强指针指向，系统就会自动释放。

## 继承

继承的特性

1、单根性：一个类只能有一个父类

2、传递性：A类从B类继承，B类从C类继承，那么A类就同时拥有B、C类的成员。

# 创建对象

Objective-C创建对象需通过alloc以及init两个消息。alloc的作用是分配内存，init则是初始化对象。 init与alloc都是定义在NSObject里的方法，父对象收到这两个信息并做出正确回应后，新对象才创建完毕。以下为范例：

```objective-c
MyObject * my = [[MyObject alloc] init];
```

在Objective-C 2.0里，若创建对象不需要参数，则可直接使用new

```objective-c
MyObject * my = [MyObject new];
```

# 方法

Objective-C 中的类可以声明两种类型的方法：实例方法(+)和类方法(-)。

![img](https://www.runoob.com/wp-content/uploads/2015/08/2011022010310145.jpg)

消息被中括号( [ 和 ] )包括。中括号中间，接收消息的对象在左边，消息（包括消息需要的任何参数）在右边。例如，给myArray变量传递消息insertObject:atIndex:消息，你需要使用如下的语法：

```objective-c
[myArray insertObject:anObj atIndex:0];
```

允许嵌套消息；

```objective-c
[[myAppObject getArray] insertObject:[myAppObject getObjectToInsert] atIndex:0];
```

下面的例子演示了一个类方法如何作为类的工厂方法。在这里，arrayWithCapacity是NSMutableArray类的类方法，为类的新实例分配内容并初始化，然后返回给你。

```objective-c
SMutableArray*   myArray = nil; // nil 基本上等同于 NULL

// 创建一个新的数组，并把它赋值给 myArray 变量
myArray = [NSMutableArray arrayWithCapacity:0];
```

## 属性

```objective-c
@interface Person : NSObject {
    @public
        NSString *name;
    @private
        int age;
}

@property(copy) NSString *name;
@property(readonly) int age;

-(id)initWithAge:(int)age;
@end
```



## 动态类型

即消息可以发送给任何对象实体，无论该对象实体的公开接口中有没有对应的方法。

一个对象收到消息之后，他有三种处理消息的可能手段，第一是回应该消息并运行方法，若无法回应，则可以转发消息给其他对象，若以上两者均无，就要处理无法回应而抛出的例外。只要进行三者之其一，该消息就算完成任务而被丢弃。若对"nil"（空对象指针）发送消息，该消息通常会被忽略，取决于编译器选项可能会抛出例外。

foo可以是任意类型的实例；

```objective-c
- setMyValue:(id) foo;
```

foo可以是任意类型 需要遵守aProtocol协议 ；

foo只能是NSNumber类型实例。

```objective-c
- setMyValue:(id <aProtocol>) foo;
```

```objective-c
- setMyValue:(NSNumber*) foo;
```

## 转发OC中id数据类型

- 动态数据类型id
- 数据类型的作用

1、定义变量；2、作为函数的参数；3、作为函数的返回值

默认情况下，所有的数据类型都是静态数据类型；

在编译时就知道变量的类型，知道变量中有哪些属性和方法，在编译的时候就可以访问这些属性和方法，并且如果通过静态数据类型定义了变量，如果访问了不属于静态数据类型的属性和方法，那么编译器就会报错。

id也是一种数据类型，并且是一种动态数据类型。

动态数据类型的特点：在编译的时候编译器并不知道变量的真实类型，只有运行的时候才知道真实的数据类型，并且如果通过动态数据类型定义变量，如果访问了不属于动态类型数据的属性和方法，编译器不会报错。

在多态中，通过静态数据类型定义变量，不能调用子类的实例对象； 





转发

对一个对象发送消息，不管它是否能够响应之。除了响应或丢弃消息以外，对象也可以将消息转发到可以响应该消息的对象。转发可以用于简化特定的设计模式，例如观测器模式或代理模式。



类别（Category）

一个分类可以将方法的实现分解进一系列分离的文件。可以将一组相关的方法放进一个分类。

若分类声明了与类中原有方法同名的函数，则分类中的方法会被调用。因此分类不仅可以增加类的方法，也可以代替原用的方法。这个特性可以用于修正原油代码中的错误，更可以从根本上改变程序中原有类的行为。若两个分类中的方法同名，则被调用的方法是不可预测的。

扩展（Extension）

1、类别中原则上只能增加方法（能添加属性的原因只是通过runtime解决无setter/getter的问题而已）；

2、类拓展不仅可以增加方法，还可以增加实例变量（或者属性），只是该实例变量默认是@private类型的，使用范围只能在自身类，而不是子类或其他地方；

3、类拓展中声明的方法没被实现，编译器会报警，但是类别中的方法没被实现编译器是不会有任何报警的。。这是因为类扩展是在编译阶段被添加到类中，而分类是在运行时添加到类中。

4、类扩展不能像类别那样拥有独立的实现部分，类扩展所声明的方法必须依托对应类的实现部分类实现。

5、定义在.m文件中的类扩展方法为私有的，定义在.h文件中的类扩展方法为公有的。类扩展是在.m文件中声明私有方法的非常好的方式。

协议（Protocol）

1、协议通过关键字进行@required和@optional进行设置，若果不设置则默认是@required

2、协议通过<>进行实现，一个类可以同时实现多个协议，中间通过逗号分隔

3、协议的实现只能在类的声明上，不能放到类的实现上，只能写在@interface上 不能写在@implementation

4、协议中不能定义属性、成员变量等，只能定义方法



# 基本语法（Basic Syntax）

定义一个类的接口：

| `@interface SimpleClass : NSObject` |
| ----------------------------------- |
| ` `                                 |
| `@end`                              |

 类名： SimpleClass 

这个类继承于NSObject

属性控制

例：一个人的类，他的名字可能被调用

| @interface Person : NSObject   |
| ------------------------------ |
|                                |
| @property NSString *firstName; |
| @property NSString *lastName;  |
|                                |
| @end                           |



Person类有两个公共属性

可以通过声明数据readonly

| @interface Person : NSObject              |
| ----------------------------------------- |
| @property (readonly) NSString *firstName; |
| @property (readonly) NSString *lastName;  |
| @end                                      |



```objective-c
- (void)someMethodWithFirstValue:(SomeType)info1 secondValue:(AnotherType)info2;
```

声明方法 包含多个参数



整个项目中的类名应该独一无二

 所有在interface中声明的方法 都需要在implementation中执行它们。

| #import "XYZPerson.h"     |
| ------------------------- |
|                           |
| @implementation XYZPerson |
|                           |
| @end                      |



首先 import XYZPerson

然后implementation 执行 XYZPerson

最后end



[self message]

消息的接受者是本类对象，方法的实现从本类开始查找

[super message]

消息的接受者是本类对象，方法的实现从父类开始查找



对象是被动态创建的

分配内存：

```objective-c
+ (id)alloc;
```

 分配内存不仅需要分配当前类，还需要容纳所有父类（superclass）

alloc可以清楚对象的属性，避免内存中的垃圾造成问题，但还无法完全初始化对象。

初始化：

```objective-c
- (id)init;
```

返回对象指针的调用：

```objective-c
NSObject *newObject = [[NSObject alloc] init];
```

这里设置newObject变量指向一个新创立的NSObject实例。

init可能返回和alloc不同的对象 所以先alloc 再 init

不要init一个对象而不分配指针，像下面这样：

```objective-c
NSObject *someObject = [NSObject alloc];
[someObject init];
```

# 工厂模式

NSNumber类定义了几种工厂模式来初始化，包括：

| `+ (NSNumber *)numberWithBool:(BOOL)value;`   |
| --------------------------------------------- |
| `+ (NSNumber *)numberWithFloat:(float)value;` |
| `+ (NSNumber *)numberWithInt:(int)value;`     |
| `+ (NSNumber *)numberWithLong:(long)value;`   |

工厂模式使用方法如下：

```objective-c
NSNumber *magicNumber = [NSNumber numberWithInt:42];
```

如果不需要给实例赋值可以用new方法

| `XYZObject *object = [XYZObject new];`              |
| --------------------------------------------------- |
| `    // is effectively the same as:`                |
| `    XYZObject *object = [[XYZObject alloc] init];` |

# OC是一种动态语言

需要一个指针来追踪对象在内存中的位置。



对象的相等判断：

数值判断用 ==

```objective-c
if (someInteger == 42) 
```

当是两个对象时，用来判断两个指针是否指向同一个对象；

```objective-c
if (firstPerson == secondPerson)
```

如果要判断两个对象是否表示相同的数据，应该用 isEqual；

```objective-c
if ([firstPerson isEqual:secondPerson])
```

如果要比较两个对象代表值的大小：

```objective-c
if ([someDate compare:anotherDate] == NSOrderedAscending)
```



OC是消息结构的语言，其运行时所应执行的代码由运行环境决定，而使用函数调用的语言，则由编译器决定。

OC的重要工作都由“运行期组件”（runtime component）而非编译器来完成。使用OC的面向对象特性所需的全部数据结构及函数都在运行期组件里面。运行期组件中含有全部内存管理方法。运行期组件本质上就是一种与开发者所编代码相连接的“动态库”（dunamic library），其代码能把开发者所编写的所有程序粘合起来。这样的话，只需要更新运行期组件，即可提升应用程序性能。OC中对象所占内存总是分配在“堆空间”，而绝不会分配在“栈空间”。

NSString * some string = @"The string"

声明了一个 some string变量，变量类型是NSString* 表明这个变量存的是一个指向NSString的指针。

此时，如果再创建一个变量，另其指向同一地址，那么并不拷贝该对象，只是这两个变量会同时指向此对象。

在OC中指针变量存在**栈**上，实例存在**堆**上。

分配在堆中的内存必须直接管理，而分配在栈上的用于保存变量的内存则会在其栈帧弹出时自动清理。

OC将堆内存管理抽象出来了，不需要用malloc及free来分配或释放对象所占内存。这部分工作抽象为一套内存管理架构，名叫“引用计数”。

**堆内存和栈内存：**

1、内存区域不同，对内存是区别于栈区、全局数据区和代码区的另一个内存区域。堆允许程序在运行时动态地申请某个大小的内存空间。栈内存在函数中定义的一些基本类型的变量和对象的引用变量都在函数的栈内存中分配。

![img](https://iknow-pic.cdn.bcebos.com/35a85edf8db1cb13f62cdbc1d354564e93584b9f?x-bce-process=image/resize,m_lfit,w_600,h_800,limit_1)

2、特点不同，堆内存实际上指的就是优先队列的一种数据结构。第一个元素有最高的优先权；栈内存实际上就是满足先进后出的性质的数学或数据结构。栈内存是存取速度比堆要快，仅次于寄存器，栈数据可以共享。

3、范围不同，堆内存中分配的内存需要程序员手动释放，如果不释放，而系统内存管理器又不自动回收这些堆内存进行动态分配对内存的话，内存就一直被占用。栈内存中，为这个变量分配内存空间，当超过变量的作用与后，会自动释放掉为该变量所分配的内存空间，该内存空间可以立即被另作他用。

## 内存分配

栈区--------------------------------高地址。         

堆区

全局区（未初始化）

全局区（已完成初始化）

常量

代码区-----------------------------低地址

|          | 栈                               | 堆                            |
| -------- | -------------------------------- | ----------------------------- |
| 管理方式 | 系统编译器自动管理               | 程序员手动管理                |
| 分配方式 | 高位向低位拓展                   | 低位向高位拓展                |
| 申请效率 | 系统自动分配，连续空间速度快     | alloc分配，通过链表链接速度慢 |
| 内存大小 | 一般主线程1M，子线程512K线程独有 | 依赖系统有效虚拟内存进程共享  |



# 封装数据

Accessor method 获取或设置property values

```objective-c
NSString *firstName = [somePerson firstName];
[somePerson setFirstName:@"Johnny"];
```

如果不想数据会被setter修改，可以添加readonly属性

```objective-c
@property (readonly) NSString *fullName;
```

OC支持点语法

```objective-c
NSString *firstName = somePerson.firstName;
somePerson.firstName = @"Johnny
```

## MVC模型

模型-视图-控制器

视图对象：是用户可以看见的对象，例如按钮、文本框、滑动条。视图对象用来构建用户界面，在Quiz应用中，显示问题和答案的标签以及标签下方的按钮都是视图对象。

模型对象：负责存储数据，与用户界面无关。

控制器对象：用于控制视图对象为用户呈现的内容，以及负责确保视图对象和模型对象的数据保持一致。

=======================================================================================

# 初始化对象

self = [super init];

...

...

return self;

## self

self存在于方法中，是一个隐式局部变量。编写方法时不需要声明self，并且程序会自动为self赋值，指向收到消息的对象本身。通常情况下，self会用来向对象自己发送消息。初始化方法的最后一行代码必须返回初始化后的对象。这样，调用者才能将该对象赋给指针变量。

## super

super如何工作的？通常情况下，当某个对象收到消息时，系统会先从这个对象的类开始，查询和消息名相同的方法名。如果没找到，则会在这个对象的父类中继续查找。该查询过程会沿着继承路径向上，直到找到相应的方法名为止。

头文件的声明顺序。实例变量声明应该写在最前面，然后是类方法，接下来是初始化方法，最后是其他方法。这种排列顺序是一种约定，可以使头文件更容易阅读。

# NSArray与NSMutabkeArray

数组对象只能保存指向Objective-C对象的指针，所以不能将基本类型的变量或C结构加入数组对象。如果要将基本类型的变量和C结构加入数组，可以先将它们包装成OC对象，如@‘abc’ 这种NSNumber、NSValue和NSData。

**注意**，不能讲nil加入数组对象。如果要将‘空’加入数组对，就必须使用NSNull对象。NSNull对象的作用就是代表nil，代码如下：

[items addObject:[NSNull null]];

# 类拓展

类拓展用来隐藏私有信息，换言之，它是类的公共接口。类拓展通常被用来向类的公共接口添加额外的私有方法和属性。例如一个Person类，类中有Identifier属性，在公共接口中这一属性定义为只读，而在实现代码的上方的类拓展中将其定义为读写。这是为了让内部方法可以直接修改属性值。



Objective-C在发送消息时，哪个方法会被调用，并不是在编译时决定的，而是在应用运行的过程中决定的。不仅仅是一个可编译至机器语言的编程语言。相反，它需要一个运行时系统来执行自己的代码。可以直接同运行时系统互动。

# OC内存管理（自动引用计数）

栈内存存放指针；堆内存存放具体数据

## 强引用与弱引用

·指针变量指向某个对象，相应的对象就会多一个拥有着，并且不会被程序释放。这种指针特性称为强饮用

·程序也可以选择让指针变量不影响其指向对象的拥有者个数，这种不会改变拥有者个数的指针特性称为弱引用。

弱引用用于解决强引用循环问题。当两个对象互相拥有时，将无法通过ARC机制来释放。即使应用中的其他对象都释放了针对这两个对象的所有权，这两个对象及其拥有的所有对象也无法释放。

# property

@property NSString *name;

属性的名字时实例变量的名字去掉下画线，编译器根据属性生成实例变量时会自动在变量名前加上下画线。

任何属性都可以有一组特性，用于描述响应存取方法的行为。这些特性需要写在小括号里，病根在@property指令后面。例：

@property(nonatomic, readwrite, strong) NSString *itemName;

atomic 和 nonatomic 区别：

atomic相当于加锁，但是在iOS开发中，使用同步锁的开销比较大， 这会带来性能问题。一般情况下并不要求属性必须是“原子的”，因为这并不能保证“线程安全”(thread safety)，若要实现“线程安全”的操作，还需采用更为深层的锁定机制才醒。

# static关键字

三个作用：

1、隐藏：当我们同时编译多个文件时，所有未加static前缀的全局变量和函数都具有全局可见性。 不加static，其它源文件也可以访问数据，具有全局可见性。对于函数来说，static的作用仅限于隐藏，而对于变量，static还有其它两个作用。

2、static的第二个作用是保持变量内容的持久。存储在静态数据区的变量会在程序刚开始运行时就完成初始化，也是唯一的一次初始化。共有两种变量存储在静态存储区：全局变量和static变量，只不过和全局变量比起来，static可以控制变量的可见范围。

3、static第三个作用时默认初始化为0。

# 事件处理

事件的产生与传递。

当触摸事件后，系统会将该事件加入到一个由UIApplication管理的事件队列中，UIApplication会从事件队列中取出最前面的事件，并将事件分发下去以便处理。主窗口会在视图层次结构中找到一个最合适的视图来处理触摸事件。

用户点击屏幕产生的一个触摸事件，经由一系列的传递过程后，会找到一个最适合的视图来处理事件，找到最合适的视图控件后，就会调用控件的touches方法来作具体的事件处理。touches的默认做法是将事件顺着相应者链条向上传递，将事件交给上一个响应者处理。

**什么是响应者链条：**

​		由多个响应者对象连接起来的链条。

**什么是响应者对象：**

​		继承了UIResponder的对象

系统是如何寻早最合适的View

1、先判断自己是否能接收触摸事件

2、在判断触摸的当前点在不在自己身上

3、如果在自己身上，它会从后往前遍历子空间，遍历出每一个空间后，重启前两步

4、如果没有符合条件的子控件，那么本身就是最合适的View

# 为什么一定要call [super ViewDidLoad]

继承父类的相关属性，最好每一次写函数的时候都通过call父类来继承。写了没坏处，忘写了但确实需要的时候有问题。

# Provisioning profile

provisioning profile配置文件是数字实体的集合，这些数字实体将开发人员和设备与授权的iPhone开发团队为一地联系在一起，并使设备可以用于测试。必须在要运行应用程序代码的每个设备上安装开发配置文件。每个开发设置配置文件将包含一组iPhone开发证书，唯一设备标示符和一个应用程序ID。在配置文件中指定的设备只能由配置文件中包含iPhone开发证书的个人用于测试。一个设备可以包含多个配置文件。

如果要打包到真机上运行一个App，一般要经历以下三步：

1、需要指明它的App ID，并且验证Bundle ID是否与其一致；

2、需要证书对应的私钥来进行签名，用于标识这个App是合法、安全、完整的；

3、如果是真机调试，需要确认这台设备是否授权运行该App。

# 生命周期

iOS应用的5种状态：

1、Not Running（非运行状态）：应用没有运行或被系统终止运行；

2、Inactive（前台非活跃状态）：应用正式进入前台状态，但是还没有接受事件处理；

3、Active（前台活跃状态）：应用进入前台状态，能接受事件并且进行处理；

4、Background（后台状态）：应用进入后台之后，依然能够执行代码。如果有可以执行的代码，就会执行，如果没有可执行的代码或者将可执行的代码执行完毕，应用会马上进入挂起状态；

5、Suspended（挂起状态）：被挂起的应用进入一种“休眠”状态，不能执行任何代码。当手机系统内存不足时，应用会被终止。

应用程序架构：

iOS应用程序都遵循mvc架构架构。Model负责存储数据和处理业务逻辑，View负责显示数据和与用户交互，Controller是两者的中介，协调Model和View相互协作。

[UIApplication](https://link.jianshu.com?t=https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIApplication_Class/)对象
 用户与iOS设备交互时产生的事件(Multitouch Events，Motion Event，Remote Control Event)交由`UIApplication`对象来分发给**control objects**([UIControl](https://link.jianshu.com?t=https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIControl_Class/index.html#//apple_ref/occ/cl/UIControl))对应的**target objects**来处理并且管理整个事件循环，而一些关于app运行时重要事件委托给`app delegate`来处理。

[App delegate](https://link.jianshu.com?t=https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIApplicationDelegate_Protocol/)对象
 `App delegate`对象遵循`UIApplicationDelegate`协议，响应app运行时重要事件(app启动、app内存不足、app终止、切换到另一个app、切回app)，主要用于app在启动时初始化一些重要数据结构；例如，初始化`UIWindow`，设置一些属性，为window添加`rootViewController`。

[View controller](https://link.jianshu.com?t=https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/)对象
 `View Controller`有一个`view`属性是view层次结构中的**根view**，你可以添加子view来构建复杂的view；controller有一些`viewDidLoad`、`viewWillAppear`等方法来管理view的生命周期；由于它继承`UIResponder`，所有还会响应和处理用户事件。

[Documents](https://link.jianshu.com?t=https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDocument_Class/)和data model对象
 **data model**对象主要用来存储数据。例如，饿了么app在搜索切换地址后，有历史记录搜索地址历史，当app下次启动时，读取和显示搜索地址历史。
 **document**对象(继承UIDocument)用来管理一些或所有的data model对象。document对象并不是必须的，但提供一种方便的方式来分组属于单个文件或多个文件的数据。

[UIWindow](https://link.jianshu.com?t=https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIWindow_Class/)对象
 `UIWindow`对象位于view层次结构中的最顶层，它充当一个基本容器而不显示内容，如果想显示内容，添加一个content view到window。
 它也是继承`UIResponder`，所以它也是会响应和处理用户事件。

[View](https://link.jianshu.com?t=https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIView_Class/)、[control](https://link.jianshu.com?t=https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIControl_Class/)、[layer](https://link.jianshu.com?t=https://developer.apple.com/library/ios/documentation/GraphicsImaging/Reference/CALayer_class/)对象
 `View`对象可以通过addSubview和removeFromSuperview 等方法**管理**view的层次结构，使用layoutIfNeeded和setNeedsLayout等方法**布局**view的层次结构，当你发现系统提供view已经满足不了你想要的外观需求时，可以重写drawRect方法或通过layer属性来构造复杂的**图形外观和动画**。还有一点，UIView也是继承UIResponder，所以也能够**处理用户事件**。
 `Control`对象通常就是处理特定类型用户交互的View，常用的有button、switch、text field等。
 除了使用`View`和`Control`来构建view层次结构来影响app外观之外，还可以使用Core Animation框架的`Layer`对象来渲染view外观和构建复杂的动画。

## UIViewController

用户交互和数据展示都是由它来控制，了解它的生命周期，就能做到：在合适的时机，做合适的事情。

每个生命周期函数：

-loadView

此时，控制器的view还未初始化，可以通过重写这个方法自定义控制器的View，如果这样做，那就不能调用[super loadView]

-viewDidLoad

在控制器的生命周期中，它只会被调用一次，此时，view已经初始化好，非常适合做一些页面的初始化任务。由于此时view的bounds尚未确定，所以不适合写frame类型的布局代码，但是给视图添加约束没有影响。

-viewWillAppear

它会在控制器的视图将要出现在屏幕中时被调用，在控制器生命周期中可能会被调用多次。在此处，适合做一些与视图出现相关联的任务，例如改变状态栏的方向、风格。

-viewWillLayoutSubviews

当view的子视图即将布局时，此方法会被调用

-viewDidAppear

它会在控制器的视图出现在屏幕后被调用，此时，view的bounds已经确定，不过在这里写布局相关代码，可能会反映到屏幕上。

-viewWillDisappear

视图即将从屏幕中消失时触发

-viewDidDisappear

视图从屏幕中消失后出发。

# iOS开发证书

App ID即Product ID，用于标示一个或一组App。

在Mac/iOS开发语境中，bundle是指一个内部结构按照标准规则组织的特殊目录。在Mac OS应用程序目录下的某个.app上可右键显示包内容（Contents），其本质上就是可执行二进制文件（MacOS）及其资源（Resources）的打包组合。因此，在Xcode中配置的Bundle Identifier必须和App ID是一致的或匹配的。

App ID字符串通常以反域名（reverse-domain-name）格式的Company Identifier作为前缀。

# Effective Objective-C

**· 除非确有必要，否则不要引入头文件。**一般来说，应在某个类的头文件中使用向前声明来提及别的类，并在实现文件中引入那些类的头文件，这样做可以尽量降低类之间的耦合。

**向前声明：**

有一个课程类Class和学生类Student，两个类之间需要相互引用。（student.h中倒入class.h，class.h中导入student.h）

问题是，OC中类的相互引用的问题，如果相互导入，编译是不通过的。

解决方法（向前声明）：

使用@class Student，不会将Student.h文件拷贝过来，只是告诉编译器Student这个类在别的地方中有定义，这样就不知道这个类中的任何信息了。

**·用定义常量的方式定义常量，少用#define预处理指令**。

**·枚举**，enum。枚举是一种常量命名方式，某个对象所经历的各种状态就可以定义为一个简单的枚举集。

**属性**：用于封装数据。

****

**·属性特质，属性可以拥有的特质分为四类**

**原子性（nonatomic）**：由编译器所合成的方法会通过锁机制确保其原子性。如果属性具备nonatomic特质，则不适用同步锁。

**读/写权限：**具备readwrite特质的属性拥有获取方法（getter）与设置方法（setter）；具备readonly特质的属性仅拥有获取方法。

**内存管理语义：**

assign、strong、weak、unsafe_unretained、copy



## RunTime和RunLoop

Objective-C是基于C语言加入了面向对象特性和消息转发机制的动态语言，这意味着它不仅需要一个编译器，还需要Runtime系统来动态创建类和对象，进行消息发送和转发。

Objective-C 语法 [receiver message]

但是，实际上使用该语法并不会马上执行receiver对象的message方法的代码，而是向receiver发送一条message消息，这条消息可能由receiver来处理，也可能由转发给其他对象来处理，也有可能假装没有接收到这条消息而没有处理。

具体是如何发送消息的：**首先根据receiver对象的isa指针获取它对应的class，优先在class的cache查找message方法，如果找不到，再到methodLists查找。如果没有在class找到，再到super_class查找。一旦找到message这个方法，就执行它实现的功能。

如果向一个对象发送它无法处理的消息，会出现什么情况？

消息是通过objc_msgSend(id, SEL,...)来实现的。首先会在对象的类对象的cache，method list以及父类对象的cache，method list依次查找SEL对应的IMP。

如果没有找到，并且实现了动态方法决议机制就会决议。如果实现动态决议机制或者决议失败且实现了消息转发机制，就会进入消息转发流程。否则程序crash。

也就是说如果同时实现了动态决议和消息转发，那么动态决议先于消息转发。只有当动态决议无法决议selector的实现，才会尝试进行消息转发。

小结：

1、方法先经过缓存查找，方法列表查找，后进入动态方法解析阶段

2、实例方法解析需要实现 resolveInstanceMethod方法

3、类方法解析需要实现resoleClassMethod方法

4、类方法存储在元类之中，由于元类继承自根元类，根元类最终继承自NSObject，因此对类方法解析的时候，最终回查找到NSObject。由于元类和根元类由系统创建，无法修改，所以可以在根元类的父类NSObject中，添加对应的实例方法resolveInstanceMethod进行动态解析。

[RunTime和RunLoop](https://juejin.im/post/6844903806203854862#heading-0)

RunLoop基本作用：保持程序的持续运行。处理App中的各类事件（触摸事件、定时事件、Selector事件），节省CPU资源，提高程序性能：没有事件时就进行睡眠状态。

一个线程对应一个RunLoop（采用字典存储，线程号为key，RunLoop为value）。RunLoop 是事件接受的分发机制的实现；提供一种异步执行代码的机制，不能并行执行任务；在主队列中，main RunLoop直接配合任务的执行，负责处理UI事件，定时器以及其他内核相关的事件。

[同步执行和异步执行](https://blog.csdn.net/friendan/article/details/12844899)

iOS应用启动时会开始一个运行循环（RunLoop），运行循环的工作是监听事件，例如触摸。当事件发生时，运行循环会为相应的事件找的合适的处理方法。这些处理方法又会调用更多的其他方法，以此类推。只有当这些方法都执行完毕时，控制权才会再次回到运行循环。iOS做了两方面优化来保证用户界面的流畅性：不重绘显示的内容没有改变的视图；在每次事件处理周期中只发送一次drawRect：消息。

Runtime可以访问并修改私有属性。KVC只能获取私有属性。

KVC(key-value coding)键值编码，就是指iOS的开发中，可以允许开发者通过key名直接访问对象的属性，或者给对象的属性赋值。而不需要调用明确的存取方法。这样就可以在运行时动态地访问和修改对象的属性。而不是在编译时确定。

# iOS签名机制

假设，我们有一个APP需要发布，为了防止中途篡改APP内容，保证APP的完整性，以及APP是由指定的私钥的。首先，先将APP内容通过摘要算法，得倒摘要，再用私钥对摘要进行加密得到密文，将源文本、密文、和私钥对应的公钥一并发布即可。

那么如何验证呢？
 验证方首先查看公钥是否是私钥方的，然后用公钥对密文进行解密得到摘要，将APP用同样的摘要算法得到摘要，两个摘要进行比对，如果相等那么一切正常。这个过程只要有一步出问题就视为无效。



作者：没阳光的午后
链接：https://www.jianshu.com/p/c22886db98ec
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

# iOS重用对象

iOS设备内存有限，如果某个对象要显示大量的记录，并且要针对每条记录创建相应的UITableViewCell对象，就会很快耗尽iOS设备的内存资源。 为了解决这一问题，需要重用对象。当用户滚动时，部分对象会移出窗口，将移出窗口的对象放入对象池，等待重用。当对象要求数据源返回某个对象时，数据源可以先查看对象池。如果有未使用的UITableViewCell对象，就可以用新的数据配置这个UITableViewCell对象，然后将其返回给UITableView对象，从而避免重新创建新对象。

从iOS6开始，添加了缓存池的优化方法。1、先去缓存池中找，是否有可重用的cell；2、如果缓存池中没有，是否有可以重用的cell；3、设置数据。

注册cell的三种方法：1、用XIB的方式注册一个cell，并设置重用标示。如果tableView需要一个cell，会加载制定的xib来创建需要的cell；2、通过制定一个类来注册cell，并设置重用标示。如果tableView需要一个cell，会根据指定的类来自动创建；3、通过storyboard来注册cell，并设置重用标示。