# iOS 实现 Toast

iOS 没有 Toast 功能，利用定时器实现，自定义 view 然后自动触发，之后消失

![](https://tva1.sinaimg.cn/large/008i3skNgy1gtt7ntltbpj60xe0csq5902.jpg)

```objective-c
+ (void)showToast:(NSString *)string
{
    CGRect initRect = CGRectMake(([[UIScreen mainScreen]bounds].size.width - 320)/2, ([[UIScreen mainScreen]bounds].size.height - 80)/2, 320, 80);
    UILabel *label = [[UILabel alloc] initWithFrame:initRect];
    label.tag = 10000;
    if ([[UIApplication sharedApplication].keyWindow viewWithTag:label.tag]) {
        return;
    }
    label.text = string;
    label.textAlignment = NSTextAlignmentCenter;
    label.textColor = [UIColor whiteColor];
    label.font = [UIFont systemFontOfSize:17];
    label.backgroundColor = [UIColor colorWithRed:0 green:0 blue:0 alpha:0.6];
    label.numberOfLines = 0;
    label.lineBreakMode = UILineBreakModeWordWrap;
    [[UIApplication sharedApplication].keyWindow addSubview:label];
    [NSTimer scheduledTimerWithTimeInterval:3.0 target:self selector:@selector(removeToastWithView:) userInfo:label repeats:NO];
}
 
+ (void)removeToastWithView:(NSTimer *)timer
{
    UILabel *label = [timer userInfo];
    [label removeFromSuperview];
}
```

1. userInfo：实现参数传递

2. repeats：`If YES, the timer will repeatedly reschedule itself until invalidated. If NO, the timer will be invalidated after it fires.` 为防止循环引用，设置成 NO

