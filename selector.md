# setStatusBarStyle

```
if ([vc respondsToSelector:NSSelectorFromString(@"updateStatusBarStyle:")]) {
        UIStatusBarStyle style = [query[@"style"] integerValue] > 0 ? UIStatusBarStyleLightContent : UIStatusBarStyleDefault;
#pragma clang diagnostic push
#pragma clang diagnostic ignored "-Warc-performSelector-leaks"
        [vc performSelector:NSSelectorFromString(@"updateStatusBarStyle:") withObject:@(style)];
#pragma clang diagnostic pop
    } else {
        
    }
```

1. 首先判断 vc 是否有 updateStatusBarStyle 这个方法
2. 有的话执行 [vc performSelector:NSSelectorFromString(@"updateStatusBarStyle:") withObject:@(style)];

3. else 执行 NSAssert

   `NSAssert(condition, desc)` 当 condition 为 NO 时，终止并抛出异常
