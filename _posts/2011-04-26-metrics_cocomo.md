---
id: 552
title: 软件度量-CoCoMo模型
date: 2011-04-26T05:50:56+00:00
author: tanglei
layout: post
guid: http://www.tanglei.name/?p=552
permalink: /metrics_cocomo/
duoshuo_thread_id:
  - 1351844048792453341
categories:
  - 软件度量及其应用
tags:
  - CoCoMo模型
  - 软件度量
---
**概念**

COCoMo是指Constructive Cost Model，构造性成本模型，Boehm于1981年提出，用于对软件开发项目的规模、成本、进度等方面进行估算

CoCoMo模型是一个综合经验模型，模型中的参数取值来至于经验值，并且综合了诸多的因素、比较全面的估算模型

比较实用、可操作，在欧盟国家应用较为广泛

**CoCoMo模型的层次** － 支持不同的阶段

**基本COCoMo模型**

系统开发的初期，估算整个系统的工作量(包括维护)和软件开发和维护所需的时间

**中间COCoMo模型**

估算各个子系统的工作量和开发时间

**详细COCoMo模型**

估算独立的软构件，如各个子系统的各个模块的工作量和开发时间.(详细COCOMO模型：将软件系统模型分为系统、子系统和模块三个层次)

根据不同应用软件的不同应用领域,COCOMO模型划分为如下3种软件应用开发模式:

**组织模式(Organic Mode)**.这种应用开发模式的主要特点是在一个熟悉稳定的环境种进行项目开发,盖项目与最近开发的<a>其他</a>项目有很多相似点,项目相对较小,而且并不需要许多创新.

**嵌入式应用开发模式 (Embedded Mode)**.在这种应用开发模式种,项目受到接口要求的限制.接口对整个应用的开发要求非常搞,而且要求项目有很大的创新,例如开发一种全新的游戏.

**中间应用开发模式(也叫半独立型) (Semidetached Mode)**.这时介于组织模式和嵌入式应用开发模式之间的类型.

**基本CoCoMo模型**

E = a (kLOC)^b ;E是工作量(人月) ，a和b是经验常数

D = c E^d ;D是开发时间(月) ，c和d是经验常数

其中，a,b,c,d为经验常数，其取值见下表

[<img class="size-medium wp-image-553 alignleft" title="cocomo1" src="http://www.tanglei.name/wp-content/uploads/2011/04/cocomo1-300x80.png" alt="CoCoMo1" width="300" height="80" />](http://www.tanglei.name/wp-content/uploads/2011/04/cocomo1.png)

**中间CoCoMo模型**

E = a (kLOC)^b *EAF

其中，E表示工作量(人月)，EAF表示工作量调节因子，a,b为经验常数，其取值见下表

[<img class="alignleft size-full wp-image-554" title="cocomo2" src="http://www.tanglei.name/wp-content/uploads/2011/04/cocomo2.png" alt="CoCoMo" width="155" height="92" />](http://www.tanglei.name/wp-content/uploads/2011/04/cocomo2.png)

**EAF的取值**(考虑15个因素)

软件产品属性(3)：软件可靠性，软件复杂性，数据库的规模

计算机属性(4)：程序执行时间，程序占用内存大小，软件开发环境的变化，软件开发环境的响应速度

人员属性(5)：分析员能力，程序员能力，领域经验，开发环境的经验，程序设计语言的经验

项目属性(3)：软件开发方法的能力，软件工具的数量和质量，软件开发的进度要求

**EAF的取值(范围)**

很低、低、正常、高、很高、极高，正常情况下 Fi=1

Boehm建议取值范围[0.70-1.66]

EAF的计算＝ΠFi  ( i=1..15)

调节因子及其取值由统计结果和经验决定，不同的软件开发组织在不同的时期可能会有不同的取值

使用中间CoCoMo模型可以估算开发软件产品的工作量，比较各种开发方案的工作量。

案例分析：用基本CoCoMo模型估算项目的工作量、开发时间和参加项目开发的人数

CAD软件：目标代码行33.2kLOC，属于中等规模，半独立型，因而a = 3.0, b = 1.12, c = 2.5, d = 0.35

E = 3.0*(33.2)^1.12 =152 PM

D = 2.5*(152)^0.35 = 14.5 (月)

参加项目人数N = E/D = 152/14.5 = 11(人)