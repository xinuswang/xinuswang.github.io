---
title: iOS的WebView中通过HTML调用系统摄像头拍照和录像
date: '2019-07-25 17:45:00'
key: 2019-07-25-17-45-00
tags:
- Camera
- Capture
- WebView
categories:
- iOS
---

### 相关的HTML代码
```html
<div>
    <p style="margin-left: 8px">拍照</p>
    <input type="file" accept="image/*" capture="camera"/>
</div>
<div>
    <p style="margin-left: 8px">视频</p>
    <input type="file" accept="video/*" capture="true">
</div>
```

### 问题记录
1. 需要在App的info.plist中配置相机以及麦克风的权限；
2. 如果授权被拒绝，唤起的相机无法正常拍照或者录像；