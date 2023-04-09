# 第一题
这两个程序的不同之处在于第二个程序在分配内存后使用了 `memset` 来填充内存。这会导致第二个程序消耗更多的内存，因为它在每次分配内存后都会将其全部填充为 1。因此如果在编译过程中，程序 1 分配的内存因为没有使用而被优化，那么会一直进行循环，而程序 2 每次都会占用内存，最终内存分配完就会停止。

# 第二题
## 实现思路

根据命令行输入分析需要的 ls 方式，调用 list_dir 执行其功能。
![image.png](https://s2.loli.net/2023/04/05/SqeCMbfhTy36JNi.png)

这里用到 dirent 库中的目录 entry 结构体判断当前所处的目录位置，从而方便进行递归调用的判断。
![image.png](https://s2.loli.net/2023/04/05/Bax3EdMiqwROUSF.png)

wc 命令主要实现了统计行数的功能，较为简单。

# 实现结果
![QQ图片20230405173823.png](https://s2.loli.net/2023/04/05/4b5UtFOkhiCjnVc.png)

![})QY(ZO5Q_E$GZ_MXX9$3NU.png](https://s2.loli.net/2023/04/05/qapLtvbyU2XEAlg.png)

## 和源码对比
实现的大致思路是相同的，但是源码使用了很多其他的模块中的结构进行编写。以及功能上更加全面，考虑到的操作系统中的问题也更多，因此稳定性肯定更好。接下来从几个具体的方面进行比较：
- 我的程序直接读取命令行，而源码使用 getopt 函数：
![image.png](https://s2.loli.net/2023/04/05/kg7O8eU2jnClhqx.png)

- 我在输出时使用了简单的 printf，但是源码会考虑使用很多种 print 函数：
![image.png](https://s2.loli.net/2023/04/05/Da4cEfmxgQRo8ey.png)
- 实现方式上，源码使用 `traverse` 函数先对目标目录进行遍历，随后将生成的结构（链表）交给 ` display ` 函数进行输出