- [一、三种结构](#一三种结构)
  - [1.1 顺序结构](#11-顺序结构)
  - [1.2 选择结构](#12-选择结构)
  - [1.3 循环结构](#13-循环结构)
    - [1.3.1 while 循环](#131-while-循环)
    - [1.3.2 do...while](#132-dowhile)
    - [1.3.3 for 循环](#133-for-循环)
- [二、三步走战略](#二三步走战略)
  - [2.1 第一步](#21-第一步)
  - [2.2 第二步](#22-第二步)
- [三、编程实践](#三编程实践)
  - [3.1 一个数分解为其质因子之积的形式](#31-一个数分解为其质因子之积的形式)
  - [3.2 用 C 语言代码实现菱形图案](#32-用-c-语言代码实现菱形图案)
  - [3.3 用定积分极限定义计算 0 到 180 度之间，sin(x) 与横轴所围成的面积](#33-用定积分极限定义计算-0-到-180-度之间sinx-与横轴所围成的面积)
- [四、强调几点](#四强调几点)
- [五、说明](#五说明)

连着写了好几篇的非技术文章了，今天写写技术文章，两者穿插着写，**三步走战略、五大能力体系、思维、打法**，在每一篇文章中都会体现，重在思考、理解，C 语言真的值得每一个程序员去学学，重在编程思想与编程哲学。

不是我技术文章更新较慢，而是一些能力、思维的提升比较重要，这种是大的战略方向，意识必须给到位，而且关于这方面还有许多要写的。

## 一、三种结构

**用工程化思想，指导程序设计的过程。**

- 很重要的一个思想：**模块化；**
- 模块化程序的特点：**单入口、单出口；**

模块与模块之间的三种关系（必须非常熟练的掌握、理解）：顺序结构、分支结构（选择结构）、循环结构，这三种结构基本上构成了模块的框架。

### 1.1 顺序结构

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_jpg/iaumSdLKJXtSCialDqcncib9nPFgPh6RsGDNsgB2owJbfiboxzFfyDZE8UgOYdBXCgVuzE26ho7b9cu4lBELr7dznQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(顺序结构)</p>

从上往下执行每一条代码，机器严格的按照指令走，没有选择、没有循环，是最简单的结构。

### 1.2 选择结构

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_jpg/iaumSdLKJXtSCialDqcncib9nPFgPh6RsGDUB4qbRqsqEQKRacGg8TS4aRJ5Ild2w7y5d2HAXGnl2UjoWSBcbeQPA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(选择结构)</p>

```c
if(条件表达式)
    语句 1 
else
    语句 2

if(条件表达式)
    语句 1

if ... else ...   或者 if ... 语句，也是必须掌握的，很简单的。
```

**注意：**

- if 后面的 ()，坚决不能丢；
- if 和 else，只控制其后的一条语句；若需要控制多条语句，则必须用 {} 将这些语句括起来，称为一条 “复合语句”。

### 1.3 循环结构

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_jpg/iaumSdLKJXtSCialDqcncib9nPFgPh6RsGDlNmX13ichMSuELiamzWxibdsQIcye5ZKTX0E7Oe44enAWoQKHzoJqhVYQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(循环结构)</p>

#### 1.3.1 while 循环

```c
while(条件表达式){
    循环体;
    步长;
}

循环体最少执行 0 次，最多执行无数次。
```

#### 1.3.2 do...while

```c
do 
    循环体;
while(条表);  

do ... while... 这个循环一般不使用。
```

#### 1.3.3 for 循环

```c
for(初值; 条表; 步长){
    循环体;
}
```

while、for 循环用的比较多，三要素：**初值、条件、步长**，必须明确。

这三种结构，只要掌握了 C 的，对于其他语言都是类似的，**一定要以技术的深度为主，熟练的掌握一门，编程思想到位了，其他都不是问题，再将技术进行横向的扩展，由易入难，由深入广的打法。**

一个核心观点：我们写的程序，通过指令，转换为机器能识别的是 0 和 1，机器是严格的按照指令执行，最终实现我们预期的任务。

## 二、三步走战略

### 2.1 第一步

当我们面对一个编程问题，不要急于动手去敲，三步走：**输入 + 处理 + 输出；**

输入是什么？中间怎么处理？最终的输出结果又是什么？

想清楚了，再动手去实现，那就很简单了。

### 2.2 第二步

三步走：**分而治之  + 变量跟踪 + 换位思考；**

**分而治之**：问题再大，也要学会需求拆解，细化，能否把问题拆的足够好，充分的反映了一个人编程经验以及技术能力。

**变量跟踪**：在编写程序到某一模块，必须把自己当成机器，去一步一步的追踪各个变量的值的变化过程，从而得出程序的功能！查找程序错误也是这样做的。

**换位思考**：在编程的过程中，需要不停的在 “开发者” 和 “程序的使用者(用户)”之间的角色转换，以决定程序的编写方式。

**明确了三步走的打法，以及编程前的准备，再动手去敲，去思考，养成良好的编程习惯是受益终生的，这种思维不仅仅在编程、在其他领域都是受益的，因为能力的提升才是你的资本。**

**要学的是怎么思考，怎么分析，怎么去实现，把这些能力提升起来。**

## 三、编程实践

**说的再多，分析的再清楚，你不去一行一行、一个字母一个字母敲出来，是不起任何作用的**，我当年初学编程的时候，是一个字母一个字母的敲，没用什么代码补全工具，这个很锻炼我的编码能力与代码的认知感觉。

**动手追踪：对于要实现的相关程序，必须自己动手，通过手工实现一些例子；再手工实现的过程中，去寻找、概况、总结在这过程中的一般性规律，而程序就是对这个规律的精准描述。**

**动手追踪的能力一定要培养起来，要勤快起来，不能偷懒的光看，脑子要多想，多动手画、敲。**

下面通过代码实现三个 C 语言的例子，加深学习和理解。

### 3.1 一个数分解为其质因子之积的形式

手工的在纸上画一下，怎么分解，找出规律，用代码实现即可。

```c
#include<stdio.h>

void main(void)
{
    int num;
    int i;
    int n;

    printf("请输入一个数：");
    scanf("%d", &num);
    n = num;

    printf("%d = ", num);
    for(i = 2; n > 1;)
      if(n%i == 0)
      {
        printf("%d", i);
        if(n != i)
          printf("*");
        n /= i;
      }
      else
        i++;

    printf("\n");
}
```

运行结果：

- gcc test.c -o test
- ./test

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_jpg/iaumSdLKJXtSCialDqcncib9nPFgPh6RsGDdnU5dyPk0AyujuFX7ic3kLdeKJ5SzmBc46x40uQ6zJwCx0aQfk8HuUg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(运行结果)</p>

### 3.2 用 C 语言代码实现菱形图案

要观察这些星星的个数是怎么变化的，用笔在纸上画，找出规律。

```c
#include<stdio.h>
#include<math.h>
 
void main(void)
{
    int n, i, j;
 
    printf("请输入行数（奇数）:"); //因为是菱形，所以必须为奇数行
    scanf("%d", &n);

    for(i = 0; i < n; i++)
    {
      for(j = 0; j < abs(n/2 - i); j++)
        printf(" ");
      for(j = 0; j < 2 * (n/2 - abs(n/2 -i)) + 1; j++)
        printf("*");
      printf("\n");
    }

    printf("\n"); 
}
```

运行结果：

- gcc test.c -o test
- ./test

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_jpg/iaumSdLKJXtSCialDqcncib9nPFgPh6RsGD1EZSozAibgseJLOzM6pfoxvCpc7T3HVLcEfIE4tagIbRtnRMVuTHwvw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(运行结果)</p>

### 3.3 用定积分极限定义计算 0 到 180 度之间，sin(x) 与横轴所围成的面积

分析：很多人咋一看，很难啊，没思路，实现不了，你先自己想想，看看能不能用代码实现这个问题。

其实，这个特别简单，C 语言入门级别，会点高数求极限，知道这个公式就可以了，遇到问题，认真的分析分析，这些都是最简单、最基础的，下面的图很清晰的表示了。

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_jpg/iaumSdLKJXtSCialDqcncib9nPFgPh6RsGDn6rBV1xO8etqEXMy0vZwWKMerdOjicakqs1eT5gpMLBrZAiamOhqBGhA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(sin图形)</p>

```c
#include<stdio.h>
#include<math.h>
 
void main(void)
{
    double x, dx, s = 0;
 
    printf("请输入Δx:");
    scanf("%lf", &dx);

    for(x = 0; x <= 3.1415926; x += dx) //这块的3.1415926可以使用宏定义define
      s += sin(x) * dx;

    printf("面积是：%lf\n", s);
}
```

运行结果：

- gcc test.c -o test
- ./test

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_jpg/iaumSdLKJXtSCialDqcncib9nPFgPh6RsGDNvC2iaIU2N6FTzjUJu1ickekicUwgwVicmrukWoUDsGe7pJaYYSjZWcw9A/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(运行结果)</p>

**学过高数的应该都懂，dx越小，求的极限越接近于真实面积，而极限本身就是这些小面积的求和，大学阶段：高数、概率论、线性代数、离散数学极为重要，对于搞算法的我们来说，非线性拟合问题，拟合函数，低阶高阶特征组合，各参数梯度计算，各个参数求偏导、等都是必备的，没有扎实的数学功底，如何能成为一个优秀的程序员呢？**

## 四、强调几点

<font color=green size=5>*1、*</font>

今天，我的 C 之旅已经分享到了三种结构，基本语法差不多了，算是 C 语言最简单的地方，接下来是 C 的三大重点：数组 + 指针 + 函数。

**前面的基础部分，还需要你仔细、认真的通过看视频 + 看书 + 敲代码，巩固起来（其中的细节很多），不会就多看几遍，我建议初学者多看视频，多动手，C 的视频我前面文章分享过了，就是 b 站那个郝斌讲的。**

<font color=green size=5>*2、*</font>

通过我上面举的几个例子，发现没有，**其实编程就是自己通过在纸上认真的画，认真的去想，认真的去追踪，一定要花大量时间，能沉得住气，找一般性规律，尤其初学者，一定要坚持，一定要花大量时间，这个得靠自己理解，自己想清楚。**

前面提到的三步走：你自己再通过实践去理解，去悟，看出门道，最终就是通过代码实现即可。

**对需求的理解，对数学的掌握以及算法，都是特别的重要，思想、能力、习惯的培养至关重要，一定要找到适合自己的学习方式、方法。**

**上面我的打法，思考，其实真的在任何行业，任何领域都适用，看似在编程，其实在人生，这就是能力，这就是大格局，人生需要布局，需要大的战略，冲破现状，真正的成长起来。**

**三步走战略的打法，以及五大能力体系的构建，是内功，需要时间，需要勤加练习，是我选择的道路，目前仍在摸索的路上。。。**

<font color=green size=5>*3、*</font>

昨天有一个读者给我发了一条微信消息，说我的文章对他的帮助很大，他把我的文章，都打印出来，认真的在专研我的一些思想，和我想表达的一些观点，认真的在悟，我真的是很吃惊，没想到自己的经历还是帮助到了一些人。

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtSCialDqcncib9nPFgPh6RsGD4aVemOIdaMMbshtcdHWiaiaRic15mUHuxOzpibdu3NXJA4b3E61WH4WeCA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(打印的公众号文章)</p>

其实以前就有人给我说，把我的文章保存了 pdf 文档，还有的在认真的做笔记，我其实是很开心的能帮到各位。

遇到问题，遇到需求，不知道如何下手的，没有思路的，这篇文章希望给你带来一点帮助与提升，真的是需要打法与战略的，再通过实践，长时间的积累，去提升自己。

**优秀的人总是在寻找迄今未开拓的地区！！！**

## 五、说明

原创文章链接：[C 语言程序设计-->结构化程序设计](https://mp.weixin.qq.com/s?__biz=MzU4MjQ3NzEyNA==&mid=2247483914&idx=1&sn=472deb568d0dba5cfc2a77771d05c36d&chksm=fdb6f621cac17f37cbd999ca3a505ef406791965876dcb4edb1975c703e69bdaa4186100f77f&token=1250675081&lang=zh_CN#rd)
