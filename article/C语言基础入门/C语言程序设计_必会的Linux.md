- [一、重要的 Linux](#一重要的-linux)
- [二、Linux C](#二linux-c)
- [三、说明](#三说明)

C 语言的学习，我前面写的都是一些基础的语法知识，但是又是 C 语言中相当重要的部分，**我只是把核心的知识点，精简的总结了出来，你们还得结合书、视频，去学习其中细节、去实践，只有这样，才能真正的理解消化、吸收。**

其实 C 的学习，可以使用 Win Linux Mac 等多平台，由于我本人工作是公司配发的 Mac，为了方便我的书写，我之后打算用的是 Linux 平台下的 gcc 来进行 C 程序的编译、链接、执行。

## 一、重要的 Linux

对于 Linux，我是强烈建议大家必须的会，这个是一个硬性要求技术，你说不会 Linux，真的来公司，你就知道多悲催了，**不管什么方向，只要是 IT 行业，跟编程有一点点关系的，Linux 一定一定的非常熟练。**

我在校期间，当年特别喜欢折腾 Linux，各种版本都用过，因为我是在实验室，我个人笔记本装的是虚拟机，用的是 VM（**我 VM 可是 8 系统，见下图**）我在实验室的台式机是三系统，win xp、win 7 和ubuntu，对我来说，当年在校大把的时间，都去专研这些了。

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_jpg/iaumSdLKJXtRSKj6ZXO4zVjicIicxau9sr7VCm1915dsoJKPouh0W9lUBkDyxn7iaiaqSZcHAdVJADYavXC06UBAicAA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(VM安装的Linux虚拟机)</p>

根据我的个人经验，我觉得大部分人日常还要使用 Win，Mac 又太贵，**我是建议大家用 VM 安装虚拟机，去 ubuntu 官网下载镜像即可**，运维方向的建议直接搞个 Linux 系统，至于环境安装，软件需求这些，有问题的私聊我。

今天，我不是写 Linux 系列的，不会说太多 Linux 方面的知识，主要给大家分享一下怎么用 Linux 写 C 程序 和 在 Linux 下面得到程序的结果。

## 二、Linux C

在 Linux 下面进行编程，基本上都是黑框框，命令行模式的，但是其执行的效率是非常高的，我已经好久没用过 Win了，并且我日常的开发都是在 Mac 系统下面，用 Vim 和 PyCharm 写程序，今天，要写的是 C 程序，我建议大家直接用 Vim 就好，给出三步走学习方向。

1. 对于 Linux 常见的命令学习，这些细节性的东西，买本 <Linux 鸟哥私房菜>，去掌握一些要用到的命令：ls、cd、mkdir、mv、rm、chmod、find、grep 等，了解一下Linux 的日常使用；

2. 对于在 Vim 下写程序，可以在 ~/.vimrc 里面配置各种语法高亮、自动对齐、显示行数等各种，非常的方便，在熟悉 Vim 的常见使用快捷方式，就可以在 Vim 中写 C 程序了，Vim 真的是很高效的文本编辑器，是我最喜欢的之一；

3. 写好了 C 程序，就可以执行了：
   1. gcc first.c -o first（first.c 是程序的文件名称，first 是最终可执行文件的名称）；
   2. chmod 777 first（在命令行改一下权限）；
   3. ./first（就可以看到结果了）；

上面的三步，我觉得大家百度或者 google 去找找，资料一大堆，写的都很细，花一周时间，快速的学习这些基础，然后就可以用 Linux 下面的 Vim 写程序，编译执行了，超级爽。

对于这三步走战略，可以结合视频、书籍去学习，其中必将有太多的细节需要自己去专研，有什么问题，都可以私聊我。

## 三、说明

原创文章链接：[C 语言程序设计-->必会的 Linux](https://mp.weixin.qq.com/s?__biz=MzU4MjQ3NzEyNA==&mid=2247483838&idx=1&sn=456eabd301bfb7f57204ebc59f9a94a5&chksm=fdb6f595cac17c839100f8f0e141eebe9a32c897bce92fe46ef4724418a6eaa11da7c7b989fc&token=1250675081&lang=zh_CN#rd)
