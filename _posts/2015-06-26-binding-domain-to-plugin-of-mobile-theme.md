---
id: 2669
title: 给手机主题插件Wptouch绑定单独的域名
date: 2015-06-26T20:39:09+00:00
author: tanglei
layout: post
guid: http://www.tanglei.name/?p=2669
permalink: /binding-domain-to-plugin-of-mobile-theme/
duoshuo_thread_id:
  - 1351844048792453519
categories:
  - wordpress
  - 我做站长
  - 经验技巧
tags:
  - plugin
  - wordpress
  - wptouch
  - 经验技巧
---
目标是使得在wordpress站点中，绑定域名<m.tanglei.name>{.uri},通过此域名访问wordpress站点时都以wptouch主题访问。

最终解决方案：

手动设置UA，让wptouch后台添加设置的UA能够match后切换。相关联系太多，不能直接设置`is_mobile_device`为`true`或者直接`$this->is_supported_device()`返回`true`。

vim core/class-wptouch-pro.php 中的is\_supported\_device()方法中：

<pre class="sourceCode php"><code class="sourceCode php">&lt;span class="kw">$domain&lt;/span> = &lt;span class="kw">$_SERVER&lt;/span>&lt;span class="ot">[&lt;/span>&lt;span class="st">&#39;HTTP_HOST&#39;&lt;/span>&lt;span class="ot">];&lt;/span>
&lt;span class="kw">if&lt;/span> &lt;span class="ot">(&lt;/span>&lt;span class="kw">$domain&lt;/span> == &lt;span class="st">&#39;m.tanglei.name&#39;&lt;/span>&lt;span class="ot">)&lt;/span>
     &lt;span class="kw">$_SERVER&lt;/span>&lt;span class="ot">[&lt;/span>&lt;span class="st">&#39;HTTP_USER_AGENT&#39;&lt;/span>&lt;span class="ot">]&lt;/span>=&lt;span class="st">&#39;tanglei&#39;&lt;/span>&lt;span class="ot">;&lt;/span> &lt;span class="co">//跟wptouch admin后台设置的一样即可&lt;/span></code></pre>

首页解决了～ 还得改首页上的链接～ 这些链接都是www打头的～ vim wp-config.php 添加如下设置，成功后 WP后台设置-常规中wordpress地址和站点地址不可编辑。 //&#8220;\`{.php .numberLines} Attention 这个jekyll不支持

<table class="sourceCode php numberLines">
  <tr class="sourceCode">
    <td class="lineNumbers">
      <pre>1
2
3
4
5
6
</pre>
    </td>
    
    <td class="sourceCode">
      <pre><code class="sourceCode php">&lt;span class="co">//multiple domain set tanglei begin&lt;/span>
&lt;span class="kw">$tangleihome&lt;/span> = &lt;span class="st">&#39;http://&#39;&lt;/span>.&lt;span class="kw">$_SERVER&lt;/span>&lt;span class="ot">[&lt;/span>&lt;span class="st">&#39;HTTP_HOST&#39;&lt;/span>&lt;span class="ot">];&lt;/span>
&lt;span class="kw">$tangleisiteurl&lt;/span> = &lt;span class="kw">$tangleihome&lt;/span>&lt;span class="ot">;&lt;/span>
&lt;span class="fu">define&lt;/span>&lt;span class="ot">(&lt;/span>&lt;span class="st">&#39;WP_HOME&#39;&lt;/span>&lt;span class="ot">,&lt;/span> &lt;span class="kw">$tangleihome&lt;/span>&lt;span class="ot">);&lt;/span>
&lt;span class="fu">define&lt;/span>&lt;span class="ot">(&lt;/span>&lt;span class="st">&#39;WP_SITEURL&#39;&lt;/span>&lt;span class="ot">,&lt;/span> &lt;span class="kw">$tangleisiteurl&lt;/span>&lt;span class="ot">);&lt;/span>
&lt;span class="co">//multiple domain set tanglei end&lt;/span></code></pre>
    </td>
  </tr>
</table>

对SEO不太好～管他呢～

效果如下

<div class="figure">
  <img src="https://raw.githubusercontent.com/tl3shi/markdown2wordpress/master/posts//binding-domain-to-plugin-of-mobile-theme/m.tanglei.name.preview.png" /></p>
</div>