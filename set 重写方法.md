## 为什么需要重写 set 方法？

因为有时候要在 set 的时候做额外操作

比如在 set 的时候将字符串内的空格去掉

![](https://tva1.sinaimg.cn/large/008i3skNgy1gts5dl2imrj61ci0eqtbv02.jpg)

## 为什么这里的 _xxx 而不是 self.xxx？

因为 self.xxx 是对属性的访问，本质是调用属性的 setter 方法，引用计数 +1

_xxx 这是对成员变量的访问，是对指针的赋值，引用计数器没有变化。

## 这里为什么是 copy 方法 不能直接赋值

因为在下面要对 _reactNativeBundleName 做修改

