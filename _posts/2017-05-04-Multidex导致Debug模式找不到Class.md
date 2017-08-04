---

layout: post
title: "Background sticky concurrent mark sweep GC freed"
author: "talkeryang"
meta: "Springfield"

---

## 问题

Debug模式安装应用到4.4上使用，apk无法启动报错。

## 问题分析
 ```java
	if (DEBUG) {
		MultiDex.install(this);
	}
 ```

## 原因

Android 5.0和更高版本使用名为ART的运行时，它原生支持从APK文件加载多个DEX文件。