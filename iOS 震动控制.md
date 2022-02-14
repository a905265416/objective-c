# 背景

RN 业务需要有控制震动，希望给业务方提供一个能够自定义震动强度，震动时间的方法。

## 方法一、UIFeedbackGenerator

该方法有三个具体的子类：

UIImpactFeedbackGenerator
UINotificationFeedbackGenerator
UISelectionFeedbackGenerator

其中 UIImpactFeedbackGenerator 比较符合业务场景，需要在 iOS 10 以上系统使用，iPhone 7及以上设备

![](https://tva1.sinaimg.cn/large/008i3skNgy1gv91dl6lg8j61ta0ky42x02.jpg)

### 使用方法

```objective-c
if(@available(iOS 10.0, *)) {
            UIImpactFeedbackGenerator *impactFeedBack = [[UIImpactFeedbackGenerator alloc] initWithStyle:UIImpactFeedbackStyleHeavy];
            [impactFeedBack prepare];
            [impactFeedBack impactOccurred];
        }
```

**只能控制强度，不同强度的震动时长一样**

## AudioServicesPlaySystemSoundWithVibration

私有方法不行，只能用公有 API `AudioServicesPlayAlertSound(kSystemSoundID_Vibrate)`

使用方法 

```objective-c
AudioServicesPlayAlertSound(kSystemSoundID_Vibrate);
```

![](https://tva1.sinaimg.cn/large/008i3skNgy1gv91wmpgj6j60q10djt9t02.jpg)