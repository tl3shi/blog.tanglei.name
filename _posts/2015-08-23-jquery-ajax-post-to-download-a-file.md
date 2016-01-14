---
id: 2719
title: jQuery Ajax请求下载文件资源
date: 2015-08-23T15:24:28+00:00
author: tanglei
layout: post
guid: http://www.tanglei.name/?p=2719
permalink: /jquery-ajax-post-to-download-a-file/
duoshuo_thread_id:
  - 1351844048792453525
categories:
  - Scala
  - 工作那些事儿
  - 敲敲代码
tags:
  - jquery
  - scala
  - work
  - 前端
---
最近遇到这样一个问题，后端用Scala结合Play框架，前端jQuery+Bootstrap, 需求是这样的，其实跟[SO](http://stackoverflow.com/questions/3499597/javascript-jquery-to-download-file-via-post-with-json-data)上的这个问题一样， 根据Ajax的Post请求要求server端或者直接返回Json数据或者直接返回可以下载的file文件。搜索了下问题，貌似单独一次ajax请求搞不定。

解决方案大同小异，但都是通过发请求两次；

### server端逻辑不变 {#server端逻辑不变}

server端逻辑不变，client根据server的返回判断再次post可以download的file。server端直接返回的是file，ajax请求的返回的时候再通过一样的form隐藏表单请求一次；[Handle file download from ajax post](http://stackoverflow.com/questions/16086162/handle-file-download-from-ajax-post) Server端：

<div class="sourceCode">
  <pre class="sourceCode java"><code class="sourceCode java">&lt;span class="kw">if&lt;/span> request is json
    &lt;span class="fu">Ok&lt;/span>(json)
&lt;span class="kw">else&lt;/span>
    Ok.&lt;span class="fu">sendFile&lt;/span>(File)</code></pre>
</div>

当是filedownload的请求时，response的header如下：

<div class="sourceCode">
  <pre class="sourceCode python"><code class="sourceCode python">Content&lt;span class="op">-&lt;/span>Disposition:attachment&lt;span class="op">;&lt;/span> filename&lt;span class="op">=&lt;/span>&lt;span class="st">"15_08_23-11_02_57_3227832721122260226064.csv"&lt;/span>
Content&lt;span class="op">-&lt;/span>Length:&lt;span class="dv">4388&lt;/span>
Content&lt;span class="op">-&lt;/span>Type:text&lt;span class="op">/&lt;/span>csv</code></pre>
</div>

client端：

<div class="sourceCode">
  <pre class="sourceCode javascript"><code class="sourceCode javascript">&lt;span class="kw">var&lt;/span> url &lt;span class="op">=&lt;/span> &lt;span class="st">"/tool/query"&lt;/span>&lt;span class="op">;&lt;/span>
&lt;span class="va">$&lt;/span>.&lt;span class="at">ajax&lt;/span>(&lt;span class="op">{&lt;/span>
    &lt;span class="dt">url&lt;/span>&lt;span class="op">:&lt;/span> url&lt;span class="op">,&lt;/span>
    &lt;span class="dt">type&lt;/span>&lt;span class="op">:&lt;/span> &lt;span class="st">"POST"&lt;/span>&lt;span class="op">,&lt;/span>
    &lt;span class="dt">data&lt;/span>&lt;span class="op">:&lt;/span> params&lt;span class="op">,&lt;/span>
    &lt;span class="dt">success&lt;/span>&lt;span class="op">:&lt;/span> &lt;span class="kw">function&lt;/span>(response&lt;span class="op">,&lt;/span> status&lt;span class="op">,&lt;/span> request)&lt;span class="op">{&lt;/span>
      &lt;span class="kw">var&lt;/span> disp &lt;span class="op">=&lt;/span> &lt;span class="va">request&lt;/span>.&lt;span class="at">getResponseHeader&lt;/span>(&lt;span class="st">&#39;Content-Disposition&#39;&lt;/span>)&lt;span class="op">;&lt;/span>
        &lt;span class="cf">if&lt;/span> (disp &lt;span class="op">&&&lt;/span> &lt;span class="va">disp&lt;/span>.&lt;span class="at">search&lt;/span>(&lt;span class="st">&#39;attachment&#39;&lt;/span>) &lt;span class="op">!=&lt;/span> &lt;span class="op">-&lt;/span>&lt;span class="dv">1&lt;/span>) &lt;span class="op">{&lt;/span>
        &lt;span class="kw">var&lt;/span> form &lt;span class="op">=&lt;/span> &lt;span class="at">$&lt;/span>(&lt;span class="st">&#39;&lt;form method="POST" action="&#39;&lt;/span> &lt;span class="op">+&lt;/span> url &lt;span class="op">+&lt;/span> &lt;span class="st">&#39;"&gt;&#39;&lt;/span>)&lt;span class="op">;&lt;/span>
        &lt;span class="va">$&lt;/span>.&lt;span class="at">each&lt;/span>(params&lt;span class="op">,&lt;/span> &lt;span class="kw">function&lt;/span>(k&lt;span class="op">,&lt;/span> v) &lt;span class="op">{&lt;/span>
            &lt;span class="va">form&lt;/span>.&lt;span class="at">append&lt;/span>(&lt;span class="at">$&lt;/span>(&lt;span class="st">&#39;&lt;input type="hidden" name="&#39;&lt;/span> &lt;span class="op">+&lt;/span> k &lt;span class="op">+&lt;/span>
                &lt;span class="st">&#39;" value="&#39;&lt;/span> &lt;span class="op">+&lt;/span> v &lt;span class="op">+&lt;/span> &lt;span class="st">&#39;"&gt;&#39;&lt;/span>))&lt;span class="op">;&lt;/span>
            &lt;span class="op">}&lt;/span>)&lt;span class="op">;&lt;/span>
        &lt;span class="va">form&lt;/span>.&lt;span class="at">appendTo&lt;/span>(&lt;span class="st">&#39;body&#39;&lt;/span>).&lt;span class="at">submit&lt;/span>().&lt;span class="at">remove&lt;/span>()&lt;span class="op">;&lt;/span>
        &lt;span class="cf">return&lt;/span>&lt;span class="op">;&lt;/span>
      &lt;span class="op">}&lt;/span>
      &lt;span class="cf">if&lt;/span>(&lt;span class="va">response&lt;/span>.&lt;span class="at">status&lt;/span> &lt;span class="op">==&lt;/span> &lt;span class="st">"ok"&lt;/span>)&lt;span class="op">{&lt;/span>
         &lt;span class="at">showResult&lt;/span>(&lt;span class="va">response&lt;/span>.&lt;span class="at">data&lt;/span>)&lt;span class="op">;&lt;/span>
      &lt;span class="op">}&lt;/span>&lt;span class="cf">else&lt;/span>&lt;span class="op">{&lt;/span>
         &lt;span class="at">showError&lt;/span>(&lt;span class="st">&#39;Error: &#39;&lt;/span>&lt;span class="op">,&lt;/span> &lt;span class="va">response&lt;/span>.&lt;span class="at">msg&lt;/span>)&lt;span class="op">;&lt;/span>
      &lt;span class="op">}&lt;/span>
    &lt;span class="op">}&lt;/span>
&lt;span class="op">}&lt;/span>)</code></pre>
</div>

确实是请求了两次，返回了两次file的内容，增大了带宽等负担，实测chrome，第一次response返回了实际的数据，第二次请求不是ajax请求，浏览器弹框保存文件，juery有log信息`Resource interpreted as Document but transferred with MIME type text/csv:`；好处client的请求不变，仅仅将Ajax请求改为不通过的form请求，server端处理简单，不需要改变，只需要一个action即可。其实再加个标记可以防止server发回两次数据的。

### server端逻辑改变 {#server端逻辑改变}

server端在第一次请求的时候不直接返回file，而是返回一个url，该url可以获取文件，通过iframe的方式再请求一次，然后iframe的src指向最新的资源(可以是直接如上得file资源)；或者直接用一个get请求去下载文件。 同样是请求了两次，第一次仅仅返回一个url(不管这个url是直接返回的file content还是说get请求)，第二次才返回真正的file内容，带宽较少，但server端需要有两个action进行处理。

Reference:

  * [File Download requests using jquery/POST request with psuedo ajax](https://gist.github.com/DavidMah/3533415)
  * [Handle file download from ajax post](http://stackoverflow.com/questions/16086162/handle-file-download-from-ajax-post)
  * [Javascript/jquery to download file via POST with JSON data](http://stackoverflow.com/questions/3499597/javascript-jquery-to-download-file-via-post-with-json-data)