iOS 目录结构

* ./Applications：存放所有的系统 app 和来自 cydia 的 app 不包括 storeApp
* ./developer: 设备连接xcode后被指定调试用机, 生成改目录, 包含一些调试需要的工具和数据. 子目录: ../Applications, ../Library, ../Tools, ../usr.
* ./Library：存放一些提供系统支持的数据
* ./System/Library：iOS 文件系统中最重要的目录之一，存放大量系统组件
* ./System/Library/Frameworks 和 /System/Library/PrivateFrameworks：存放 iOS 各种 framework
* ./User：实际指向 /var/mobile
* ./var/mobile/Containers：存放 storeApp

