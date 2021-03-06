---
id: 1221
title: HTTP状态码304原理
date: 2011-11-02T22:27:23+00:00
author: tanglei
layout: post
guid: http://www.tanglei.name/?p=1221
permalink: /intern-in-tencent-http-304/
duoshuo_thread_id:
  - 1351844048792453337
categories:
  - SoftwareEngineering
  - 实习那些事儿
tags:
  - HTTP状态码304原理
  - If-Modified-Since
  - If-None-Match
  - Last-Modified
---
昨天因为收到告警信息，原因是自动化测试用例用例的脚本有问题。其中一个请求过去设置了If-None-Match的值为 700390322，然后response返回304.测试人员肯定是抓包然后有If-None-Match这个字段，就每次发了这个值，但是其实，服务器那边根据这个值判断是否是新请求新的内容，如果服务器端内容没有变的话，直接返回304，让浏览器端直接取缓存就可以了。根据这个扩展了下相关知识。

<p align="left">
  <strong>Last-Modified</strong><strong>/</strong><strong>If-Modified-Since</strong><strong></strong>
</p>

<p align="left">
  Web 服务是不变的：通常服务器知道你所请求的数据的最后修改时间，并且 HTTP 为服务器提供了一种将最近修改数据连同你请求的数据一同发送的方法。
</p>

<p align="left">
  如果你第二次 (或第三次，或第四次) 请求相同的数据，你可以告诉服务器你上一次获得的最后修改日期：在你的请求中发送一个 If-Modified-Since 头信息，它包含了上一次从服务器连同数据所获得的日期。如果数据从那时起没有改变，服务器将返回一个特殊的 HTTP 状态代码 304，这意味着 “从上一次请求后这个数据没有改变”。这一点有何进步呢？当服务器发送状态编码 304 时，<em>不再重新发送数据</em>。您仅仅获得了这个状态代码。所以当数据没有更新时，你不需要一次又一次地下载相同的数据；服务器假定你有本地的缓存数据。
</p>

<p align="left">
  所有现代的浏览器都支持最近修改 (last-modified) 的数据检查。如果你曾经访问过某页，一天后重新访问相同的页时发现它没有变化，并奇怪第二次访问时页面加载得如此之快——这就是原因所在。你的浏览器首次访问时会在本地缓存页面内容，当你第二次访问，浏览器自动发送首次访问时从服务器获得的最近修改日期。服务器简单地返回 304: Not Modified (没有修改)，因此浏览器就会知道从本地缓存加载页面。
</p>

<p align="left">
  <strong> </strong><strong>ETag</strong><strong>/</strong><strong>If-None-Match</strong><strong></strong>
</p>

<p align="left">
  ETag 是实现与最近修改数据检查同样的功能的另一种方法：没有变化时不重新下载数据。其工作方式是：服务器发送你所请求的数据的同时，发送某种数据的 hash (在 ETag 头信息中给出)。hash 的确定完全取决于服务器。当第二次请求相同的数据时，你需要在 If-None-Match: 头信息中包含 ETag hash，如果数据没有改变，服务器将返回 304 状态代码。与最近修改数据检查相同，服务器<em>仅仅</em> 发送304 状态代码；第二次将不为你发送相同的数据。在第二次请求时，通过包含 ETag hash，你告诉服务器：如果 hash 仍旧匹配就没有必要重新发送相同的数据，因为你还有上一次访问过的数据。
</p>