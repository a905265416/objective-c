## @try @catch @finally 使用

OC 中很少像其他语言频繁使用异常处理，但是还是可以用的。

### 为什么少用？

1. try catch 无法捕获 UncaughtException， 而 OC 中大部分 crash 如内存溢出、野指针等都是无法捕获的，而能捕获的只有数组越界之类，try catch 对于 OC 来说比较鸡肋。
2. Apple 更提倡开发者使用 NSError 来处理程序运行中可恢复的错误
3. 多人编程中，错误的使用了 try-catch，把逻辑写在 catch 中
4. 综上所述，OC 代码中使用的很少，可以通过判断是否非空、判断数组是否越界等方法进行处理。

## @catch

catch 是在有 crash 的时候才会执行

## @finally

finally 是一定会执行的



## 什么时候会保护

这种情况会直接触发

```objective-c
NSArray *arr = @[@1,@2];
@try {
    [arr objectAtIndex:3]
} @catch (NSException *exp) {
    NSLog(@"crash!!!");
} @finally {
    NSLog(@"safe");
}
```

如果多包一层方法，还是会触发

```objc
@try {
  [self testFun];
} @catch (NSException *exp) {
  NSLog(@"crash!!!");
} @finally {
  NSLog(@"safe");
}

- (void)testFun {
    NSArray *arr = @[@1,@2];
    if ([arr objectAtIndex:3]) {
        return;
    }
}
```

