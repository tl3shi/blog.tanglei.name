---
id: 1770
title: 2012百度实习生笔试题目
date: 2012-05-06T23:10:23+00:00
author: tanglei
layout: post
guid: http://www.tanglei.name/?p=1770
permalink: /intern-in-baidu-first-exam-2012/
duoshuo_thread_id:
  - 1351844048792453138
categories:
  - 实习那些事儿
tags:
  - 实习
  - 实习生
  - 百度
  - 笔试
---
【背景】

> 打算这个暑假再找个实习玩玩的，有些后悔之前拒掉创新工场一个小公司的实习offer了，应该作为保底的。因为今天去北大霸笔，告诉我不要08级的实习生，不过我还是做了笔试题目了。下面分享下今年的笔试题目，题目分为很多类型的，例如同行的同学申请的数据挖掘，我申请了通用的软件研发，题目大多数一样，只有最后一道题系统设计题目不一样而已。如果你也有兴趣的话，不妨看看这些题目，试着做做，写写代码，希望你留言交流哦。

  * 【简答题.1】

给定一个单词a，如果通过交换单词中字母的顺序可以得到另外的单词b，那么定义b是a的兄弟单词，例如单词army和mary互为兄弟单词。现在给定一个字典，用户输入一个单词，如何根据字典找出这个单词有多少个兄弟单词？要求时间和空间效率尽可能的高。

  * 【简单题.2】

进程线程有何区别及联系，如何理解“线程安全”问题？

  * 【简单题.3】

C和C++中如何动态分配和释放内存，他们的区别是什么？

  * 【算法和程序设计.1】

网页爬虫在抓取页面时，从指定的url站点入口开始爬取这个站点上的所有url link，抓取到下一级link对应的页面后，同样对该页面上的link进行抓取从而完成深度遍历。为简化问题，我们假设每个页面上至多只有一个link，如从[www.baidu.com/a.html](http://www.baidu.com/a.html)链接到[www.baidu.com/b.html](http://www.baidu.com/b.html)再链接到[www.baidu.com/x.html](http://www.baidu.com/x.html)，当爬虫抓取到某个页面时，有可能再链接回[www.baidu.com/b.html](http://www.baidu.com/b.html)，也可能爬取到一个不带任何link的终极页面。当抓取到相同的url或者不包含任何link的终极页面时即完成爬取。爬虫在抓取到这些页面后会建立一个单向链表，用来记录抓取到的页面。如：a.html->b.html->x.html&#8230;->NULL.
  
问：对于爬虫分别从[www.baidu.com/x1.html](http://www.baidu.com/x1.html)和[www.baidu.com/x2.html](http://www.baidu.com/x2.html)两个入口开始获得两个单向链表，得到这两个单向链表后，如何判断他们是否抓取到了相同的url？（假设页面url上百亿，存储资源受限，无法用hash方法判断其是否包含相同的url）
  
请先描述相应的算法，再给出相应的代码实现。（只需给出判断方法代码，无需爬虫代码）

  * 【算法和程序设计.2】

数组al[0,mid-1]和al[mid,num-1]是各自有序的，对数组al[0,num-1]的两个子有序段进行merge，得到al[0,num-1]整体有序。要求空间复杂度为O(1)。注：al[i]元素是支持'<&#8216;运算符的。

  * 【系统设计题】

百度搜索框中的suggestion提示功能是如何实现的？请给出实现思路和主要的数据结构、算法。有什么优化思路可以使得时间和空间效率最高？

&#8230;全文完