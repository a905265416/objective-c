```objective-c
- (void)setObject:(ObjectType)anObject forKey:(KeyType <NSCopying>)aKey;
```



NSMutabbleDictionary 专有方法，为什么不用 setValue

因为 setValue 是 NSObject 的方法，setObject 是专门针对 Dictionary 设计的方法

