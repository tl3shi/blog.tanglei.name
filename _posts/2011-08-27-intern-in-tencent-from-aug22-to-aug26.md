---
id: 1138
title: 实习工作日志8-22—8-26
date: 2011-08-27T16:16:48+00:00
author: tanglei
layout: post
guid: http://www.tanglei.name/?p=1138
permalink: /intern-in-tencent-from-aug22-to-aug26/
duoshuo_thread_id:
  - 1351844048792453243
categories:
  - 实习那些事儿
tags:
  - 实习工作日志
  - 腾讯实习
---
这周好像没做什么，主要就是跟测吧。30号上线啊得……

8-22:运维工具等培训、招聘模块模调申请整理添加

8-23:自测、推荐热门问题后台管理。

8-24：跟测

发现问题：加模调时，不细心，返回码copy错误。

备注下：前台通过provinceid[]=11&provinceid[]=22 ,后台直接获取可得array过来的参数

<p align="left">
         leitang(唐磊) 19:15:05
</p>

<p align="left">
  从其他地方点击到宣讲会那页时 默认选中的那条记录当天的所有宣讲会信息。如果1页没有展示完，会提示还有更多。根据还有更多请求了。。。请求时没有加上日期的参数 所以就一直往后了请求 跟 其他 一页展示完了的不一致。【所以啊，以后分页时服务器端主动把参数吐出去。这个是经验这个是经验】
</p>

<p align="left">
  leitang(唐磊) 19:17:50
</p>

<p align="left">
  你是不是没有提交代码。 港澳台分了么， 241上没有分。如果不分的话 就得这样传参provinceid[]=11&provinceid[]=22。 分了就还跟其他的一样。
</p>

<p align="left">
   8-25 ：跟测
</p>

<p align="left">
  8-26：跟测，去掉User对象
</p>