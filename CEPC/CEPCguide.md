



##        一些入门级操作介绍



[TOC]



![图片1](C:\Users\Ann\Desktop\图片2.png)

​																	**分析的总流程图**



#### 一.  准备工作(Requirement)

##### 1. 各项软件位置

[CEPCsoft](http://cepcsoft.ihep.ac.cn/) ：整个的分析过程和例子都有

[WHIZARD](https://whizard.hepforge.org/) ：用来做蒙卡模拟的软件

[ROOT](https://root.cern/doc/v618/) ：ROOT文件工具



##### 2. 各个资源网站

[高能所计算环境使用手册](http://afsapply.ihep.ac.cn/quick/) ：一些磁盘位置，AFS账号管理

[CEPC WEB](http://cepc.ihep.ac.cn/) : CEPC官网

[Indico-CEPC](https://indico.ihep.ac.cn/category/211/) ：可以找到一些会议资料以及有用文件

[2020 BESIII Winter School in Changchun](https://indico.ihep.ac.cn/event/11031/other-view?view=standard) ：BES3的学习资料，一些大致分析框架与CEPC类似









#### 二. 事例产生(Event Generation)

##### 1. 理论分析

###### 1) 衰变道分析

衰变道分析是整个过程最重要的一步。需要得到所有可能的衰变道，并大致绘制出费曼图。为下面的本底分析		提供来源。

###### 2)...









##### 2. 产生子模拟(Generator)

###### 1) whizard输入



**详细步骤在[whizard_manual](https://whizard.hepforge.org/manual_whizard_1.pdf)中有详细介绍**





下面是在IHEP服务器中运行whizard的详细过程：



**下载WHIZARD：**

```shell
> cd /workfs/bes/$USER/ #进入一个工作目录，专门用来分析。因为中间我们需要下载一些软件，所以注意内存

> mkdir WHIZARD
> cd WHIZARD

> cp /cefs/data/stdhep/generator/downloads/whizard-1.95.tgz ./ #复制WHIZARD-1.95版本

> tar xzf whizard-1.95.tgz
```



**配置环境以及编译：**

```shell
> cd /workfs/bes/$USER/WHIZARD/
> ./configure	#配置主体环境
```



**选择输入文件：**

```shell
> cd conf	#我们主要讲所选取的事例文件放在这里面，具体查看manual

> cp -i whizard.prc.default whizard.prc  #如果你是第一次配置，那么你需要自己复制一个prc文件。此处我们复制已有的初始prc文件，并且改名为whizard.prc。

> vim whizard.prc	#修改输入的prc文件，具体操作见manual

#同理，我们对whizard.in进行操作
> cp -i whizard.in.default whizard.in
> vim whizard.in

#我们可以对whizard中的prc,in,cut1和mdl等等文件进行操作，根据我们的要求进行改变
```



**编译并运行whizard：** *<u>（首次运行）</u>*

```shell
#进入whizard的主目录
> cd /workfs/bes/$USER/WHIZARD/

> ./configure	#再次配置环境

> make install	#编译刚刚编辑whizard输入文件

#此时，我们可以进入results目录，会发现里面有我们在conf目录复制过来的prc和in文件。
> cd results
> ls
Makefile	Makefile.in		whizard.in		whizard.prc		whizard.mdl		whizard
#可能有cut1和cut5，但都是空的

> ./whizard		#运行whizard可执行文件，可产生一个out文件，及我们所要的产生子的模拟文件
> vim whizard.out

#此过程仅为首次运行，修改prc和in文件后重新编译过程如下面代码所示
#中间可能会出现错误，具体解决方案欢迎交流讨论，或者参见manual
```



**重新编译：**

```shell
#进行过程文件清理
> cd /workfs/bes/$USER/WHIZARD/

> make proclean		#remove the process-dependent files

> make realclean	
#do a thorough cleanup, and it will also remove the ComHEP and MadGraph executables used for generating matrix elements, recovering the state just after configuration.

> make distclean
#remove also the files resulting from configuration,and all files you have made before: whizard.prc and whizard.in
#After execute this command, you have to run configure before any further make command can be executed.

#注意：根据你的需要，选择进行上述清理代码，否则你的文件将全部清理！在清理前注意备份必要文件。
```





###### 2) 探测器模拟

用产生子产生一些四动量信息，然后传递到探测器里







##### 3. 事例选择

利用初末态例子的动量分布、B和轻子不动质量和事例所含粒子数等，选择信号事例。

利用事例选择函数，可以大致筛选一部分事例。







#### 三. 预筛选(Pre-filtering)

预筛选大致步骤（杭州师范大学廖立波 2017）：

1. 首先，通过蒙卡的真实信息得到信号与本底的一些可观测量分布，并寻找信号与本底分布的差别。其中可观测量必须能够体现事例的整体信息。
2. 通过显著差异的可观测量分布进行筛选。
3. 做完蒙卡真实信息的筛选之后，还需要在重建之后对筛选完的事例进行检验。

 

在预筛选时，缩小ee-的不变质量为一个特定区间（在自然单位制下，c=hbar=1，以简化数值运算，因此能量、动量和质量量纲相同），以提高信号事例所占比例。





#### 四. 本底分析

几种常用的本底扣除方法：

- 质量筛选

  利用剩余粒子数进行筛选，如此过程选择3-n（具体数值还未分析）个剩余末态粒子。



- 观察喷注

  利用喷注的不变质量峰进行观察，推测可能形成喷注的例子。以b夸克喷注为例，利用现有真实b夸克喷注与数据进行对比，利用相似值B-tag进行筛选。



- 次级顶点

  对于寿命较长的粒子，由于不会迅速衰变。因此会继续移动导致产生次峰，即次级顶点。通过观察次级顶点，可以扣除一部分本底。



- 动量筛选

  利用一些粒子的横向动量较小或较大，可以进行扣除。







#### 五. 信号抽取

经过本底扣除，信号事例数被一步步减少，最后得到我们所需要衰变道的信号事例。







#### 六. 分支比计算

1. 分支比公式如下：

$$
\begin{equation}
\mathrm{BR}\left(\mathrm{B}_{\mathrm{s}}^{0} \rightarrow \mu^{+}+\mu^{-}\right)=\frac{N_{s i g}}{N_{t o t} \cdot \varepsilon}
\end{equation}
$$







#### 七. 误差分析