---
title: WeiboSDK授权登录的问题
date: 2016-04-13 14:51:32
tags:
- weibo
- authorization
categories:
- ios
---

## WeiboSDK授权登录的问题
最近的一个项目里面，集成了WeiboSDK，主要是要用到OAuth授权登录。这个问题发现得比较早，但是一直没有出来。目前手上其他优先级高的任务都完成了，这个Bug自然需要解掉。

先说说Bug的现象。App集成了Weibo的SDK，版本3.1.1，按照[文档所列的要求](https://github.com/sinaweibosdk/weibo_ios_sdk)，完成的所有关联的配置，包括对iOS9的支持。
<!-- more -->

1. iPhone上安装最新的Weibo客户端，并登录一个账号；
2. 在我们的App中（简称App）进入登录页面，点Weibo的图标，Weibo客户端会被调用至前台，出现授权页面；
3. 若该账号第一次授权，则一切正常；会正确的出现App的图标和相应的描述；点击确认按钮，完成授权并切回App；
4. 若账号以前授权过，授权页面会正常显示，但不需要用户点击确认按钮，自动授权完成，并切回App。
<!-- more -->
这个问题比较严重，因为：

- 不再给用户决定的权利，跳过确认直接授权登录；
- 如果Weibo客户端上有多个账户，无法让用户切换账号。

## 暂时无解
基本认定了是Weibo自己某种缓存机制作怪，翻了几遍文档和SDK的API，没有找到任何可以去取消这种直接授权的参数。尝试给SDK Team写邮件，被拒收了。对外公布的邮箱，竟然不接收外部邮件。好在加入了他们的QQ讨论群，得到的答复也基本如此：
> 这个是微博的机制，就是这样的，微博内有授权缓存，判断一段时间内授权过得应用，默认不需要手动操作。说服QA的话，用其他线上app演示一下不就行了？文档不好找，这机制蛮久了。

虽然不太喜欢“其他App都是如此，所以如此也没有什么问题”的意思。但目前看来无解，这个问题暂时标记为As Designed，结束。