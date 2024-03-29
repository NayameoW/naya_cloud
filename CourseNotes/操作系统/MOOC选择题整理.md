# 1 计算机系统概述
操作系统是对**计算机资源**进行管理的软件
配置了操作系统的机器一台比原来的物理机器功能更强的计算机，这样的计算机只是一台逻辑上的计算机，称为**虚拟计算机**
**Celeron** 不是一个操作系统环境（Solaris/Windows CE/Linux 是操作系统环境）
**实时操作系统**：该操作系统的系统响应时间的重要性超过协同资源的利用率
实时操作系统必须在规定时间内处理来自外部的事件
实时系统必须既要及时响应、快速处理，又要有高可靠性和安全性
分时操作系统：允许在一台主机上**同时连接多个终端**，各个用户可以通过各自的终端交互使用计算机
如果分时系统的时间片一定，那么**用户数越多**，响应时间越长
系统调用是**操作系统向用户程序提供的接口**
用户程序的输入和输出操作实际上由**操作系统**完成
操作系统中，并发性是指**若干个事件在同一时间间隔内发生**
若把操作系统看成计算机资源的管理者，**中断**不属于操作系统所管理的资源
多道程序设计是指**在一台处理机上并发运行多个程序**
**提高处理器资源利用率**的关键技术是多道程序设计技术
操作系统中采用多道程序设计提高 CPU 和外部设备的**利用率**
利用多道程序设计的前提条件之一是系统具有**中断功能**
当计算机提供了管态和目态时，**输入/输出指令**必须在管态下执行
当 CPU 执行操作系统代码时，称处理机处于**管态**
特权指令是指其执行**可能有损系统的安全性**
计算机系统中判断是否有中断事件发生应该在**执行完一条指令后**

# 2 处理器管理
[[2-处理器管理]]
**静态**优先权是在创建进程时确定的，确定之后在整个运行期间不再改变
下列进程状态变化中，**等待->运行变化**是不可能发生的
当**时间片到**时，进程从运行状态变为就绪状态
进程管理中，当**等待的事件发生**，进程从阻塞态变成就绪态
下面对进程的描述中，错误的是**进程是指令的集合**
下面所述步骤中，**由调度程序为进程分配 CPU** 不是创建进程所必需的
多道程序环境下，操作系统分配资源以**进程**为基本单位
下面哪一个选项体现了原语的主要特点：**不可分割性**
关于内核级线程，以下描述不正确的是**控制权从一个线程传送到另一个线程时不需要用户态-内核态-用户态的模式切换**
一个进程被唤醒意味着**进程变为就绪状态**
在引入线程的操作系统中，资源分配的基本单位是**进程**
在下述关于父进程和子进程的叙述中，正确的是**父进程和子进程可以并发执行**
对进程的管理和控制使用**原语**
所谓“可重入”程序是指**能够被多个进程共享的程序**
原语是**不可中断的指令序列**
在进程调度算法中，对短进程不利的是**先来先服务算法**
一个可共享的程序在执行过程中是不能被修改的，这样的程序代码应该是**可重入代码**
在进程管理中，当**时间片用完**时，进程状态从运行态转换到就绪态
Solaris 的多线程的实现方式为**混合式**
在 UNIX 系统中运行以下程序，最多可再产生出**7**进程
```
main ( ){
	fork ( ); /*←pc (程序计数器)，进程 A  
	fork ( );  
	fork ( ); 
}
```

# 3 存储管理
[[3-内存管理]]
静态重定位的时机是**程序装入时**
能够装入内存任何位置的代码程序必须是**可动态连接的**
在可变式分区管理中，采用内存移动技术的目的是**合并空闲区**
在存储管理中，采用覆盖与交换技术的目的是**减少程序占用的内存空间**
在分区存储管理中，下面的**首次适应法**最有可能使得高地址空间变为大的空闲区
以下**页式**存储管理能提供虚存
在分页式虚存中，分页由**操作系统**实现
在虚拟页式存储管理方案中，下面**缺页中断处理**完成将页面调入内存的工作
采用**分段式存储管理**不会产生内存碎片
采用**分页式存储管理**不会产生外部碎片
一台机器有 48 位虚地址和 32 位物理地址，若页长位 8KB，如果设计一个反置页表，则**有 $2^{19}$ 个页表项**
作业在执行中发生了缺页中断，经操作系统处理后，应该让其执行**被中断的后一条**指令
在请求分页存储管理中，当访问的页面不存在内存时，便产生缺页中断，缺页中断是属于 **I/O 中断**
通常所说的“存储保护”的基本含义是**防止程序间相互越界访问**
LRU 置换算法所基于的思想是**在最近的过去很久未使用的在最近的将来也不会使用**
在下面关于虚拟存储器的叙述中，正确的是**要求程序运行前不必全部装入内存且在运行过程中不必一直驻留在内存**
虚存的可行性基础是**程序执行的局部性**
把逻辑地址转变为内存的物理地址的过程称作**编译**
在段页式存储管理系统中其内存地址空间是**三维**的
页面替换算法 **FIFO** 有可能会产生 Belady 异常现象
> Belady 异常：增加 page frame 的数量，反而增加了缺页错误

# 4 设备管理
按**信息交换单位**分类可将设备分为块设备和字符设备
CPU 输出数据的速度远远高于打印机的打印速度，为了解决这一矛盾，可采用**缓冲技术**
硬件和软件的功能扩充，把原来独占的设备改造成能为若干用户共享的设备，这种设备称为**虚拟设备**
通道又称 I/O 处理机，它用于实现**内存与外设**之间的信息传输
为了使多个进程能有效地同时处理输入和输出，最好使用**缓冲池**结构的缓冲技术
如果 I/O 设备与存储设备进行数据交换不经过 CPU 来完成，这种数据交换方式是 **DMA 方式**
在中断处理中，输入/输出中断可能是指设备出错、数据传输结束
在采用 SPOOLing 技术的系统中，用户的打印结果首先被送到**磁盘固定区域**
大多数低速设备都属于**独享**设备
**磁盘**是直接存取的存储设备
操作系统中的 SPOOLing 技术，实质是指**块设备**转化为共享设备的技术
在操作系统中，用户程序申请使用 I/O 设备时，通常采用**逻辑设备名**
采用假脱机技术，将磁盘的一部分作为公共缓冲区以代替打印机，用户对打印机的操作实际上是对磁盘的存储操作，用以替代打印机的部分是**虚拟设备**
**先来先服务**算法是设备分配常用的一种算法
将系统中的每一台设备按某种原则进行统一的编号，这些编号作为区分硬件和识别设备的代号，该编号被称为该设备的**绝对号**
通道程序是**由一系列通道指令组成**
I/O 软件的分层结构中，**设备驱动程序**负责将把用户提交的逻辑 I/O 请求转化为物理 I/O 操作的启动和执行
使用 SPOOLing 系统的目的是为了提高 **I/O 设备**的使用效率
下列算法中，用于磁盘移臂调度的是**最短寻找时间优先算法**


# 5 文件管理
Unix 系统中，文件的索引结构存放在 **inode 节点**中
操作系统中对文件进行管理的部分叫做**文件系统**
为了解决不同用户文件的命名冲突问题，通常在文件系统中采用**多级目录**
无结构文件的含义是**流式文件**
下列文件中不属于物理文件的是**记录式文件**
文件系统的主要目的是**实现对文件的按名存取**
下列文件中属于逻辑结构的文件是**流式文件**
文件系统采用多级目录结构后，对于不同用户的文件，其文件名**可以相同也可以不同**
文件目录的主要作用是**按名存取**
在文件系统中，文件的不同物理结构有不同的优缺点。在下列文件的物理结构中，**索引结构**具有直接读写文件任意一个记录的能力，又提高了文件存储空间的利用率。
文件系统用**目录**组织文件
文件路径名是指**从根目录到文件所经历的路径中的各符号名的集合**
一个文件的相对路径名是从**当前目录**开始，逐步沿着各级子目录追溯，最后到指定文件的整个通路上所有子目录名组成的一个字符串
对一个文件的访问，常由**用户访问权限和文件属性**共同限制
存放在磁盘上的文件**即可随机访问，又可顺序访问**
在文件系统中，位示图可用于**磁盘空间的管理**
常用的文件存取方法由两种：顺序存取和**随机**存取
Unix 系统中，通过**目录项**实现文件系统的按名存取功能。
Unix 文件系统中，打开文件的系统调用 open 输入参数包含**文件名**
Unix 文件系统中，打开文件的系统调用 open 返回值是**文件描述符（字）**

# 6 并发程序设计
对于两个并发进程，设互斥信号量为 mutex，若 mutex=0, 则**表示有一个进程进入临界区**
用 V 操作唤醒一个等待进程时，被唤醒进程的状态变为**就绪**
P 操作、V 操作是进程同步、互斥的**原语**
若信号量 S 的初值为 3，当前值为 -2，则表示有 2 个等待进程
设有 n 个进程共用一个相同的程序段（临界区），如果每次最多允许 m 个进程 (m<n) 同时进入临界区。则信号量的初值为 m
在操作系统中，临界区指**一段程序**
关于进程间通信，信箱通信是一种**间接**通信方式
在一段时间内，只允许一个进程访问的资源称为**临界资源**
一个进程在获得资源后，只能在使用完资源后由自己释放，这属于死锁必要条件的**不可剥夺条件**
系统出现死锁的原因是**若干个进程因竞争资源无休止地循环等待，且都不释放已占有的资源**
在系统提供的可共享的资源不足时，会出现死锁，不适当的**进程的推进顺序**也可能产生死锁
某系统中有 3 个并发进程，都需要同类资源 4 个，该系统不会发生死锁的最小资源数是 10 个
死锁定理是用于处理死锁的**检测死锁**方法
死锁检测时检查的是**资源分配图**
进程资源静态分配方式是指一个进程在建立时就分配了它需要的全部资源，只有该进程所要资源都得到满足的条件下，进程才开始运行。这样可以预防进程死锁。静态分配方式破坏死锁的**占有且等待**必要条件
银行家算法通过**破坏循环等待条件**来避免死锁
某系统中有 11 台打印机，N 个进程共享打印机资源，每个进程要求 3 台，当 N 不超过 5时，系统不会死锁
若有 4 个进程共享同一程序段，每次允许 3 个进程进入该程序段，用 P、V 操作作为同步机制，则信号量 S 的取值范围是 3, 2, 1, 0,-1
采用资源剥夺法可以解除死锁，还可以采用**撤销进程**方法解除死锁
资源的按序分配策略可以破坏**循环等待资源**条件

