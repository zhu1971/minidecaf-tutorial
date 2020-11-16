# MiniDecaf 编译实验

## 实验概述
MiniDecaf [^1] 是一个 C 的子集，去掉了如 include/define/多文件/struct 等特性。
这学期的编译实验要求同学通过多次“思考-实现-重新设计”的过程，一步一步实现从简单到复杂的 Minidecaf 语言的完整编译器，
能够把 MiniDecaf 代码编译到 RISC-V 汇编。
从而能够理解并解决编译真实的程序设计语言时遇到的问题，并能与编译的原理进行对照。

下面是 MiniDecaf 的快速排序，和 C 是一样的
```c
int qsort(int *a, int l, int r) {
    int i = l; int j = r; int p = a[(l+r)/2];
    while (i <= j) {
        while (a[i] < p) i = i + 1;
        while (a[j] > p) j = j - 1;
        if (i > j) break;
        int u = a[i]; a[i] = a[j]; a[j] = u;
        i = i + 1;
        j = j - 1;
    }
    if (i < r) qsort(a, i, r);
    if (j > l) qsort(a, l, j);
    return 0;
}
```

如目录所示，MiniDecaf 实验分为六大阶段，由十二个小步骤组成。
每个步骤，你的任务都是把 MiniDecaf 程序编译到 RISC-V 汇编，并能在QEMU硬件模拟器上运行。
**每步做完以后，你都有一个完整能运行的编译器。**
随着实验一步一步进行，MiniDecaf 语言会从简单变复杂，每步都会增加部分的语言特性。

> * 实验的关键目标是理解和掌握编译器的设计与实现方法，并能与编译原理课程的知识互补与相互印证。
> * 我们提供一系列的参考实现，包含 Python/Rust/Java/C++ 的。
> * 同学遇到困难可以分析了解参考实现、也可以复用他们的代码。不论同学采用那种方式，都希望能达到实验目标。
> * 编译器边边角角的情况很多，所以你的实现只要通过我们的测例就视为正确。


## 实验提交
你需要使用 **git** 对你的实验做版本维护，然后提交到 **git.tsinghua.edu.cn**。
大家在网络学堂提交帐号名后，助教给每个人会建立一个私有的仓库，作业提交到那个仓库即可。
关于 git 使用，大家也可以在网上查找资料。

每次除了实验代码，你还需要提交 **实验报告**，其中包括
* 你的学号姓名
* 简要叙述，为了完成这个 step 你做了哪些工作（即你的实验内容）
* 指导书上的思考题
* 如果你复用借鉴了参考代码或其他资源，请明确写出你借鉴了哪些内容。*并且，即使你声明了代码借鉴，你也需要自己独立认真完成实验。*

**晚交扣分规则** 是：
* 晚交 n 天，则扣除 n/15 的分数，扣完为止。例如，晚交三天，那你得分就要折算 80%。


## 备注
[^1]: 关于名字由来，往年实验叫 Decaf，所以今年就叫 MiniDecaf 了。不过事实上现在的 MiniDecaf 和原来的 Decaf 没有任何关系。

## Reference
- [Writing a C Compiler by Nora Sandler](https://norasandler.com/2017/11/29/Write-a-Compiler.html)
- [An Incremental Approach to Compiler Construction by Abdulaziz Ghuloum](http://scheme2006.cs.uchicago.edu/11-ghuloum.pdf)
