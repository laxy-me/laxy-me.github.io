---
layout: post
title: "Android Q变更"
author: "talkeryang"
meta: "Springfield"
---

##只要在Android Q上运行就会受影响的
### 非SDK接口限制
Android 9（API 28）开始开始限制非SDK接口的使用。  
>Android Q 包含更新后的受限非 SDK 接口列表。  
>如果TargetApi未设置到Android Q，暂时不会受到影响。  
>虽然暂时可以使用灰名单中的一些非SDK接口，会存在无法运行的风险。

## WLAN广播
在Android Q中与 Wi-Fi Direct相关的以下广播不在是粘性的  
```
WIFI_P2P_CONNECTION_CHANGED_ACTION
```
```
WIFI_P2P_THIS_DEVICE_CHANGED_ACTION
```
