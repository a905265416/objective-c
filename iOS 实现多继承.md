# 什么是多继承

假设 C 类要同时继承 A 类和 B 类，则为多继承。而 Objc 不支持多继承，由于消息机制名字查找发生在运行时而非编译时，很难解决多个基类可能导致的二义性问题（两个类有同名属性or方法）。

# 间接实现多继承

## 消息转发

当想一个对象发送消息时，但 runtime system 在当前类和父类中都找不到对应的实现时，runtime system 并不会立即报错使程序崩溃，而是依次执行下列步骤：

![img](http://cdn.cocimg.com/cms/uploads/allimg/130528/4196_130528172246_1.png)

1. 动态方法解析：向该类发送 resolveInstanceMethod 信号，检查是否动态向该类添加了方法。

2. 快速消息转发：检查该类是否实现了，若返回值非 nil 或非 self ，则 向该返回对象重新发送消息。
3. 标准消息转发：runtime发送methodSignatureForSelector:消息获取Selector对应的方法签名。返回值非空则通 forwardInvocation:转发消息，返回值为空则向当前对象发送doesNotRecognizeSelector:消息，程序崩溃退出。

因此，可以通过2、3来实现消息转发。

### 快速消息转发

有两个类：Teacher 和 Doctor，Doctor 可以做手术（operate 方法）

```objective-c
@interface Teacher : NSObject      
@end   
```

```objc
@interface Doctor : NSObject      
- (void)operate;   
@end   
```

通过消息转发，可以让 Teacher 调用 Doctor 的方法

```objc
- (id)forwardingTargetForSelector:(SEL)aSelector   
{       
  Doctor *doctor = [[Doctor alloc]init];       
	if ([doctor respondsToSelector:aSelector]) 
	{           
  	return doctor;       
	}       
 	return nil;   
}   
```

消息可以动态转发，但是编辑器的静态检查绕不过，Teacher 没有实现 operate，又该如何声明？

**方法一：类别category**

```objc
@interface Teacher (DoctorMethod)   
- (void)operate;      
@end   
```

**方法二：导入头文件，调用时强转类型**

Teacher 类中引入 Doctor 头文件，并在调用时强转类型

```objective-c
Teacher *teacher = [[Teacher alloc]init];  
[(Doctor *)teacher operate];   # 这里强转成 id 类型也可以，会有什么隐患？ 如果引入了其他头文件也有这个方法会出问题
```

```objc
//   //  Teacher+Profession.m   //        
#import "Teacher+Profession.h"   

const char *ProfessionType = "NSString *";   
@implementation Teacher (Profession)      
-(void)setProf:(NSString*)prof   
{       
	objc_setAssociatedObject(self, ProfessionType, prof, OBJC_ASSOCIATION_RETAIN_NONATOMIC);   
}      
-(NSString *)prof   
{       
	NSString *pro = objc_getAssociatedObject(self, ProfessionType);
	return pro;   
}      
@end   
```

分类中添加属性

