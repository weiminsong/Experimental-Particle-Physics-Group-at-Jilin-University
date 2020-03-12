



##        Introduction



[TOC]

​																	

#### Chapter one.  Requirement

##### 1. Softwares

[CEPCsoft](http://cepcsoft.ihep.ac.cn/) 

[WHIZARD](https://whizard.hepforge.org/) ：Monte Carlo

[ROOT](https://root.cern/doc/v618/) 



##### 2. Websites

[高能所计算环境使用手册](http://afsapply.ihep.ac.cn/quick/) ：Some disk locations, AFS account management

[CEPC WEB](http://cepc.ihep.ac.cn/) : website of CEPC

[Indico-CEPC](https://indico.ihep.ac.cn/category/211/) ：you can find some documents here

[2020 BESIII Winter School in Changchun](https://indico.ihep.ac.cn/event/11031/other-view?view=standard) ：resources of BES3, whose general analytical frameworks are similar to CEPC.

[THCondor](http://afsapply.ihep.ac.cn/cchelp/zh/local-cluster/jobs/HTCondor/) : Job submission







#### Chapter Two. Event Generation

##### 1. Theoretical Analysis

###### 1) channals

Decay channel analysis is the most important step in the whole process. You need to get all the possible decay channels and draw feynman diagram. Provide a source for the background analysis below.

###### 2)...









##### 2. Generator

###### 1) WHIZARD



**Detailed information is in [whizard_manual](https://github.com/weiminsong/Experimental-Particle-Physics-Group-at-Jilin-University/CEPC/Useful%20files/whizard.pdf).**

NOTES : Version 2.X is recommended.



Here's how to run whizard 2.6 in an IHEP server:



Download and set environment :

```shell
> cd /workfs/bes/$USER/
> cp /afs/ihep.ac.cn/users/l/liaoyp/besfs/load_* ./    # copy env files

> source load_cepcsoft.sh
> source load_whizard.sh
```



Then you can execute "whizard".

For example:

```shell
> mkdir HelloWorld
> cd HelloWorld

> touch hello.sin      # whizard can run .sin(SINDARIN) file
> vim hello.sin

printf "hello world!"

> whizard -r hello.sin 
# Then you can see a banner and "hello world!"

# Also, you can write a simple file named ee.sin

process ee = e1,E1 => b,B
sqrts = 240 GeV
n_events = 10
sample_format = lhef
simulate (ee)

# Execute whizard and it will take you several minetes.
# The final result is the desired event file, ee.lhe.

```





###### 2) Detector simulation

Generate information of momentum from the generator and pass it on to the detector.







##### 3. Cases selection

We can select cases by using the momentum distribution, the invariable mass of B meson and lepton and the number of particles contained.

By using the case selection function, a part of the cases can be roughly filtered.





#### Chapter Three. Pre-filtering

General steps of pre-screening (Libo Liao, Hangzhou normal university, 2017) :



1. Firstly, some considerable measurement distributions of signal and background are obtained through the real information of monte carlo, and find differences between signal and background distribution. The measurement of observable information must be able to reflect the overall information of the case.

2. Filter the signals by significant difference in the observable measurement distribution.

3. After filter of the data of monte carlo, it is necessary to check the result after reconstruction.





In pre-filtering, the inv mass of e,e- is reduced to a specific interval (in the NU, c=hbar=1 to simplify the calculation, so that the dimensions of energy, momentum and mass are the same) to increase the proportion of the signal case and cut background case.





#### Chapter Four. Background Analysis

Several common background deduction methods:

- mass selection

  The number of remaining particles is used for selection. In this process, 3-n (whose specific values have not been analyzed) remaining final state particles are selected.

- observe Jet

  By observing the constant mass peak of jet, speculate that an example of jet may be formed. Taking b quark jet as an example, the data of existing b quark jet was compared with the data, and the similar value b-tag was used for selection.

- secondary vertex

  For long-lived particles, because they don't decay quickly. So it's going to keep moving and it's going to create a subpeak, a secondary vertex. By looking at the secondary vertices, you can subtract some of the background.

- momentum filtering

  It can be deducted by using the small or large transverse momentum of some particles.



#### Chapter Five. Signal Selection

After the background deduction, the number of signal cases is reduced step by step, and finally we get the signal cases of the decay channel we need.





#### Chapter Six. Calculation of Branch ratio

1. The equation of Branch ratio：

$$
\begin{equation}
\mathrm{BR}\left(\mathrm{B}_{\mathrm{s}}^{0} \rightarrow \mu^{+}+\mu^{-}\right)=\frac{N_{s i g}}{N_{t o t} \cdot \varepsilon}
\end{equation}
$$







#### Chapter Seven. Analysis