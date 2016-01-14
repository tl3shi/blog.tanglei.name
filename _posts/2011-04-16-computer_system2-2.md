---
id: 442
title: 软考：计算机系统知识(二)
date: 2011-04-16T12:16:38+00:00
author: tanglei
layout: post
guid: http://www.tanglei.name/?p=442
permalink: /computer_system2-2/
duoshuo_thread_id:
  - 1351844048792453368
categories:
  - 软考
tags:
  - 中央处理器CPU
  - 存储器系统
  - 输入/输出系统
---
上接<http://www.tanglei.name/computer_system1/>

**1.3****存储器系统：**

**概述**：

计算机中的存储系统是用来保存数据和程序的。对存储器最基本的要求就是存储容量要大、存取速度快、成本价格低。为了满足这一要求，提出了多级存储体系结构。一般可分为高速缓冲存储器、主存、外存3个层次，有时候还包括CPU内部的寄存器以及控制存储器。

n          衡量存储器的主要因素：存储器访问速度、存储容量和存储器的价格；

n          存储器的介质：半导体、磁介质和光存储器。

n          存储器的组成：存储芯片+控制电路（存储体+地址寄存器+数据缓冲器+时序控制）；

n          存储体系结构从上层到下层离CPU越来越远、存储量越来越大、每位的价格越来越便宜，而且访问的速度越来越慢

存储器系统分布在计算机各个不同部件的多种存储设备组成，位于CPU内部的寄存器以及用于CU的控制寄存器。内部存储器是可以被处理器直接存取的存储器，又称为主存储器，外部存储器需要通过I/O模块与处理器交换数据，又称为辅助存储器，弥补CPU处理器速度之间的差异还设置了CACHE，容量小但速度极快，位于CPU和主存之间，用于存放CPU正在执行的程序段和所需数据。

通常衡量主存容量大小的单位是字节或者字，而外存的容量则用字节来表示。字是存储器组织的基本单元，一个字可以是一个字节，也可以是多个字节。

**信息存取方式**：信息的存取方式影响到存储信息的组织，常用的有4种，

◆顺序存取

存储器的数据是以记录的形式进行组织，对数据的访问必须按特定的线性顺序进行。磁带存储器的存取方式就是顺序存取。

◆直接存取

共享读写装置，但是每个记录都有一个唯一的地址标识，共享的读写装置可以直接移动到目的数据块所在位置进行访问。因此存取时间也是可变的。磁盘存储器采用的这种方式。

◆随机存取

存储器的每一个可寻址单元都具有唯一地址和读写装置，系统可以在相同的时间内对任意一个存储单元的数据进行访问，而与先前的访问序列无关。主存储器采用的是这种方式。

◆相联存取

也是一种随机存取的形式，但是选择某一单元进行读写是取决于其内容而不是其地址。Cache可能采用该方法进行访问。

衡量存储器系统性能的指标有以下几种：

Ø         存取时间：一次读/写存储器的时间

Ø         存储器带宽：每秒能访问的位数。

Ø         存储器周期：两次相邻的存取之间的时间

Ø         数据传输率：每秒钟数据传输的bit数目。

**主存储器：**

主存储器是指能由CPU直接编程访问的存储器，它存放需要执行的程序与需要处理的数据。因为它通常位于所谓主机的范畴，常称为内存。如果内存的地址为n位，容量为2的n次。

主存储器的种类很多，主要有：

Ø         随机存储器（RAM）：可以读出和写入，随机访问存取，断电消失

Ø         只读存储器（ROM）：只能读出原有的内容，不能写入新内容

Ø         可编程ROM（PROM）

Ø         可擦除PROM（EPROM）

Ø         电可擦除PROM（E<sup>2</sup>PROM）

Ø         闪速存储器（flash memory）

实际的存储器总是由一片或多片存储芯片配以控制电路组成的，其容量往往是W×B来表示。W表示该存储器的存储单元（word）的数量，而B表示每一个word由多少bit组成。

**辅助存储器：**

由于主存容量有限（受地址位数、成本、速度等因素制约），在大多数计算机系统中设置一级大容量存储器作为对主存的补充与后援。它们位于主机的逻辑范畴之外，常称为外存储器，简称外存。

外存的最大特点是容量大、可靠性高、价格低，主要有两大类。

◆磁表面存储器：这类外存储器主要包括磁带和磁盘存储器。

▲磁带

磁带存储设备是一种顺序存取的设备，存取时间较长，但存储容量大。磁带上的信息是以文件块的形式存放的，而且便于携带，价格便宜。按它的读写方式可分为两种：启停式和数据流。

▲磁盘存储器

磁盘存储器是目前应用最广泛的外存储器。它存取速度较快，具有较大的存储容量，适用于调用较频繁的场合，往往作为主存的直接后援，为虚拟存储提供了物理基础。可分为软盘和硬盘。

◆光存储器

光盘存储器是利用激光束在记录表面存储信息，根据激光束的反射光来读出信息。按照它的记录原理可分为形变型、相变型（晶相结构）和磁光型。有CD、CD-ROM、WORM、EOD等。

CD-ROM：只读光盘，只能一次性写入数据，由生产厂家将数据写入，永远保存

CD-WO：可由用户写入一次，写入后不能修改或擦除，但是可以多次读出

CD-MO：可改写光盘，可以读出也可以写入数据；

光盘存储器的特点：

大容量、标准化、相容性、持久性、实用性

**辅助存储器方面的计算：**

1.存储容量为capacity=n\*t\*s*b，n为存放数据的总盘面数；t为每面的磁道数；s为每道的扇区数；b为每个扇区存储的字节数

2.寻道时间为磁头移动到目标磁道所需的时间。

3.等待时间为待读写的扇区旋转到磁头下方所用的时间。一般用磁道旋转一周所用的时

间的一半作为平均等待时间。

4．磁盘存取时间=寻道时间+等待时间。

5．位密度：沿磁道方向，单位长度存储二进制信息的个数；

6．道密度：沿磁盘半径方向，单位长度内磁道的数目；

7. 数据传输速率R=B/T，B为一个磁道上记录的字节数，T为每转一周的时间

8．磁带机的容量计算：（这些公式要熟悉记住）

数据传输率=磁带记录密度*带速；

数据块长度=字节数*块因子/记录密度+块间间隔；

读N条记录所需时间T=启停时间+有效时间+间隔时间；

例题：

假设一个有 3 个盘片的硬盘，共有 4 个记录面，转速为 7200 转/分，盘面有效记录区域的外直径为 30cm，内直径为 lOcm，记录位密度为 250位/mm，磁道密度为 8道/mm，每磁道分16个扇区，每扇区 512字节，则该硬盘的非格式化容量和格式化容量约为\_\_(58)\_\_，数据传输率约为\_\_(58)\_\_若一个文件超出一个磁道容量，剩下的部分\_\_(60)\_\_。

<table border="0" cellspacing="1" cellpadding="0" width="94%">
  <tr>
    <td width="25%">
      (58) A.120MB和1OOMB
    </td>
    
    <td width="25%">
      B.30MB和25MB
    </td>
    
    <td width="25%">
      C. 60MB和50MB
    </td>
    
    <td width="25%">
      D.22.5MB 和 25MB
    </td>
  </tr>
  
  <tr>
    <td width="25%">
      (59) A.2356KB/s
    </td>
    
    <td width="25%">
      B.3534KB/s
    </td>
    
    <td width="25%">
      C.7069KB/s
    </td>
    
    <td width="25%">
      D.1178KB/s
    </td>
  </tr>
  
  <tr>
    <td colspan="2" width="50%">
      (60) A.存于同一盘面的其它编号的磁道上
    </td>
    
    <td colspan="2" width="50%">
      B.存于其它盘面的同一编号的磁道上
    </td>
  </tr>
  
  <tr>
    <td colspan="2" width="50%">
      C.存于其它盘面的其它编号的磁道上
    </td>
    
    <td colspan="2" width="50%">
      D.存放位置随机
    </td>
  </tr>
</table>

58：B  59: D  60: B

**RAID****存储器（廉价磁盘冗余阵列）：**基本思想是用多个小的磁盘存储器，通过合理的分布数据，支持多个磁盘同时进行访问，从而改善磁盘存储器的性能。其采用的主要技术：

1．   分块技术：把数据分块写到阵列中的磁盘上；

2．   交叉技术：对分布式的数据采用交叉式进行读写，提高访问速度；

3．   重聚技术：对多个磁盘空间重新编址，数据按照编址后的空间存放；

主要特点如下：

1．   物理上多个磁盘，但操作系统看是一个逻辑磁盘**；**

2．   数据分布在磁盘阵列中的磁盘存储器上；

3．   采用冗余技术和校验技术提高可靠性，可恢复数据；

4．   RAID速度快、容量大、功耗低、价格便宜、容易扩展。

RAID0：无冗余、无校验，具有最高的I/O性能和最高的磁盘空间利用率

RAID1：磁盘镜像、磁盘利用率50%，具有最高的安全性

RAID2：海明码纠错、数据分块、并行访问、适合大批量数据、已很少使用

RAID3：奇偶校验、数据分块、并行访问、单独校验盘

RAID4：奇偶校验、独立存取、单独校验盘、适合访问频繁、传输率低

RAID5：独立存取、无单独校验盘、适合访问频繁、传输率低

**Cache****存储器：（对系统和应用程序员都是透明的）（重点）**

Cache位于主存储器与CPU通用寄存器组之间，全部由硬件来调度，用于提高CPU的数据I/O效率，对程序员和系统程序员都是透明的。Cache容量小但速度快，它在计算机的存储体系中是访问速度最快的层次。

使用Cache改善系统性能的依据是程序的局部性原理，即程序的地址访问流有很强的时序相关性，未来的访问模式与最近已发生的访问模式相似。根据这一局部性原理，把主存储器中访问概率最高的内容存放在Cache中，当CPU需要读取数据时就首先在Cache中查找是否有所需内容，如果有则直接从Cache中读取；若没有再从主存中读取该数据，然后同时送往CPU和Cache。

系统的平均存储周期t<sub>3</sub>与命中率h有很密切的关系，如下的公式：

t<sub>3</sub>=h×t<sub>1</sub>+(1-h)×t<sub>2</sub>

其中，t<sub>1</sub>表示Cache的周期时间，t<sub>2</sub>表示主存的周期时间。

当CPU发出访存请求后，存储器地址先被送到Cache控制器以确定数据是否已在Cache中，若命中则直接对Cache进行访问，否则直接进行主存访问。

Cache的地址映射是指把主存地址空间映射到Cache地址空间，Cache和主存都使用同样大小的块为单位。Cache中常见的映射方法有三种。

Ø         直接映射：一对一,(不需要替换算法)

Ø         全相联映射：多对多

Ø         组相联映射：将块划分成组，主存中的一组与Cache相对应，根据高位地址标志符来访问数据，组相联可以允许相同的Block和word标志，而tag标志不同。

随着程序的执行，访问频繁地区将逐渐迁移，Cache中的内容逐渐变得陈旧，访问命中率下降，就需要更新内容。常用的替换算法有三种。

Ø         随机淘汰法：

Ø         先进先出法FIFO：

Ø         近期最少使用法LRU：

对于这个算法可以从整体上把握，每个的优点、缺点，不需要记算法的过程。

另外，为了保证环存在Cache中得数据与主存中的内容一致，对写操作来说有以下几种方法：

Ø         写直达：同时

Ø         写回：

Ø         标记法

**虚拟存储器：（重点）（对应用程序员透明）**

虚拟存储系统的作用是给程序员一个更大的虚拟的存储空间，其容量可远远超过主存储器的容量，而与辅助存储器容量相当。

我们提供给用户的这个存储器，即在软件编程上可以使用的存储器，就称为虚拟存储器。它的容量即虚拟存储空间，简称虚拟空间。面向虚拟存储器的编程地址称为虚拟地址，或称为逻辑地址。与主存和辅助存储器地址相对应。

为了实现虚拟存储器，需将虚拟存储空间与物理实存空间，按一定的格式分区组织管理，根据管理的方式不同可以分为三种虚拟存储器：页式、段式和段页式。

Ø         页式管理：

Ø         段式管理：

Ø         段页式管理：

此外还可以增加一个小容量的高速存储器实现一种快表查询，而快表和慢表也构成了两级存储器系统

另外，与Cache一样，虚拟存储器系统还需采用一定的调度策略实现主存内容的变换，使当前需要的程序和数据都在主存之中。常用的淘汰算法有：

Ø         FIFO算法：选择最先进入主存的页面淘汰

Ø         LRU算法：选择在最近一段时间内访问频率最低的页面淘汰

**1.4****中央处理器CPU** 

CPU由寄存器组、算术逻辑单元ALU和控制单元CU这3部分组成。

CPU的功能：

Ø         读取指令

Ø         解释指令

Ø         读取数据

Ø         处理数据

Ø         保存数据

1. 寄存器组分为两大类：

Ø         用户可见的寄存器，有通用寄存器、数据寄存器、地址寄存器、标志寄存器等；

Ø         状态寄存器，包括程序计数器PC、指令寄存器IR、存储器地址寄存器MAR、存储器缓冲寄存器MBR、程序状态字PSW。

2.运算器ALU：负责对数据进行算术和逻辑运算。

3.控制器CU：负责控制整个计算机系统的运行，读取指令寄存器、状态控制寄存器以及外部来的控制信号，发布外控制信号控制CPU与存储器、I/O设备进行数据交换；发布内控制信号控制寄存器间的数据交换；控制ALU完成指定的运算功能；管理其他的CPU内部操作。

控制器的实现有硬布线逻辑和微程序控制两种方案

中断控制机制：

计算机系统通常提供了中断机制，允许某一事件中止CPU正在执行的程序，转去对该事件进行处理，然后再返回原程序被中止处继续执行。其作用是提高CPU的处理效率，使CPU与I/O设备并行工作，还可以实现分时操作过程。

中断处理过程可分为：中断响应过程和中断服务过程。

中断的分类：按中断源位置可分为内部中断和外部中断；

按中断源的类型可分为硬件中断和软件中断；

按中断源的屏蔽特性可分为可屏蔽中断和不可屏蔽中断。

CPU处理中断有两种策略：中断排队和中断嵌套。

**计算机的指令系统：**

机器指令的格式、分类及功能:

CPU所完成的操作是由其执行的指令来决定的，这些指令被称为机器指令。

CPU所能执行的所有机器指令的集合称为该CPU的指令系统。

机器指令一般由操作码、源操作数、目的操作数和下一条指令的地址组成。

Ø         操作码指明要执行的操作；

Ø         源操作数是该操作的输入数据；

Ø         目的操作数是该操作的输出数据；

Ø         下一条指令地址通知CPU到该地址去取下一条将执行的指令。

指令系统可分为数据传送类、算术运算类、逻辑类、数据变换类、输入/输出类、系统控制类、控制权转移类等类型。

指令的寻址方式

常用的寻址方式有立即数寻址、直接寻址、间接寻址、寄存器寻址、基址寻址、变址寻址、相对寻址。

指令的执行过程

1.计算下一条要执行的指令的地址；

2.从该地址读取指令；

3.对指令译码以确定其所要实现的功能；

4.计算操作数的地址；

5.从该地址读取操作数；

6.执行操作；

7.保存结果；

**1.5** **输入/****输出系统**

**I/O****系统在CPU、存储器和各种外部设备之间负责协调和控制数据的输入/输出。**

I/O系统控制器基本结构：

n          数据寄存器：

n          状态寄存器：

n          控制寄存器：

n          控制电路：

n          外设接口控制：

I/O系统的工作方式：

Ø         程序控制：CPU完全控制，CPU必须时时查询I/O设备的状态；

Ø         程序中断：I/O设备以中断方式通知CPU，定期查询状态

Ø         DMA方式：CPU只在数据传输前和完成后才介入

I/O系统的发展主要阶段：

Ø         数据通信：CPU直接控制外设；

Ø         程序控制：CPU不关心外设的具体细节，I/O增加了数据交换的功能；

Ø         中断方式：中断机制减少了CPU的等待时间，

Ø         DMA方式：暂停、周期窃取、共享方式

Ø         输入输出通道：专门的处理器控制I/O功能；

Ø         输入输出处理机：不仅拥有处理器，还有本地存储器

根据外部设备和I/O系统交换数据方式，设备接口可分为串行和并行接口。

常见的磁盘设备接口有：总线、DMA、通道、SCSI、并行口、RS232C、USB、IEEE1394

SCSI接口：并行接口；系统级的设备接口

P1394接口：高速串行总线，数据传输率高，价格低容易实现

I/O设备的类型和特性：

键盘：标准101键，主要作为字符、数字和汉字的输入

鼠标：坐标定位部件，有机械式、光电式和混合式三种。

显示器：输出设备，输出图象和字符，性能参数是分辨率和灰度级

打印机：输出设备，分击打式和非击打式打印机

扫描仪：图象输入设备，扫描图象或文本成数字图片，然后输入计算机处理

摄像头：图象输入设备图象数字化后存入到磁盘。

例题：

为了快速传送大量数据，微型计算机中采用存储器直接访问技术，简称DMA。用DMA方式传送时，在存储器和**A**之间直接建立高速传输数据的通路，不需要**B**的干预。利用DMA方式传送数据时，数据的传送过程完全由成为DMA控制器的硬件控制。DMA控制器具有如下功能：

1)        向CPU申请**C**传送。

2)        在CPU允许DMA工作时，处理总线控制的传交。

3)        在DMA期间管理**D**，控制数据传送。

4)        确定数据传送的起始地址和**E** ，并在传送过程中不断修正。

5)        数据传送结束时，给出表示DMA操作完成的信号。

 **A~E****：** ①控制台       ②硬件       ③外部设备       ④数据长度

⑤CPU          ⑥存储器     ⑦DMA            ⑧系统总线

⑨数据方向     ⑩传输速率

**[****分析]**

DMA（Direct Memory Access，直接存储器访问）是一种不需要CPU干预，在存储器和外部设备之间直接通过系统总线高速传输数据的方法。DMA方法使用DMA控制器DMAC来控制和管理数据传输。

**[****答案]**

**A****：**③ **B：**⑤  **C：**⑦ **D：**⑧ **E：**④