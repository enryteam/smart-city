- [Apollo自动驾驶进阶课（7）——Apollo控制技术_Oceans_depth的博客-CSDN博客_apollo 速度控制](https://blog.csdn.net/qq_45577461/article/details/107943151)

控制模块的输入来自：**规划模块**和**反馈阶段信息**（如localization和HD Map），此部分信息包括车辆位置、朝向、速度等。

[Apollo](https://so.csdn.net/so/search?q=Apollo&spm=1001.2101.3001.7020)软件框架的输出结果是控制指令，与下层模块canbus（车辆交互标准）进行交互；同时控制模块也会从底层车辆得到反馈信号（车辆本身in vehicle reference frame：速度信息、四轮转速信息、车辆健康状况信息、底盘是否报错信息、危险信息）![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817122539748.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

## 1.控制概览

控制模块包括三个部分：

- **预处理**，主要功能包括三方面：
  第一是对输入信号的检查，对不正常信号的过滤；
  第二是做一些紧急处理；
  第三是做一些滤波操作，例如信号的平滑等。
- **控制器**，主要功能包括：模型建立、系统识别和分析，控制器/观察器设计以及参数调优等功能，如图3所示。
- **后处理**，将信号发送给执行器，包括限制的处理以及信号滤波，如图4所示。因为油门、刹车、转向这种执行器本身有上下限、滞后（回滞曲线），所以需要对信号进行一些相关处理。

### 1.1 控制的意义

控制主要是**为了弥补数学模型和物理世界执行之间的不一致性**。

#### 性能要求及评测

[自动驾驶](https://so.csdn.net/so/search?q=自动驾驶&spm=1001.2101.3001.7020)系统对性能的要求需要控制模块，主要体现在以下几个方面：

- 稳定性，包括在所有场景下的车辆行为稳定和安全。
- 稳定状态的行为，减少或者消除规划和实际车辆行为的差别。
- 瞬时状态的行为。

自动驾驶系统是否满足性能要求可以从三个角度去评测：时域、频域以及discrete domain（离散域）。

- **时域**，指输出在时间轴上应该满足的要求。其衡量的指标包括steady state gain、rising time、setting time、overshoot和undershoot。每个指标对应的具体含义如图所示：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817124109370.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)
- **频域**，在频域空间，X轴是输入频率，Y轴是输出跟输入的比例，理想状态下输出和输入比例应该为1。系统性能在频域中的评价指标包括pass band、cutoff frequency等，如图所示：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817124025455.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)
- **离散域**，discrete domain。

对系统来说，在time domain跟frequency domain中的系统需求是可以等价转换的，系统在时域中的要求、响应、数学表达跟频域是可以相互对应的：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817124541742.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020081712463448.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

此外，系统性能要求还有一些其它的考量指标，如图所示：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817124720343.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

#### PID控制器

控制器的存在才能使得这些性能指标的满足成为可能。

最简单的控制器就是PID控制器，即比例、积分、微分控制，是一个model free的控制方法，也就是说PID控制具有通用性。![PID控制的基本原理](https://img-blog.csdnimg.cn/20200817130113197.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

U是参考量，它和反馈信号之间的差距用error 表示，即图中的e。
比例控制P的意思是该控制量与误差成比例，用kp*e(t) 表示。当kp比较小的时候，接近终值的速度会非常慢（如右图的红线所示），但是它有超调与undershoot现象。当kp设置比较大时，则达到稳态速度变快，但会超调（如右图紫色曲线所示）。
如果系统中存在损耗，比如汽车上坡的动力或者摩擦损耗，使得比例控制每次增加的控制量就等于或者小于损耗时，出现稳态误差，这就是引入积分控制的目的，它可以将之前的误差进行积分，消除稳态误差。而微分控制的目的是：使系统更快的从瞬态转化为稳态。

系统的控制量就是P+I+D三项的和。
PID控制是一个在工业控制应用中常见的反馈回路部件，由比例单元P、积分单元I和微分单元D组成。PID控制的基础是比例控制；积分控制可消除稳态误差，但可能增加超调；微分控制可加快大惯性系统响应速度以及减弱超调趋势。

## 2.基于模型的控制方法

相对于简单的PID控制，Apollo里面更多使用基于模型的控制方法，它包括四个部分：**建模、系统辨识、控制器设计**和**参数调优**。本节主要介绍前三个部分。

### 2.1Modeling建模

Modeling一般可以分为**分析建模**和**拟合建模**。通常，一个模型主要由各种属性表示，主要包括描述输入输出的数量、模型是线性还是非线性、连续还是离散等特性。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817131109899.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

控制模块中的模型，通常包括**运动学模型**和**动力学模型**。运动学模型是一种几何模型，感知、预测讨论的模型则以运动学模型为主。控制模块中，更多考虑动力学模型。运动学模型是动力学模型的一个子集。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817131202374.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

在自动驾驶中，Dynamic model以Kinematics model为初始模型，将环境等参数设置到Kinematics model中，把车看作质点进行分析。Dynamic model将车按车轮等部分分开进行约束或者系统补偿。

图中是两个比较简单的几何模型，左图是一个综合移动机器人控制模型，右图是著名的自行车模型，它把汽车看作只有两个轮胎的自行车，该模型在当年的DARPA挑战赛上获得冠军。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817131433456.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

实际上，只考虑几何约束是不够的。下图的动力学模型，不仅考虑了几何约束，还考虑了力矩和扭矩平衡。在自行车模型中，把前后轮都在XY两个方向进行分解。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817131631794.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

下图是刚体的一些力矩分析以及扭矩分析的公式，总体满足牛顿第二定律。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817131801893.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

在假设纵向速度为0的情况下，对横向方程进行线性化，如下图。线性化的过程需要基于一些假设。大家一定要记住，做完控制之后要检查这些假设是否合理或者是否会造成很大的误差。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817131906645.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

通常情况下，模型的建立是基于误差，而不是参考值，如图8所示，对实际侧向加速度和理想侧向加速度之间的误差进行建模。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817132111451.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

在控制器实现过程中，通常会将**ODE**或者**PDE**方程进行处理，转化为矩阵计算的形式。虽然在数学表达形式上不一致，但是其物理含义保持不变，如图9所示。在状态空间表示中还会给出一些状态量的标识，包括输入量。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817132250100.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

关于汽车的动力学模型的参考文献：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817222827515.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

### 2.2 系统辨识

在模型中，有些参数是未知的，系统辨识的目的是确定这些未知参数的值。确定未知参数的方法有三种：

- **白盒**，指对于基于第一原理（如牛顿定律）的模型结构，可以由测量数据估计模型的参数。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200817223234126.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)
- **灰盒**，用于只有部分模型结构可知，通过数据重建的方法来获取模型的其它部分的方法。
- **黑盒**，指模型结构和参数都在未知的情况下，只能通过输入输出数据来估计的方法。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818125943289.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

关于白盒和黑盒方法更多的参考资料：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818130117788.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

基于学习的系统辨识方法可以参考以下资料，基于学习的辨识方法和黑盒方法很类似。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818130229350.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

### 2.3控制器设计

控制器的设计包括**滤波器设计、控制器设计**以及**观察器设计**等。

滤波器可以分为线性和非线性，数字滤波或者模拟信号滤波，离散滤波或者连续滤波等。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818130450740.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

系统在频域里面需要满足某些性能要求，滤波器通常也会对频域信号进行处理。根据频域边界对滤波器进一步细分，包括低通滤波，高通滤波等。![在这里插入图片描述](https://img-blog.csdnimg.cn/2020081813064596.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

根据实现方式不同，滤波器又可以分为高斯滤波、卡尔曼滤波、贝叶斯滤波等，这些滤波器通常用于预测和跟踪。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818131015441.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

## 3.控制器类型

控制器的类型大致可以分为三类：**开环控制、前馈环控制**和**后馈环控制**。![在这里插入图片描述](https://img-blog.csdnimg.cn/2020081813113016.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

### 3.1前馈环控制

前馈环控制器可以分为两类，如图：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818131547188.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

前馈环控制器的主要控制策略有很多种，这里主要介绍三种：**Optimal Control（优化控制）、 Adaptive Control（自适应控制）、Robust Control（鲁棒性控制）**。

设计控制器需要考虑：

- **可控性**（Controllability）是指系统是不是能按期望通过控制量U达到相应的动态；
- **可观性**（Observability）是指在初识状态已知的情况下，是不是可以重构整个系统的状态。

#### 优化控制

优化控制的目的：在给定系统的情况下，找到或者设计出一个控制法则使系统可以满足特定的优化标准。

图中给出了优化控制的一个分类和演化过程。最早可追溯到上世纪五六十年代的卡尔曼滤波和后来的LQR。这两个控制在一起可以得到一个LQG，LQG是一个线性并且没有限制的控制器，在这个基础上增加限制，就得到了LMPC。在LMPC的基础上，增加非线性因素就得到了MPC。从图左边到右边的控制器演化，响应速度更快，但是计算代价更高。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818133126886.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

##### LQR线性二次型调节器

Apollo项目开源了LQR算法。在线性化的横向状态方程上做LQR，一般的表示方程如图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818134154511.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

这个基础上，增加前馈项，然后做一个拉普拉斯转换，从时域转换到频域。目标是使系统的error X=0，经过一系列变换之后可得到前馈项，具体过程如图：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818134528824.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

##### MPC

MPC控制器的基本逻辑：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818134727925.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

它包含**Predictive Plant、Real Plant、MPC Controller**以及**Feedback Correction**。MPC和跟LQR的区别在于，MPC有一个关于时间T的优化矩阵，同时还有一系列的控制约束。如果想设计一个非常高效的、能在工程上应用其满足鲁棒性理论要求的控制器，一定要做离散化。

MPC的代价函数如图，代价函数增加了约束边界，有上边界和下边界：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818134931416.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

关于优化控制的的参考文献：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818135005840.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

#### 自适应控制

自适应控制：一种针对控制系统中参数多变或者初始值不确定的控制方法。
最简单的一种方法就是根据输入使用swith的方式，根据输入或者gain选择不同的控制算法：![在这里插入图片描述](https://img-blog.csdnimg.cn/2020081813521284.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

实际上，自适应控制更多的作为其他控制器的一种补充使用：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818135342165.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

关于自适应控制的参考资料：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818135521170.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

#### 鲁棒性控制Robust Control

鲁棒性用来解决如何确定模型的正确性问题，主要是用来处理模型的非确定性，是一种在已知模型错误边界的情况下，设计一个性能不错而且稳定的控制器的方法。

最简单的鲁棒性控制器是LQR/LTR控制器，也是一个二次线性调节器，如图：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818135609339.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

#### 离散化

离散化实际上是在尽可能的保存连续空间信息的情况下，把连续空间的问题转换为离散空间的描述，使得计算机能够更好地处理。
离散化跟Digital Stability是相关的，如果采样不够好，会丢失很多信息使得系统不稳定。

离散化有很多的方法，各种方法都有各自的优缺点。但是总的来说都是把数字信号转换为模拟输入/输出信号。同样，也会把Analog输出进行离散化，然后输入到数字信号控制器中。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818140031215.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

图16是进行离散化的一个简单例子，左边是时域里的函数performance的表达方式，右边是进行离散化的一些常用表达形式。最后一列是收敛的速率，表示在一定工况下，数字控制器在给定的时间下是可以保证收敛的。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818140125197.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

离散化时的一下简单转换公式对应关系：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818140246848.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

更多关于离散化的参考资料：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818140636322.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

### 3.2 控制器的其他方面

影响控制器性能的一些因素，包括：

- **Deadzone**，主要是执行器的一些特性引起的，例如汽车的油门，可能给油0%～15%的区间都不会使汽车前行，这个时候反应在图上就是一条平行的线段，称之为Deadzone。在控制器设计的时候需要对这部分进行补偿设计：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818141018516.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)
- **饱和和抗饱和**处理，是出于对执行器的特性的考虑，通常一个执行器是有上限和下限的。把输出值做一个限制，使得输出在执行器的上下限范围内。如果不进行饱和处理，在输出100%的情况下突然转换状态，收敛到最终值可能需要很长的时间。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818141237597.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

关于Deadzone补偿和饱和、抗饱和的参考文献：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818141437284.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

### 3.3 控制器的发展趋势

未来控制器可能从以下几个方面发展，如图22所示，包括数据驱动的控制、结合轨迹生成的控制、结合预测的控制、基于模型的增强学习控制方法。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200818141550208.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

### 3.4 工程应用案例

目前，在Apollo中，控制的工程应用主要有两个方面，一个是系统识别，使用的是自动标定方法。另一个是安全策略：![在这里插入图片描述](https://img-blog.csdnimg.cn/2020081814172343.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

在自动驾驶系统中，有很多的部件参数是不确定，供应商也不会提供，但是在控制或者其它模块可能需要对这些部件进行建模，首先就得识别部件的参数，通常采用的是自动标定的方法。

安全策略的考虑主要是基于控制是否与底层交流的最后一个模块，所以有很多的安全策略需在控制层面完成。安全信息可分为两个部分：上游信息（Planner发出）+下层反馈信息。如果上游Planning信息丢失、延时、未更新，控制系统需要做出诸如Emergency Stop、缓行之类的决策。类似的，由于接触不稳或者其它因素，导致控制指令没有执行，控制器也需要做一些安全策略的考虑。