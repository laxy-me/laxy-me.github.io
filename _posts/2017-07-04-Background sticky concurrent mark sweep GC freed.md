---
layout: post
title: "Background sticky concurrent mark sweep GC freed"
author: "talkeryang"
meta: "Springfield"
---

今天测试修改新接口时，发现手机内存抖动。

##logcat日志信息

频繁打印以下日志

>Background partial concurrent mark sweep GC freed 1641307(37MB) AllocSpace objects, 0(0B) LOS object

##问题分析

>多次观察后发现gson解析出错后会出现该问题。因为只修改了接口，未修改实体类，初步判断是gson解析出错引起。

##原因
>
  问题原因，如果在json model里面放了非可序列化的对象就会导致这中问题，可序列化的就是那些基础数据类型和集合类型，如果在里面放个Android的Activity或者adapter这类类型字段，变量声明前面一定要加transient否则就是长期GC提示。
