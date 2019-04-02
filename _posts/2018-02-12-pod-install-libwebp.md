---
title: pod 'libwebp' 网络错误的解决办法
date: '2018-02-12 15:32:00'
key: 2018-02-12-15-32-00
tags:
- libwebp
- pod
- cocoapods
categories:
- iOS
---

### 关于WebP图片
WebP是Google开发的一种图片格式，它的体积比JPEG还小，比较省流量，对图片较多的页面，可以大大加快页面的加载速度。

iOS一些常用库提供了WebP的支持，比如**SDWebImage**库：

    pod 'SDWebImage/WebP'

### Pod install报错
**libwebp**的源码在**https://chromium.googlesource.com/webm/libwebp**，国内的环境无法直接访问到Google的服务器，所以直接`pod install`时会报错，无法拉取**libwebp**。

### 替换libwebp的源
Cocoapods安装时，会从中央仓库clone一份到本机，当执行pod相关命令时，会从本机的仓库中，通过名称和版本查找到**.podspec.json**，再读取json文件中的信息，从依赖库的源码地址拉取代码。我们可以使用`pod repo update`来更新本机的仓库。

使用`pod repo`可以查看本地仓库的存放路径，如果未添加其他仓库，则默认只会存在1个官方的仓库：
```sh
master
- Type: git (master)
- URL:  https://github.com/CocoaPods/Specs.git
- Path: /Users/xinus/.cocoapods/repos/master

1 repo
````

如上**- Path:**所表示的路径，即Pod存放在本地的仓库位置，通过**Finder**进入该目录，搜索**libweb**可以很容易的查找到它的位置。例如，我本机上的路径`/Users/xinus/.cocoapods/repos/master/Specs/1/9/2/libwebp`，这个目录下面是不同版本号的子目录：

![image](/assets/images/libwebp-pod-dir.jpg)

根据`pod install`时报错信息的版本号，进入对应的目录，假设是**1.0.0**版本，并打开目录下的**libwebp.podspec.json**文件：

```json
{
  "name": "libwebp",
  "version": "1.0.0",
  "summary": "Library to encode and decode images in WebP format.",
  "homepage": "https://developers.google.com/speed/webp/",
  "authors": "Google Inc.",
  "license": {
    "type": "BSD",
    "file": "COPYING"
  },
  "source": {
    "git": "https://chromium.googlesource.com/webm/libwebp",
    "tag": "v1.0.0"
  },
  ....
}
```

将`source - git`替换为`https://github.com/webmproject/libwebp.git`：

```json
{
  "name": "libwebp",
  "version": "1.0.0",
  "summary": "Library to encode and decode images in WebP format.",
  "homepage": "https://developers.google.com/speed/webp/",
  "authors": "Google Inc.",
  "license": {
    "type": "BSD",
    "file": "COPYING"
  },
  "source": {
    "git": "https://github.com/webmproject/libwebp.git",
    "tag": "v1.0.0"
  },
  ....
}
```

然后保存该文件，回到工程目录，重新执行`pod install`即可。

### 后记
本地仓库更新后，上述的修改会被重置，需再次按上面的方法替换libwebp的源。