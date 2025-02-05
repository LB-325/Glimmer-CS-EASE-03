# 浅谈Cache

## 一、冯诺伊曼体系结构与现代计算机组织结构***冯诺伊曼体系结构***：

***（1）冯诺伊曼体系结构***是一种计算机组织架构，由匈牙利数学家约翰·冯·诺伊曼提出。它的核心特点是程序存储概念，即指令和数据都存储在同一内存空间中，且按照顺序执行指令。这种架构包括以下几个主要部分

*1. 中央处理单元（CPU）*：执行指令和处理数据。

*2. 存储器*：统一的存储空间，用于存储程序和数据。

*3. 输入设备*：如键盘、鼠标等，用于输入数据。

*4. 输出设备*：如显示器、打印机等，用于输出结果。

*5. 外部存储*：如硬盘、光盘等，用于长期存储数据。

***（2）现代计算机的组织结构***： 现代计算机的组织结构在冯诺伊曼体系的基础上进行了扩展和优化，以适应更复杂的计算需求。现代计算机通常采用以下结构：

*1. 多核处理器*：集成多个CPU核心，以并行处理任务。

*2. 分层存储系统*：包括快速的缓存（Cache）和主存储器（如DRAM），以及更慢的外部存储（如硬盘）。

*3. 高速输入/输出系统*：支持高速数据传输的接口，如USB、PCIe等。

*4. 操作系统*：管理硬件资源，提供用户界面和应用程序运行环境。

*5. 网络连接*：支持远程数据访问和通信。

***（3）不同点：***

存储结构：冯诺伊曼体系中指令和数据共用同一存储空间，而现代计算机通常采用分层存储结构，指令和数据可以分别存储在不同级别的存储器中。
处理能力：现代计算机采用多核处理器，能够并行处理多个任务，而冯诺伊曼体系中的CPU是单核的，按顺序执行指令。
外部设备和网络：现代计算机强调高速输入/输出和网络连接，而冯诺伊曼体系中这些方面相对较弱。

## 二、主存储器的工作原理

主存储器是计算机中用于存储正在运行的程序和当前使用的数据的存储器。它通常由*动态随机存取存储器*（DRAM）组成，因为DRAM成本较低且集成度高。主存储器的工作原理包括：
***1. 地址解码***：CPU通过地址总线发送内存地址，主存通过地址解码确定要访问的存储单元。//***第一眼看到动态随机存取就想到了malloc函数动态分配内存，查阅了解到malloc函数分配的内存空间就是在DRAM中的***
***2. 数据读写***：通过数据总线，CPU可以读取或写入数据到指定的存储单元。
***3. 刷新机制***：由于DRAM需要定期刷新以保持数据，主存会周期性地刷新存储单元。

## 三、Cache的局部性原理

局部性原理是计算机科学中的一个概念，它指出大多数程序在执行时，对内存的访问倾向于集中在某个较小的区域。局部性原理包括两个方面：
***1. 时间局部性***：如果一个数据项被访问，那么不久后它很可能再次被访问。       *//**联想到了数据结构中的时间复杂度和空间复杂度***
***2. 空间局部性***：如果一个数据项被访问，那么它附近的数据项也很可能被访问。

## 四、Cache如何加快系统整体性能

***1. 减少访问延迟***：Cache位于CPU和主存之间，其访问速度远高于主存，因此当数据存储在Cache中时，CPU可以更快地访问这些数据。
***2. 减少访问次数***：由于局部性原理，程序往往会重复访问相同的数据。Cache可以存储这些频繁访问的数据，减少对主存的访问次数。
***3. 优化数据传输***：Cache通常采用块（block）的方式存储数据，这样可以一次性将多个相关数据加载到Cache中，减少单个数据项的访问延迟。

---

***学习心得与心路历程***
对Cache的学习，让我从以前只关注打游戏相关显卡（GPU），和买电脑关注的CPU和主存，才知道在他们中间还有*Cache*。

在学*Cache*前，我已经接触到了函数递归的知识

[Glimmer-CS-EASE-03/4bde8d7ddad40b3c5d99b31ca4419fdd.jpg at main · LB-325/Glimmer-CS-EASE-03](https://github.com/LB-325/Glimmer-CS-EASE-03/blob/main/4bde8d7ddad40b3c5d99b31ca4419fdd.jpg)

![1729746515485](image/Cache/1729746515485.png)

后面看到*Cache*也是先进后出的Stack方式，突然就想到了学内存管理函数里调用函数时会提前将上一个函数地址以压栈的方式记录，等最后一个函数运行完在以后进先出的方式弹出之前函数地址，就完成了上图中函数调用的返回。查了便验证了我的想法，这种嵌套函数调用有时就是需要将函数地址存于*Cache*中，以先进后出的方式进出栈
