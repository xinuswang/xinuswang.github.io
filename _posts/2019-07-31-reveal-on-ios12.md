---
title: Reveal在iOS12中的使用
date: '2019-07-31 17:51:00'
key: 2019-07-31-17-51-00
tags:
- Reveal
- Jailbreak
categories:
- iOS
---

### 概述
本文主要记录了在iOS12越狱设备上，如何安装**Reveal v.21**插件分析设备上安装的App。

前置条件：
1. iOS12已越狱设备；
2. Reveal ver.21。

其他型号或系统版本上可能存在差别，需酌情处理。

### 步骤
网上记录的Reveal的安装使用步骤，含一些插件的安装，文件的替换等操作，在前面记录的前提下，已经失效。我反复尝试了多次，目前记录正确的步骤如下：
1. 越狱可以通过**unc0ver**工具，末尾提供参考连接;
2. 安装reveal2loader插件；Cydia中的是1.0.1版本，使用中会提示版本太旧，所以需要手工安装1.0.3版本；
3. 通过终端的ssh连接手机，通过scp拷贝reveal2loader到手机上，然后通过`dpkg -i Reveal2Loader_1.0-3_iphoneos-arm.deb`进行手工安装，网上其他记录拷贝替换`reveal2Loader.dylib`等步骤不再需要；
4. 安装完毕后，在手机的系统设置中，找到Reveal，进入后在`Enable Applications`下打开需要分析的App；
5. 在电脑上打开Reveal，保证手机与电脑同一个局域网或者用usb连接，即可正常使用。

### 参考工具
1. 越狱工具：[**unc0ver**](https://github.com/pwn20wndstuff/Undecimus)；
2. reveal2loader插件：[v1.0.3](/assets/dl/Reveal2Loader_1.0-3_iphoneos-arm.deb)；
3. 可选的Shell工具：[FinalShell](http://www.hostbuf.com/), 提供类似MobaXterm功能的ssh客户端，可以方便的访问路径和拷贝文件；
4. 越狱参考：[网页链接](https://www.abcydia.com/read-16031.html)；
5. 插件参考：[网页链接](https://www.52pojie.cn/forum.php?mod=viewthread&tid=951380&page=1)。