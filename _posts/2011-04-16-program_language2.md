---
id: 454
title: 软考：程序语言部分(二)
date: 2011-04-16T12:52:01+00:00
author: tanglei
layout: post
guid: http://www.tanglei.name/?p=454
permalink: /program_language2/
duoshuo_thread_id:
  - 1351844048792453456
categories:
  - 软考
tags:
  - 编译原理
---
上接：<http://www.tanglei.name/program_language1/>

以下内容就是编译原理了。

**2****．重点与难点** ****

**2.1****文法及语言形式描述：** ****

本部分的内容难点是编译原理。与程序员级别的要求一样，这部分的内容比较复杂，不易理解。可以从下面几个知识点来掌握：

**文法和语言形式描述**

这一部分主要是需要搞清楚一些基本概念和基本原理，这也是编译原理的最基本的知识。

基本定义：包括字母表、字符、字、字长度、空字、字运算等等。

文法的定义：描述语言的语法结构的形式规则称为文法。

文法**_G_**是一个四元组，可表示为**_G_**（**_VT_**, **_VN_**, **_S, P_**）。

**_VT_**是一个非空有限集，每个元素称为终结符。

**_VN_**是一个非空有限集，每个元素称为非终结符。

**_P_**是一个非终结符，称为开始符号；它至少要在一条产生式中作为左部出现。

**_S_**是一个产生式集合（有限）。

**句子和语言：**

主要涉及几个概念。

I.   直接推导与推导（区别是否直接导出）

II.  直接归约与归约（直接推导和推导的逆过程）

III. 句型和句子（由开始符号推导出的称为句型，仅含终结符的句型称为句子）

IV.  语言（句子的全体）

**文法的分类：**

文法根据对产生式施加不同的限制，分成4种类型，即0型、1型、2型和3型。下表列出了这几种文法的特点和区别。

<table border="0" cellspacing="0" cellpadding="0">
  <tr>
    <td width="95" valign="top">
      <strong>文法类型</strong>
    </td>
    
    <td width="161" valign="top">
      <strong>文法名称</strong>
    </td>
    
    <td width="128" valign="top">
      <strong>语言名称</strong>
    </td>
    
    <td width="128" valign="top">
      <strong>对应的自动机</strong>
    </td>
  </tr>
  
  <tr>
    <td width="95" valign="top">
      0型（PSG）
    </td>
    
    <td width="161" valign="top">
      短语结构文法
    </td>
    
    <td width="128" valign="top">
      递归可枚举语言
    </td>
    
    <td width="128" valign="top">
      图灵机（Turing）
    </td>
  </tr>
  
  <tr>
    <td width="95" valign="top">
      1型（CSG）
    </td>
    
    <td width="161" valign="top">
      上下文有关文法
    </td>
    
    <td width="128" valign="top">
      上下文有关语言
    </td>
    
    <td width="128" valign="top">
      线性界限自动机
    </td>
  </tr>
  
  <tr>
    <td width="95" valign="top">
      2型（CFG）
    </td>
    
    <td width="161" valign="top">
      上下文无关文法
    </td>
    
    <td width="128" valign="top">
      上下文无关语言
    </td>
    
    <td width="128" valign="top">
      非确定下推自动机
    </td>
  </tr>
  
  <tr>
    <td width="95" valign="top">
      3型
    </td>
    
    <td width="161" valign="top">
      右线性文法（正规文法）
    </td>
    
    <td width="128" valign="top">
      有限状态文法
    </td>
    
    <td width="128" valign="top">
      有限状态自动机
    </td>
  </tr>
</table>

2型文法（上下文无关文法）：

如今程序语言基本都可以用它来描述。重点涉及几个概念，对于这几个概念可以根据书上的例子来理解和掌握。在复习资料上有例题，可以找一个分析一下（99页）；

Ø         规范推导（最右推导）：总是对句型的最右端的非终结符进行置换；

Ø         短语、直接短语和句柄(句柄：最左直接短语)

Ø         素短语：至少含有一个终结符，除本身外不含更小的素短语

Ø         规范归约

Ø         语法树和文法的二义性

对于上面的术语，一定要知道其意义，还要知道其具体的做法。

**2.2** **词法分析** ****

词法分析的任务是把构成源程序的字符串转换成单词符号串的中间程序。词法规则可用3型文法（正规文法）或正规表达式描述。转换方法有人工的状态转换图方法和有限自动机的自动方法。

这部分主要涉及以下两个方面的内容。

Ø         正规表达式和正规集

Ø         有限自动机

有限自动机作为一种识别装置，它能准确地识别正规集。它分为两类：确定的有限自动机（DFA）和不确定的有限自动机（NFA）。在有限自动机理论中，可以通过子集法的算法来实现NFA到DFA的转换。

**2.3** **语法分析** ****

语法分析的任务是识别由词法分析给出的单词符号序列是否为给定文法的正确句子（程序）。语法分析常用的方法有两类：

◆自底向上分析方法（LR分析法和算符优先分析法）

也称为移进-归约分析法。对“可归约串”刻画的不同，形成两种不同的分析方法，即规范归约分析法和算符优先分析法。

◆自顶向下分析方法

也称为面向目标的分析方法。存在两种分析方法，递归子程序法和预测分析法，都使用LL（1）文法来进行语法分析。

例题：假设某程序语言的文法如下：

S→a | b | (T)

T→TdS | S

其中，V<sub>T</sub>={a,b,d,(,)}，V<sub>N</sub>={S,T}，S是开始符号。

考查该文法，称句型(Sd(T)db)是S的一个**A** 。其中**B**是句柄；**C**是素短语；**D**是该句型的直接短语；**E**是短语。

**A****：** ****①最左推导           ②最右推导          ③规范推导          ④推导

**B****：** ****①S                  ②b                 ③(T)               ④Sd(T)

**C****：** ****①S                  ②b                 ③(T)               ④Sd(T)

**D****：** ①S                  ②S,(T),b         ③S,(T),TdS,b  ④(Sd(T)db)

**E****：** ①(Sd(T)db)      ②d(T)             ③Td                ④Sd(T)d

此句型的语法树如下所示：

S

(T)

（T  d   S）

（T  d  S   b）

（S   （T））

从语法树我们可以看出，短语就是位于同一个非终端结点的所有叶子结点，比如S、Sd(T)、Sd(T)db就是是相对于T的短语，b、(T)、(Sd(T)db)是相对于S的短语。而直接短语则进一步要求这些叶子结点的非终端结点是它们的直接父结点。因此可以S、(T)、b都是该句型的直接短语。语法树上最左的直接短语就是句柄，本题中是S。

所谓素短语是指这样一个短语，它至少含有一个终结符，并且除它自身之外不再含任何更小的素短语。最左素短语则指处于句型最左边的那个素短语。

最左推导是指任何一步推导过程σ→β，都是对σ中的最左非终结符进行替换。因此，在语法树中也很容易看出，如果语法树中的只有最左的非终结符结点（包括各级结点）具有其子树，则它就是最左推导。最右推导与之类似，最右推导也称规范推导。

**2.4****代码优化** ****

优化是对程序进行等价（指不改变程序的运行结果）变换，经变换后的程序能生成更有效（运行时间更短、占用空间更小）的目标代码。

根据优化所涉及的程序范围，可分为局部优化、循环优化和全局优化三个不同的级别

**编译原理重点难点归纳：**

了解编译程序工作的大致过程，要清楚编译程序是如何生成的。请大家记忆并理解以下概念：编译程序，解释程序，翻译程序，扫描器，分析器，编译前端与后端，符号表。

要掌握的几个重量级概念：上下文无关文法，语法分析树和二义性，同时也引出了与此紧密联系的其它概念：推导，句型，句子，最左推导，最右推导等。

最后给出了另一个常考点：乔姆斯基的方法分类。

1.上下文无关文法的定义，判断和转化，以及与上下文无关文法密切相关的概念。

首先，应该掌握上下文无关文法的四个构成要素；

其次，应该清楚对于上下文无关文法，其每个产生式的左部和右部必须满足的条件。

在有关上下文无关文法的考点中，有这样几种考查方式：

n          给出某语言的自然语言描述方式，要求写该语言的上下文无关文法表述形式；

n          给出某语言的上下文无关文法，要求用自然语言描述该语言；

n          给出某语言的上下文无法方法，要求证明该文法是否二义；

n          给出某语言的上下文无关文法，要求给出指定句子的最左或最右推导；

n          给出某语言的上下文无关文法，要求给出指定句子的语法分析树；

n          给出一个具有二义性的上下文无关文法，要求将其转换成非二义性的。

2.乔姆斯基的文法分类：

首先，应该非常清楚乔姆斯基对于四种文法分类的定义，并能理解其含义。几种文法中，最基本的是0型文法，读者可以将它理解为其它所有文法的基础，它是可以表示任何语言的文法。后面的1，2,3三种文法，是分别对于0型文法产生式的两边作了不同的限制之后，形成了新的文法。比如：规定0型文法的每个产生式中，其左边字符集长度小于右边字符集长度并且同时规定开始符号只可出现于产生式的左边，不能出现在任何产生式的右边，这样，就成为了1型文法(即上下文有关文法)。其它与此类似，在1型文法的基础上，进一步规定该文法的任意产生式，其左部只允许有一个字符且必须为非终结符，这样就构成了上下文无关文法；再在上下文无关文法的基础上进行限制：规定除了左部有且只有一个非终结符外，还特别规定右部最多只允许有两个字符，当为两上字符时必须一个为非终结符，另一个为终结符，而当只有一个字符时，必须为终结符，这样的文法就成了正规文法。这样一层套一层的限制，就形成了从0型到3型文法的定义体制，每一层都是在前一层基础上进行定义的，所以说前一层一定比该层表示的范围要广，因为其受的限制要少。

那么，我们在判断一个文法时应该以什么规则来判断呢？这个规则当然是：3->2->1->0.也就是说，我们判断是从高到低来判断的，比如：一旦判断其属于正规文法之后就没必要再判断其是否属于上下文无关的了(因为它必定属于上下文无关，我们应该以最高规则来判定其属于的文法类型)，其它情况与此类推。只有当我们判断不属于3型文法时，我们才向下判断，其是不是属于2型的，若不属于2型的，则依此类推再向下判断。最终的结果如果不属于3，2和1三种类型，那就只有属于0型了。

“给定一个文法，要求判断其属于何种文法”是一个重要考点，其出题形式可能是填空，选择等多种题型。

正规式和有限自动机，对于词法分析一章的考点，可以说80%到90%以上集中在这一节的内容上。针对于这一节的知识点介绍和考点分析：

1)        词法分析器的功能：输入的是源程序，输出的是分析完成的单词符号；

2)        状态转换图：是一张有向图，用于标识在特定的输入下词法分析器应该选择的分析方向。

对于考点1)，作为选择进行考查，而对于考点2)，多数是与有限自动机一些考查，要求给出以“状态图”表示的确定有限自动机，或者是要求直接给出针对于某正规式的状态转换图，大家记住一句话：状态转换图，就是一张当输入不同的内容时，选择不同分析路径的有向图。

下面，我们重点看一下有关“正规式与有限自动机”这一考点的各种可能考查形式：

a.题目给定一正规式，要求给出其NFA，DFA或最简DFA形式。

b.题目给定一用状态图表示的NFA，要求给出其对应的DFA或最简DFA形式。

c.题目给定一NFA，DFA或最简DFA，要求给出其对应的正规式。

d.题目给定一正规集，要求给出其相应的DFA。

e.题目给定一用自然语言描述的正规集，要求给出其相应的正规式表示形式。

这些考点，综合起来看，是在正规式，正规集，NFA和DFA之间作各种可能的转换，当然这种转换正确与否的判断标准就是转换之后的内容是不是与转换之前的内容等价，如果等价，我们就认为转换是正确的。

在考点e这类的转换题目中，有一些是需要另外规纳出来的，他们在某一方面具有共同的特征，如果掌握了其中一题，将可举一反三解出其它题。

比如有以下的几种题目就可以作以总结：

1.求偶（奇）数个a与偶（奇）数个b构成的语言的正规式

2.求能被3（4、5、或其它任意给定的n）整除的正规式的DFA

3.求不以（或以）n（n从0到9）开头的XXXX（符号某种条件的）奇（偶数）数的正规式

以上三种类型的考题，在每一种类型中，都是有规律可循的，也都有简便的方法可以帮助我们快速求解其正规式，进而快速确定DFA及最简DFA。针对于这三种类型的解题思路分析，我会在另外的文章中给出。

当词法分析器对源程序进行了词法分析，获得了一个个独立的单词符号后，编译程序总控模块就会调用语法分析子程序对这些单词符号集进行语法分析，也就是：利用该文法的产生式来判断这些单词符号是否足以构成一个在语法上正确的程序。如果可以构成一个在语法上正确的程序，则接着作编译下面的工作，比如：语法制导翻译，中间代码生成、代码优化等工作；而如果不能构成一个在语法上正确的程序，则给出相应的错误提示并将错误信息记入对应的数据记录中。

语法分析的规则主要基于两种：自上而下分析和自下而上分析。自上而下分析的大致思路是：根据产生式规则，从产生式的开始符号进行推导，一直推导到可以产生当前要判断的这个句子为止。如果推导了所有可能情况，但没有推出这样的句子，那么这个句子就是不符合该语言的语法规则的（产生式即定义了语言的语法规则）。

一种自上而下的分析方法：LL(1)分析法，下面，我介绍一下本章的主要常考知识点及考查角度：

1.给定一文法，要求将其改造成可以进行自上而下分析的形式。

这里面涉及到两方面的知识点：

左递归的去除及公因子的提取。所谓的左递归是指产生式是形如：P->Pab&#8230;的形式，即：产生式右边的第一个字符就是该产生式左边的那个非终结符。当一个文法中有左递归的产生式时，是无法进行自上而下推导的，因为只要这个产生式被推导，就势必会使这种推导过程陷入一种递归循环无休止推导的情形。去除左递归的方法是比较简单的，其基本思路是将左递归通过转化变成与之等价的右递归。即将形如：P->Pa|b 形式的左递归变成如下形式：P->bP&#8217;,P&#8217;->aP&#8217;|e(注：e表示空)。提取公因子的目的是为了避免推导过程中的回溯，也就是使每一次的向下推导是唯一的，而不是有多个选择，因为有多个选择的话就可能出现回溯。

2.给定一文法，要求判断其是否为LL(1)文法。判断一个文法是否为LL(1)文法主要有两种方法：一种是判断文法是否二义，如果二义，则文法必定不为LL(1)（注意：此命题的否合命题不真）；二是根据关于LL(1)文法成立的三个条件。显然，第一种判断方法效率是比较高的，但是，其只能判断文法“不为”LL(1)的，并不能判定文法“是”LL(1)的，要判断文法“是”LL(1)的，就得用第二种方法，但在考题中，如果要求你判断某文法是否为LL(1)的，则该文法多半不是LL(1)的，而且此点可以很容易地用二义性来证明，这是一种常考形式。

3.给定一文法，要求构造LL(1)分析表。LL(1)分析的重点和难点内容都在其分析表的构造上，后面要讲的LR分析也是，它的难点也在于其分析表的构造。构造LL(1)分析表是一个常考点，也是大分值题的可能出题点，对于普通学校而言，相比于LR分析，他们更喜欢考LL(1)。LL(1)分析表构造前，需要先弄清FIRST集和FOLLOW集的构造方法，简单地说，FIRST集是用于求非终结符推出的产生式中的第一个终结符的，而FOLLOW集是用于求与该非终结符后紧邻的那个终结符的。FIRST集的构造方法见编译原理的教材，在构造的三个规则中，前两个规则都是比较容易理解的，第三个规则看上去就有点复杂了，我们简单地来看第三条规则，就是：当由X推出的产生式中前面若干个非终结符，其FIRST集均含有空时，就取这若干个非结符的后一个字符的FIRST集，当然，这“后一个字符”可能是终结符，也可能是非终结符，只要其FIRST集不为空就行；而当X推出的右边全是非终结符，且这些非终结符的FIRST集全含有空时，就把空加到FIRST(X)中。FOLLOW集的构造方法很简单，不作详细讲解了。LL(1)分析表的构造方法见教材，构造规则主要有3条。说到这里，大家应该明确分析表中的各个单元到底代表什么含义，我作一下简单的介绍：分析表中的最顶一行，是产生式中所有的终结符；分析表中的最左一列，是产生式中所有的非终结符；而产生式中间的诸多单元格则可以存放该文法的产生式或特殊标志(比如成功和错误标志)。这样的二维表格构成的单元格的含义是：当左边的非终结符遇到最上一行中的某个终结符时应该选择哪个产生式进行向下的推导，这个产生式就是放在对应二维坐标处的产生式。

4.给定一文法，先要求求解其LL(1)分析表，然后要求给出针对于某一个句子的具体分析过程。这个考点的第二问主要就是考查考生对预测分析程序的工作过程的理解了，预测分析程序完全是按照分析表机械工作的，针对于考生而言，要明确何时出栈，何时入栈，以及如何入栈，这些细节信息都是要通过作题掌握的，只理解而不会熟练解答是没有用的。

5.给定一文法，要求给出其递归下降分析程序。递归下降分析的条件也是无左递归及不带回溯，其构造的过程比较简单，就是将每个非终结符处理成可以互相递归调用的过程体。