# 3、离散随机变量及其概率分布

在[第2章](second.md)我们介绍了概率的基础知识，最后一节(2.8)特别介绍了随机变量。随机变量是一个函数，它为随机实验的样本空间分配一个具体的数字。

在医院急诊科，前来急诊的病人有时会多，有时会少，是随机变动的。因此我们可以用随机变量来表示某一个时刻急诊科就诊总人数。通过观察，可以分析就诊病人在每一天的分布情况，由此可以分析急诊科的资源配置是否满足要求，在现有配置下不满足要求的风险有多大。这是本章主要的研究内容。

!!!note "学习目标"

    经过仔细学习本章后，可以做到：
    
    1. 从概率质量函数确定概率，或相反从概率确定概率质量函数
    2. 从累积分布函数确定概率，从概率质量函数确定累积概率分布函数，或相反。
    3. 计算离散随机变量的平均值和方差。
    4. 理解某些常用离散概率分布的假设。
    5. 选择适当的离散概率分布，计算特定应用的概率。
    6. 为某些常用的离散概率分布计算概率、确定平均值和方差

## 3.1、离散随机变量
许多系统，比如[第2章]的蒸馏实例，再比半导体生产，甚至于水泥生产、混凝土生产及浇筑等等系统，都可以用相同或相似的随机实验来模拟建模，它们都有相同的抽象模型。人们可以分析这些常见模型的随机变量分布，它们的结果又能用于其它领域的工程实例中。这是人类认识世界的模式，即举一返三的模式。在本章我们要分析少量几个常用常见的随机实验和**离散随机**变量。由于在随机实验这个抽象模型的基础上讨论，所以我们常常可以忽略具体系统底层的样本空间而直接描述特定随机变量的分布。

!!!note "实例3.1"
    商业用语音通讯系统常常包含48条外线。在某一特定时刻，观察系统会发现某些线路正在被使用。设随机变量$X$表示正在使用的线路数量。那么$X$可以是$\{0,1,\cdots,48\}$之间的任何整数。当观察到系统正有10条线路在使用时，则$x=10$。

!!!note "实例3.2"
    混凝土生产强度等级C30的普通混凝土。针对连续生产的180方混凝土，我们取两次样检测其强度。检测结果有*合格*(pass)和*不合格*(fail)两个结果。假定混凝土强度合格的概率为0.95，并且两次抽样是随机独立的。如表3.1显示了随机实验的样本空间和相关的概率。比如，因为独立性，则第一组试件合格第二级试件不合格的概率的随机变量$X$取值为$pf$，它的概率为:

    $$
    P(pf)=0.95(0.05)=0.0475
    $$

    在这个实例中，随机变量$X$被定义为合格试件组数。

!!!note "表3.1、混凝土检测"

    |试件组1|试件组2|概率|$x$|
    |--|--|--|--|
    |pass|pass|0.9025|2|
    |fail|pass|0.0475|1|
    |pass|fail|0.0475|1|
    |fail|fail|0.0025|0|

由实例3.2可知，针对连续生产的混凝土抽取两组试件，只要生产稳定可控，两组试件都不合格的概率是微乎其微的，即使有一组不合格的概率也只有9.5％，应该很少发生。如果生产过程中发生了，表明这是一个强烈的信号，告诉我们生产过程中可能有应该控制的因素未控制好，需要去查找原因解决问题。

## 3.2、概率分布和概率质量函数
随机变量是对随机实验结果的映射函数，可以用来描述非常多系统的随机过程。要用好它，则凸现了其性质的重要性。因此我们在讨论时往往会更关注它的概率分布而忽略它的底层原因。比如在3.1节中的两个实例中，我们常常关注随机变量的在$\{0,1,\cdots,48\}$中的取值。同样地，在实例3.2中，我们也常常关心随机变量在$\{0,1,2\}$上的取值。

随机变量$X$的**概率分布**描述该变量某一特定值的概率。对于本章研究的离散随机变量，分布常常由一个列表组成。该列表列出了每一个随机变量取值所对应的概率。在某些情况下，用一个公式表达这些概率也是很方便的。

!!!note "实例3.3"
    在通过数字转换的过程中有可能会接收到错误的数字位。设$X$等于接下来四个数字位接收到错误位数，可能的值就是$\{0,1,2,3,4\}$。下面的数据给出了依据模型所得到概率。假定如下：

    $$
    \begin{align}
    P(X=0)&=0.6561 &\qquad P(X=1)=0.2916 \nonumber\\
    P(X=2)&=0.0486 &\qquad P(X=3)=0.0036 \nonumber\\
    P(X=4)&=0.0001 \nonumber
    \end{align}
    $$

    $X$的概率分布就是它的每一个取值与对应的概率之间的关系。我们可以用图形来表达这种关系。事实上概率分布就是一种函数，即由随机变量取值与它随机实验时获得该值的概率。图3.1表达了这种关系。

!!!note "图3.1、错误转换数字数的概率分布"
    ![fig.3.1](images/fig3.1.png)

!!!note "概率质量函数"
    离散变量$X$它的可能取值为$\{x_1,x_2,\cdots,x_n\}$的**概率质量函数**(probability mass function)就是函数：

    (1)$\space f(x_i)\geq0$

    (2)$\space \sum_{i=1}^{n}f(x_i)=1$

    (3)$\space f(x_i)=P(X=x_i)$

根据概率质量函数的定义，实例3的各个函数值为$f(0)=0.6561$、$f(1)=0.2916$、$f(2)=0.0486$、$f(3)=0.0036$以及$f(4)=0.0001$。全部相加的各为1。

## 3.3、累积分布函数