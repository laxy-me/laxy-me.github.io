---
layout: post
title: "Windows Defender引起的Studio报错"
author: "talkeryang"
meta: "Springfield"
---

今天运行studio的时候一直报如下的错误:
```
* What went wrong:
 Failed to capture snapshot of output files for task 'transformClassesWithDexBuilderForDebug' property 'streamOutputFolder' during up-to-date check.
> Failed to create MD5 hash for file 'D:\workspace\xxx\app\build\intermediates\transforms\dexBuilder\debug\445\com\aliyun\struct\asset\AssetInfo.dex'.
```

然后呢我就进行了常规的操作方法：
1、删除build文件夹或者clean projecth或者invalidate and restart 
2、重新编译
然而一直没有效果。

之后我还将gradle版本换回老版本尝试过，并没什么用。

偶然间我发现windows一直屁颠屁颠的给我报威胁。
![windows defender报错.png](http://upload-images.jianshu.io/upload_images/2784842-70b2730ffb17cea0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这时候我就想是不是这个操作被windows个阻止了啊。
然后器看日志，果然是这样。
![报错详情.png](http://upload-images.jianshu.io/upload_images/2784842-919203f512937616.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

发现问题之后就好解决了；
![添加排除项.png](http://upload-images.jianshu.io/upload_images/2784842-e4c6670d538c368e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
之后把工程对的文件夹和studio的进程添加到排除项就好了。





