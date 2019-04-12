---
layout: post
title: "CHANGE_NETWORK_STATE权限问题"
author: "talkeryang"
meta: "Springfield"  
---

在查看崩溃日志中发现了较多的SecurityException报错，报错信息如下：
```
java.lang.SecurityException: com.xxx.xxx was not granted  either of these permissions: android.permission.CHANGE_NETWORK_STATE, android.permission.WRITE_SETTINGS.
	at android.os.Parcel.readException(Parcel.java:1602)
	at android.os.Parcel.readException(Parcel.java:1555)
	at android.net.IConnectivityManager$Stub$Proxy.requestNetwork(IConnectivityManager.java:2064)
	at android.net.ConnectivityManager.sendRequestForNetwork(ConnectivityManager.java:2470)
	at android.net.ConnectivityManager.requestNetwork(ConnectivityManager.java:2509)
	at com.superrtc.call.NetworkMonitorAutoDetect$ConnectivityManagerDelegate.requestMobileNetwork(NetworkMonitorAutoDetect.java)
	at com.superrtc.call.NetworkMonitorAutoDetect.<init>(NetworkMonitorAutoDetect.java)
	at com.superrtc.mediamanager.XReachability.setAutoDetectConnectivityStateInternal(XReachability.java)
	at com.superrtc.mediamanager.XReachability.startMonitoring(XReachability.java)
	at com.superrtc.mediamanager.EMediaManager$7.run(EMediaManager.java)
	at android.os.Handler.handleCallback(Handler.java:743)
	at android.os.Handler.dispatchMessage(Handler.java:95)
	at android.os.Looper.loop(Looper.java:150)
	at com.superrtc.util.LooperExecutor.run(LooperExecutor.java)
```
按理说android.permission.CHANGE_NETWORK_STATE这一个权限，是普通权限，只在Manifest中声明就可以获取。
出现这个问题很不科学啊，再仔细去看看错误日志，发现报错只发生在6.0这个版本和部分6.0.1版本中。

那问题应该是出在6.0 版本中，之后去查资料后发现，在6.0版本中这个权限默认是被拒绝，无法获取这个权限。所以，在需要个权限的时候会出现权限问题导致应用因为权限问题崩溃。这个在stackoverflow中有人讨论过了，[去看看](https://stackoverflow.com/questions/32185628/connectivitymanager-requestnetwork-in-android-6-0)

知道问题的原因之后的解决方案就简单了，既然CHANGE_NETWORK_STATE权限获取不到，那只好想办法打开WRITE_SETTINGS这个权限了。

跳转到应用程序设置页打开WRITE_SETTINGS这个权限：
```
Intent goToSettings = new Intent(Settings.ACTION_MANAGE_WRITE_SETTINGS);
goToSettings.setData(Uri.parse("package:" + getPackageName()));
startActivity(goToSettings);
```