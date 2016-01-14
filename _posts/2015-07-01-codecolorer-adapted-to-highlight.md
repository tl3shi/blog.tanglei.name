---
id: 2707
title: 将代码高亮插件codecolorer替换为highlight
date: 2015-07-01T00:41:39+00:00
author: tanglei
layout: post
guid: http://www.tanglei.name/?p=2707
permalink: /codecolorer-adapted-to-highlight/
duoshuo_thread_id:
  - 1351844048792453522
categories:
  - wordpress
  - 我做站长
  - 经验技巧
tags:
  - codecolorer
  - highlight
  - plugin
  - wordpress
  - 代码高亮
  - 前端
  - 经验技巧
---
最近在写一个wordpress小的客户端发布工具，就是直接写markdown，然后转为html发布到wordpress，为什么要写?

  * 不太想换之前已有的blogs，试过相应的工具将已有的wordpress blog转为markdown，效果不是很好。//直接用github+jekyll之类的静态站点
  * wordpress已有的支持markdown的插件貌似都不怎么理想，想兼容之前的比较麻烦，特别是用了代码高亮之类的插件//用wordpress已有的支持markdown的插件

所以就写了，目前的技术方案是： `本地markdown+pandoc——>html——>wordpress-xmlrpc——>wordpress server` 这样的好处是：

  * 仅仅要对已有的blog进行细小的改动即可，即改下那些po了代码的文章；
  * 本地的markdown方便管理和备份，也方便生成其他如pdf等格式；
  * win下之前还有wlw工具方便发布带有图片的blog，但在mac、linux下找不到相应方便的工具，现在用这个统一的client就比较方便传图片等资源。

本篇文章是讨论解决之前文章代码高亮的问题。一方面，现在的代码高亮是基于pandoc的，pandoc会把代码拆分添加各种tag，然后根据tag去css，且生成的html是与之前的codecolorer不兼容的，开启codecolorer插件后，现在的文章乱得一塌糊涂； 另外一方面，关闭codecolorer后，由于现在的文章代码已经不是独立的代码，是带有各种html标签的文本，解决方案是将之前的所有post中含有的代码都用pandoc转换一下，这个成本太高；后来找到一个代码高亮的插件可以自定义代码区域的标签，且是通过前端实现的，不占用服务器资源，于是就采用了这款插件[hightlight](https://highlightjs.org/)。

codecolorer之前的代码区域基本上都是通过`[cc lang="java"]java code[/cc]`实现的，hightlight可以自定义html标签， 所以大致只需要将原来的文章中所有的`[cc]` 替换成`<cc>`即可，不能用hightlight默认的`<pre><code></code><pre>`，这个又会跟pandoc的冲突(其实也可以，后面会说怎么自定义让哪些文章启用highlight)。

在将代码高亮插件codecolorer替换为highlight过程中，遇到的主要问题是：

  * codecolorer之前的代码区域仅用`[cc]`标签包围，highlight自定义标签时，换行符会出现问题。`hljs.configure({useBR: true});` 不生效，参见[hightligth讨论](https://github.com/isagalaev/highlight.js/issues/860)，结果是要求code中需要包含`<br>`标签，这不扯么。。。解决方法是手动通过js添加`<br>`。
  * 换行符问题解决了，代码缩进有出现问题了。囧。后来想想还是手动在`<cc>`周围添加`<pre>`吧。 //注意在前端加时`<cc>`区域中间的内容会被wordpress 给添加一些`<br/><p>`之类的标签切这个标签可能会添加得不合理比如代码的一部分和代码以上的文字在一个p里面，会导致选择器选择cc不能全部选到，这个禁用即可(这样可能导致之前的文章排版不太正确)，方法是主题中`the_content('Continue reading &raquo;');`替换为`echo $post->post_content;`。在后端即数据库端加就不用管。所以还是直接数据库添加较好。

代码如下:

<pre class="sourceCode javascript"><code class="sourceCode javascript">&lt;link rel=&lt;span class="st">"stylesheet"&lt;/span> href=&lt;span class="st">"https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.6/styles/default.min.css"&lt;/span>&gt;
&lt;script src=&lt;span class="st">"https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.6/highlight.min.js"&lt;/span>&gt;&lt;&lt;span class="ot">/script&gt;&lt;/span>
&lt;span class="ot">&lt;script src="http://code.jquery.com/jquery&lt;/span>&lt;span class="fl">-2.1.4&lt;/span>.&lt;span class="ot">min&lt;/span>.&lt;span class="fu">js&lt;/span>&lt;span class="st">"&gt;&lt;/script&gt;&lt;/span>
&lt;script&gt;
   &lt;span class="kw">if&lt;/span>(&lt;span class="kw">false&lt;/span>)
       &lt;span class="ot">hljs&lt;/span>.&lt;span class="fu">initHighlightingOnLoad&lt;/span>(); &lt;span class="co">//default tag&lt;pre&gt;&lt;code&gt;&lt;/span>
   &lt;span class="kw">else&lt;/span>
    &lt;span class="fu">$&lt;/span>(document).&lt;span class="fu">ready&lt;/span>(&lt;span class="kw">function&lt;/span>() {
       &lt;span class="co">//hljs.configure({useBR: true});//this does NOT work, the original code should contains &lt;br&gt;, &lt;/span>
       &lt;span class="co">//see https://github.com/isagalaev/highlight.js/issues/860&lt;/span>
       &lt;span class="co">//$(&#39;cc&#39;).each(function(){&lt;/span>
       &lt;span class="co">//    $(this).wrap("&lt;pre&gt;&lt;/pre&gt;"); //db substitute&lt;/span>
           &lt;span class="co">//var codestr = $(this).html();&lt;/span>
           &lt;span class="co">//$(this).html(codestr.replace(/\n/g, &#39;&lt;br&gt;&#39;)); //manually substitute, add &lt;pre&gt;, no need&lt;/span>
       &lt;span class="co">//});&lt;/span>
       &lt;span class="fu">$&lt;/span>(&lt;span class="st">&#39;pre cc&#39;&lt;/span>).&lt;span class="fu">each&lt;/span>(&lt;span class="kw">function&lt;/span>(i, block) {
           &lt;span class="ot">hljs&lt;/span>.&lt;span class="fu">highlightBlock&lt;/span>(block);
       });
   });
&lt;&lt;span class="ot">/script&gt;&lt;/span></code></pre>

Demo 见[这里](./codecolorer-adapted-to-highlight/highlighttest.html)。

然后就是使这些js代码应用到之前的所有文章中，直接添加到每篇含有代码的文章中的正文里容易被wordpress过滤转义掉，且加载的顺序不正确也会导致代码高亮出现问题，如果加在全站的header中有造成不必要的浪费，幸好wordpress提供了给每篇文章自定义的功能，wordpress后台发布文章时有个自定义栏目，可以给每篇文章加个标签，然后wp加载的时候根据这篇文章的标签采用不同的逻辑加载。方法可以参考[在 WordPress 指定页面加载指定 JavaScript 或 CSS 代码](http://loo2k.com/blog/wordpress-page-javascript-css-code/)[<sup>1</sup>](#fn1){#fnref1.footnoteRef}

最后就是修改那些含有代码的文章，修改`[cc]`标签，给文章添加自定义字段。sql语句如下： 自定义条目：enable_highlight 值：

<pre class="sourceCode html"><code class="sourceCode html">&lt;span class="kw">&lt;link&lt;/span>&lt;span class="ot"> rel=&lt;/span>&lt;span class="st">"stylesheet"&lt;/span>&lt;span class="ot"> href=&lt;/span>&lt;span class="st">"../wp-content/blogresources/highlightconfig/highlight.default.min.css"&lt;/span>&lt;span class="kw">&gt;&lt;/span>
&lt;span class="kw">&lt;script&lt;/span>&lt;span class="ot"> src=&lt;/span>&lt;span class="st">"../wp-content/blogresources/highlightconfig/jquery-2.1.4.min.js"&lt;/span>&lt;span class="kw">&gt;&lt;/script&gt;&lt;/span>
&lt;span class="kw">&lt;script&lt;/span>&lt;span class="ot"> src=&lt;/span>&lt;span class="st">"../wp-content/blogresources/highlightconfig/enable_highlight.js"&lt;/span>&lt;span class="kw">&gt;&lt;/script&gt;&lt;/span></code></pre>

主题的header.php文件中，`<?php wp_head(); ?>`之后添加如下代码进行过滤：

<pre class="sourceCode php"><code class="sourceCode php">&lt;span class="kw">&lt;?php&lt;/span> &lt;span class="kw">if&lt;/span> &lt;span class="ot">(&lt;/span>is_single&lt;span class="ot">()&lt;/span> || is_page&lt;span class="ot">())&lt;/span> {
    &lt;span class="kw">$head&lt;/span> = get_post_meta&lt;span class="ot">(&lt;/span>&lt;span class="kw">$post&lt;/span>-&gt;&lt;span class="kw">ID&lt;/span>&lt;span class="ot">,&lt;/span> &lt;span class="st">&#39;enable_highlight&#39;&lt;/span>&lt;span class="ot">,&lt;/span> &lt;span class="kw">true&lt;/span>&lt;span class="ot">);&lt;/span> 
    &lt;span class="kw">if&lt;/span> &lt;span class="ot">(&lt;/span>!&lt;span class="fu">empty&lt;/span>&lt;span class="ot">(&lt;/span>&lt;span class="kw">$head&lt;/span>&lt;span class="ot">))&lt;/span> { &lt;span class="kw">?&gt;&lt;/span> 
        &lt;&lt;span class="ot">?&lt;/span>php &lt;span class="fu">echo&lt;/span> &lt;span class="kw">$head&lt;/span>&lt;span class="ot">;&lt;/span> &lt;span class="kw">?&gt;&lt;/span> 
&lt;&lt;span class="ot">?&lt;/span>php } } &lt;span class="kw">?&gt;&lt;/span></code></pre>

其实可以优化下，不用jQuery的，懒得搞了。

呃，每篇文章都得单独添加一个wp_postmeta。 mysql replace没有正则匹配，一个一个来了。

<pre class="sourceCode sql"><code class="sourceCode sql">&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[/cc]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;/cc&gt;&lt;/pre&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
(&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[/cc]%&#39;&lt;/span>);</code></pre>

当试图用以上sql进行查询更新时，提示 "You can&#8217;t specify target table &#8216;wp_posts&#8217; for update in FROM clause"，因为这样对同一个表操作会冲突，中间加一个临时表解决问题。[<sup>2</sup>](#fn2){#fnref2.footnoteRef}

<pre class="sourceCode sql"><code class="sourceCode sql">&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[/cc]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;/cc&gt;&lt;/pre&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
(&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[/cc]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp);</code></pre>

<pre class="sourceCode sql"><code class="sourceCode sql">&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[cc lang="python"]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="python"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[cc lang="python"]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp);  &lt;span class="co">/*8 rows*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[cc lang="php"]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="php"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[cc lang="php"]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*8 rows*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[cc lang="cpp"]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="cpp"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[cc lang="cpp"]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*6*/&lt;/span> 

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[cc lang="java"]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="java"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[cc lang="java"]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*16*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[cc lang="c#"]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="csharp"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> 
&lt;span class="kw">in&lt;/span> ( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[cc lang="c#"]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*4*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[cc lang="c++"]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="cpp"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[cc lang="c++"]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*6*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[cc lang="html"]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="html"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> 
&lt;span class="kw">in&lt;/span> ( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[cc lang="html"]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*1*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[cc lang="xml"]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="xml"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> 
&lt;span class="kw">in&lt;/span> ( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[cc lang="xml"]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*5*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[cc lang="C"]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="C"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[cc lang="C"]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*10*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[/cc]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;/cc&gt;&lt;/pre&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[/cc]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); 
&lt;span class="co">/*66*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;&lt;code&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%&lt;code%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*11*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;&lt;/code&gt;&#39;&lt;/span>, &lt;span class="st">&#39;&lt;/cc&gt;&lt;/pre&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%&lt;/code&gt;%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*11*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[cc lang="sql"]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="sql"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[cc lang="sql"]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*5*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[cc lang="c"]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="c"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> 
&lt;span class="kw">in&lt;/span> ( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[cc lang="c"]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*4*/&lt;/span>

&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="st">&#39;[cc lang="javascript"]&#39;&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="javascript"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> 
&lt;span class="kw">in&lt;/span> ( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%[cc lang="javascript"]%&#39;&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*2*/&lt;/span>
 
&lt;span class="kw">UPDATE&lt;/span> wp_posts &lt;span class="kw">SET&lt;/span> post_content = &lt;span class="kw">REPLACE&lt;/span>( post_content, &lt;span class="ot">"[cc lang=&#39;python&#39;]"&lt;/span>, &lt;span class="st">&#39;&lt;pre&gt;&lt;cc class="python"&gt;&#39;&lt;/span> ) &lt;span class="kw">where&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">in&lt;/span> 
( &lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="ot">"%[cc lang=&#39;python&#39;]%"&lt;/span>) &lt;span class="kw">as&lt;/span> tmp); &lt;span class="co">/*2*/&lt;/span>
 
&lt;span class="kw">INSERT&lt;/span> &lt;span class="kw">INTO&lt;/span> wp_postmeta (post_id, meta_key, meta_value) 
&lt;span class="kw">SELECT&lt;/span> wp_posts.ID, &lt;span class="st">&#39;enable_highlight&#39;&lt;/span>, 
&lt;span class="st">&#39;&lt;link rel="stylesheet" href="../wp-content/blogresources/highlightconfig/highlight.default.min.css"&gt;&lt;/span>
&lt;span class="st">&lt;script src="../wp-content/blogresources/highlightconfig/jquery-2.1.4.min.js"&gt;&lt;/script&gt;&lt;/span>
&lt;span class="st">&lt;script src="../wp-content/blogresources/highlightconfig/enable_highlight.js"&gt;&lt;/script&gt;&#39;&lt;/span> 
&lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> wp_posts.ID &lt;span class="kw">in&lt;/span> (&lt;span class="kw">SELECT&lt;/span> &lt;span class="kw">ID&lt;/span> &lt;span class="kw">FROM&lt;/span> wp_posts &lt;span class="kw">WHERE&lt;/span> wp_posts.post_content &lt;span class="kw">LIKE&lt;/span> &lt;span class="st">&#39;%&lt;/cc&gt;&lt;/pre&gt;%&#39;&lt;/span>);</code></pre>

参考文献：

<li id="fn1">
  <p>
    <a href="http://loo2k.com/blog/wordpress-page-javascript-css-code/">在 WordPress 指定页面加载指定 JavaScript 或 CSS 代码</a><a href="#fnref1">↩</a>
  </p>
</li>

<li id="fn2">
  <p>
    <a href="http://stackoverflow.com/questions/8333376/mysql-1093-you-cant-specify-target-table-giveaways-for-update-in-from-clau">MySQL #1093 &#8211; You can&#8217;t specify target table &#8216;giveaways&#8217; for update in FROM clause</a><a href="#fnref2">↩</a>
  </p></fn></footnotes>