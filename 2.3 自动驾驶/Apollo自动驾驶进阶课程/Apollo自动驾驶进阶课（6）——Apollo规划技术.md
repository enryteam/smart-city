- [Apollo自动驾驶进阶课（6）——Apollo规划技术_Oceans_depth的博客-CSDN博客_sl坐标系](https://blog.csdn.net/qq_45577461/article/details/107931195)

## 1.规划概览

规划问题本质上是一个搜索问题，即对一个给定的函数，寻找最优解。无人车规划问题就是给定现在的状态，找到无人车移动的最优解。通常最优解目标函数F(x)定义。
从内容考虑，规划问题涉及三个领域：

- **机器人领域** robotic fields，规划就是如何产生轨迹以完成目标，涉及RRT， A*，D* lite等。
- **控制领域**，规划理解为到达目标状态的动态系统，涉及MPC， LQR等。
- **人工智能** artificial intellegence（AI），是生成状态到动作的映射，涉及reinforcement learning，end-to-end imitation learning等。

### 1.1构建汽车运动规划

把运动规划抽象成一个path finding problem（路径查找问题）。寻找最短路径，可通过BFS、DFS。但是对于最短路径优化问题，DFS的效率太低。缺点：没有利用起点和终点之间的信息，BFS和 DFS都属于non-information search，问题就在于不知道目标在哪里。

另外，可以通过启发式方式对搜索问题进行优化。A* 算法是大概知道目标点位置，定义一个启发式函数，该函数猜测距离目标还有多远，通过这种方法先搜索一些比较近的点，然后从这个点出发逐渐扩大搜索圈。
A* 花费时间比BFS时间更短，因为它有信息支持，现在的一些路径搜索算法本质上都是从A* 算法出发，需要知道目标函数的样子。
目前，A* 算法还不能直接用在规划模块上，因为A* 算法要求对整个环境全知。而[自动驾驶](https://so.csdn.net/so/search?q=自动驾驶&spm=1001.2101.3001.7020)对周围环境是部分观察的，无人车的传感器（雷达、激光雷达、摄像机）系统能部分观察环境。

对于部分观察可以使用贪心算法，是一个增量搜索，是在看见的情况下尽量走好。如图4所示，利用D* 算法对部分观察的数据进行控制规划。
它利用当前看到的信息进行增量规划，D* 的特点是处理有限范围信息的条件下，到达预定地点的搜索问题方法。这种增量搜索很难通过一步步的迭代达到全局最优解。

没有考虑无人车运动过程中的运动模型和动力学模型。
可以通过平滑性曲线的方式来优化折线，换成一些较为平滑的曲线来完成，

上述搜索算法与自动驾驶规划的距离：

- 首先是在部分观察空间的动态障碍物，规划模块对动态障碍物的处理是关键且有难度的。
- 其次是自动驾驶汽车按照规划行驶需要动态模型。
- 第三是自动驾驶规划需要遵守交通规则，道路安全基本保证，将交通规则融入规划也是一个难点。
- 第四是实时计算，目前来说百度要求规划模块运转周期是100毫秒。

运动规划问题就是让自动驾驶车辆能够安全平稳到达终点，本质是一个三维规划问题，即 XY 坐标和时间维度，称 3D Trajectory Optimization Problem（轨迹优化问题）。
从车辆动力学模型来说，维度需要进一步上升，因为涉及到车头的方向，车的转向角、加速度等问题。

### 1.2 无人驾驶软硬件系统

##### 硬件系统

无人车硬件系统除了汽车之外，还涉及很多传感器，传感器感知汽车周围环境，即使是这样也只是部分搜索环境。还有 GPS 接收器可以做定位，以及 IMU 惯性导航系统。

##### 软件系统

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811094800983.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)
运动规划可以获得两部分信息，一部分是动态信息，包括从认知获得的信息，就是从感知模块和定位模块获得信息，另一部分是静态信息，就是高精地图。

无人驾驶系统软件包括定位、感知、预测、运动规划和控制等。
定位就是知道汽车在哪里。
感知即是对周围环境信息的获取。
预测就是感知到的障碍物的行进意图。
运动规划是在知道这些信息后。
控制模块就是得到指令之后如何控制汽车。

车辆状态、交通灯信息、障碍以及障碍轨迹、导航、高精地图都是规划模块能获得的信息。
规划就是在这样的部分可见信息中给无人车找到一条轨迹。它不仅是一条路径，而是随着时间推移路径该怎么走，它包含两方面，路径信息和速度配置文件，需要保证速度和路径变化都是平滑的。

## 2.基本技术和方法

### 2.1基本方法

- 去离散化连续空间的方法叫做**Roadmap**，使用简单的连通图表示配置空间。
  其中Visibility Graph是一种常用的Roadmap方法。Visibility Graph将起始节点，所有障碍物的顶点和目标节点相互连接来构建路线图。两点之间的最短路径一定会通过靠近障碍物边界的折线。
- **Cell decomposition**（网格分解方法），将整个空间分割成一个个cell，通过cell的连接图表示自由空间的连接属性。
- **Potential field**（势场法），直接用微分方法处理。

运动规划的基本方法主要有RRT、Lattice、Spira、Polynomial、Functional Optimization等。

一种常用的抽象连续空间的方法是PRM。它在整个配置空间随机采样一些点，如果点在障碍物上则去掉，然后将这些点连接起来，两点的最短路径就可以利用A* 算法进行求解，该方法要求是对全局感知，而无人车是一个部分感知的应用场景，因此有RRT的改进方法。

#### RRT基于快速扩展随机树算法

它构造一个根结点为起始点的配置空间树，通过随机采样增加叶子节点的方式，生成一个随机扩展树，当随机树中的叶子节点包含了目标点或进入了目标区域，便可以在随机树中找到一条由从初始点到目标点的路径。如果叶子节点和目标节点之间的连接被障碍物阻挡，则需要重新采样。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811113727685.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

通过这种方式离散化的线是不适合无人车行驶的，因为这些线的curvature不连续，甚至没有curvature。针对这一问题MIT提出使用平滑曲线进行连接的方法，如下图所示。但是该方法得到的路径可能还是不够平滑，另外对动态障碍物的处理也存在问题。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811113807260.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

#### Lattice网络方法

最原始的Lattice网格方法非常简单：在XY世界坐标系中，以1米为单位进行网格划分，然后用无人车可以行进的、曲率连续的曲线将起始点和目标点连接起来。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811113944208.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

对于道路来说，这种抽象方式并不合适。Lattice Sampling撒点不能在规则化坐标系下去撒点，因为道路并不是一个完全XY的坐标系。因此提出了在sl坐标系下进行离散的方法Lattice in Frenet Frame。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020081111462221.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

#### Polynomial方法

当抽象出这些点之后，需要使用平滑曲线连接。
有一种使用螺旋曲线的方法，即Splines方法。此外，还可以使用路径-速度迭代优化的方法对Lattice方法进行优化，也就是Polynomial方法。它将问题降维，分成了path 和 speed两个维度逐渐优化，这是一种iterative的处理方式。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811114749697.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

#### Functional Optimization方法

用Functional Optimization方法对运动规划进行处理，对整个问题建模，设计相应的代价函数。二次规划就是其中一种常用的方法。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811115013156.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811115438282.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

### 2.2运动规划框架

运动规划是在连续空间的一种优化，对于连续空间过程的优化往往比较难。因此，通常先将连续空间问题离散化表示，然后寻找对应的解决方案。可以使用图搜索的方法对离散空间问题进行求解。

质点模型将运动轨迹当成一个点，这个点和无人车是不一样的。假设把一个无人车看成一个点，这个点和另一个点不相撞，在数学定义上是点和点没有交集，但是在实际生活中一个车和一个车可是会相撞。下面介绍解决这些问题的一些方法：Configuration Space （构造空间），也就是说能够控制什么变量。对于刚体而言，不仅是XY坐标，还要有heading信息才能研究跟障碍物之间的关系。对于无人车来说有更多的变量。其复杂性主要体现在两个方面，一个是Space Dimensionality（空间维度），另一个Geometric Complexity（几何复杂性）。例如bounding box跟bounding box之间怎么相交，一个多面体跟一个多面体之间怎么检测出路径，以避免跟另一个障碍物相交。

规划问题中涉及到一些约束条件，Constraints（约束）大概分为三类：一个是Local Constraint，例如避免和障碍物碰撞。第二是Differential Constraint，比如边界曲率。最后是Global Constraint。比如最短路径。

## 3.环境中的运动规划

运动规划根据环境的变化在算法和处理方法上有很大的不同，涉及到模型建立、平滑优化和坐标转换以及障碍物投影等。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811121946565.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

### 3.1 Vehicle Model的建立

对于汽车而言，质点模型是远远不够的。
首先从刚体角度考虑，二维平面里的刚体涉及到xy和以车后轴中心xy作为坐标原点车身的朝向heading。因为无人车运动模型还多了一个转向的变量，多了一个自由度，刚体模型也不够。
可以将汽车运动模型简化为自行车模型，将四轮抽象成两个轮子，前轮中心和后轮中心的运动方向和自行车一样。车辆在垂直方向的运动被忽略掉，用一个二维平面上的运动物体来描述车辆的运动模型。
自行车运动的时候具有以下特点，旋转车头的时候，前轮和后轮都围绕一个中心点转动，并且后轮的转向半径(1/k)与方向盘转动角度(w)满足关系 **k = (tan(w))/L**，其中L为前轮中心和后轮中心的距离。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020081112224367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811122417697.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

在实际的自行车运动模型中，后轴中心是沿着一条平滑的轨迹运行，该轨迹对应的曲率 表示调整方向盘的度数，如果为正，表示向左转，反之则向右转。因此，自行车运动模型可以用x、y、朝向、曲率、速度来表示。

为了能够估计障碍物的距离，先了解曲线坐标系以及与世界坐标系之间的转换关系。

### 3.2曲线坐标系SL

SL坐标系也叫做frenet frame，以道路中心线为参考，S表示道路中心线的方向，L表示与道路中心线垂直的方向。
在结构化道路上行驶的时候，SL坐标系比XY坐标系更加贴合实际需求。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811122459198.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

#### SL坐标系到XY坐标系

因为很多信息是全局的，所以要投影到世界坐标系，例如红绿灯位置，参考的是XY世界坐标系。
在给定SL坐标系时，每一个点的S坐标本身对应一个（x-r，y-r）坐标，根据该点的横向偏移距离，可以求出给定点在世界坐标系中的XY位置，如下图所示。其中theta是参考线的方向，也就是切线方向。如果XY与S方向平行的话，轨迹的曲率还满足图中所示的关系。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811122800539.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

#### XY坐标系到SL坐标系

因为SL坐标系并不是唯一的，XY会在曲线上产生很多投影，投影点是经过XY坐标，且垂直于曲线的线段与曲线的交点，如下图所示，XY就有两个投影点。通常情况下会增加一些限制，例如投影距离不能超曲率值。需要注意的是，掉头的时候还是需要特殊处理的。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811123049562.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811123420216.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811123450978.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811123557205.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

### 3.3平滑处理

在自动驾驶中，将环境抽象成 SL 坐标系，在此坐标系下的曲线光滑度是有要求的。

- 首先，曲线本身要平滑。
- 其次，其曲率也要满足平滑的特性。

因此需要对轨迹线进行平滑处理。
XY 坐标本身与 Curvature 是有联系的，不能单独平滑曲率，也不能单独平滑 X 或者 Y。

生成一条光滑的曲线，涉及到两方面：目标和工具。
定义平滑的最简单的方法就是最短路径，但是路径最短还不能保证平滑性，因此会对其不同阶导数进行 Minimize 求解，保证导数空间的连续，这就是 Smoothing Spline 最初的思想。问题的目标就明确了，定义一个函数，能够最小化它的类似三阶导平滑性。
![一维平滑度定义](https://img-blog.csdnimg.cn/20200811124334662.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)
Smoothing Spline 具有一些特殊的性质，在给定边界的条件下，它是一个多项式，可以找到最优解。但是它的 Boundary Constraint 只考虑了起点和终点，如果中间有障碍物就不是最优解。这种情况下可以使用 Piecewise Polynomial（分段多项式）来处理。

#### 多项式

首先，可以在轨迹上以等距离的方式随机选择一些点，然后用高阶多项插值的方式来近似表示轨迹，对多项式进行优化。但是高阶多项式不能用于平滑，因为高阶的多项式抖动太大，没有办法控制幅度，这就是龙格现象，如下图所示：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811124051808.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

#### Bezier Spline

Bezier Spline 曲线是由一系列控制点定义的。如下图所示，分别给出 1 阶、2 阶、3 阶 Bezier Spline 曲线的表示形式。通过对它们做平滑，得到平滑的曲线，例如二阶平滑保证曲线的曲率平滑。但是这种方法的缺点是，除了起始点和终点，其它控制点不能保证会被得到的曲线经过。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811124956314.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811125026414.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

#### Spline 2D

一个 Piecewise Polynomial 是一维的函数，描述二维曲线时就有一个 Spline 2D。
假设把曲线分成 N 截，每节曲线段的 X 坐标是一个 Polynomial ，Y 坐标也是一个 Polynomial 。用 5 阶多项式来表示 X 和Y，称之为Quintic Spline（五次样条），每一节都是这样的函数。这种使得目标函数具有旋转不变性。
为了让曲线足够平滑，让它在 X 坐标上的变化率，也就是三阶导的平方是最小的，Y 上的变化率三阶导也是最小的，代价函数就是这两个变化率的和。代价函数的求解就是一个二次规划问题，把这种 Loss Function 定义成这种形式是因为平方的积分能够给计算带来便利。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811125259242.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)
前面说的是用一节一节的线段来保证曲线是光滑的，在线段内部用一个二维的 Polynomial 表示，在内部是 N 阶可导的，**端点约束条件**就可以保证节点处是平滑，需要保证 X 和 Y 方向的倒数是相等的，一般要求到三阶导都是相等的，包括它的 X，Y 点的值也完全相等，此时就能保证三阶导连续。

#### Spiral Path

还有一种方式叫做螺旋曲线，它通过一个极坐标形式定义，比如说沿着一条曲线，如果一个点 S 的曲率是知道的，假设它的原点在 （0，0）的位置，可以唯一定义出一条经过 S 的曲线，也就是 Spiral Path 。那么可以让 Spiral Path 满足起点、终点约束条件生成一条螺旋曲线。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811130254215.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70)

任何的曲线在足够密的时候都可以用Piecewise Spiral path 或者是 Piecewise Polynomial 表示。
Spiral Path 和 Spline 2D 的区别：
它们的出发点不一样，Polynomial 计算很快很简单，Spline 2D 是一个凸空间里面生成一个 Spline 曲线。Spiral Path 是从 Configuration Space 出发。理论上来讲，螺旋曲线生成的线是要比 Spline 更好处理，对一些极端情况处理更好。

## 4.运动规划的优化

约束问题的核心有三点：

1. **目标函数** Objective Functional，目标函数是一些关键特征的线性组合，目标函数的清晰对于求解更有利。
2. **约束** Constraint，比如路网约束、交规、动态约束等。
3. **约束问题的优化** Solver，优化求解方法的目的是找到最佳路径，比如动态规划、二次规划等。

### 4.1动态规划

动态规划通过类似于有限元的方式，把问题从连续空间抽象成离散空间，然后在离散空间中进行优化。

虽然这种方法可以逼近连续空间中的最优解，但是计算复杂度很高。
针对计算时间长的问题，可以使用牛顿方法进行优化，它的收敛次数是指数平方，也叫二次收敛。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812175712487.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812175924990.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

### 4.2二次规划

二次规划算法的本质是牛顿法的 Taylor 展开，但是它的求解过程涉及更复杂的情况。因为二次规划方法并不一定是处理一维问题，可能涉及更高阶求导。在实践中，二阶导数基本可以满足问题需求。

#### 二次规划问题的求解方法

然而，牛顿法要求 locally convex 才能保证收敛，也就是导数是严格单调递增的。但是一般函数并没有这样的特性，动态规划或二次规划都无法获得全局最优解。

为了解决这样的问题，通常使用启发式搜索方法：

> 首先通过动态规划方式对整个问题有一个粗浅的认识，
> 然后通过二次规划进行细化。

这种启发式搜索方法也是目前百度 [Apollo](https://so.csdn.net/so/search?q=Apollo&spm=1001.2101.3001.7020) 的 EM 算法的核心思想。

决策问题是一个离散空间中的优化问题，它的决定是：通过动态规划对整个空间形成一个粗浅的认识，然后以此为启发，用二次规划求最优解。

一般来说，二次规划问题会写成一个二次函数，如下图所示。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812180828755.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

对于带等式约束的二次规划问题的情况如下图所示：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812181339776.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

这种情况可以有很多种解法：

- 把限制条件放到上面的式子中，通过换元，变成一个全新的 QP 问题求解，但是这种方法很慢；
- Lagrangian method ，通过增加松弛变量的方式去掉约束条件，变成一个可以解决的问题。

对于带不等式的约束条件的二次规划问题的求解可以使用 **active set method**，其主要出发点是最后解，可能落到边界上，如果真的是边界最优，不等式约束就可以转化为等式约束问题求解。求解二次规划问题的方法 KKT的主要思想如下图所示：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812181838868.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

总之，对于求解非线性优化问题（自动驾驶中的规划基本都是非线性的），通常就是用启发式方法来求解。**先用动态规划给出一个粗略解，给出一个凸空间。然后用二次规划方法在凸空间里去寻找最优解**。

## 5.Apollo规划EM

EM是一个在已知部分相关变量的情况下，估计未知变量的迭代技术，EM的算法流程如下：
初始化分布参数；重复直到收敛。
重复直到收敛的步骤如下：

E步骤：根据隐含数据的假设值，给出当前的参数的极大似然估计；M步骤：重新给出未知变量的期望估计，应用于缺失值。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812183102962.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)
在这个场景中，有三类约束，第一个叫做 Rraffic Regulation，第二个是 Decisions，第三个是 Best Trajectory 。这些限制又分为硬限制和软限制，例如交通规则属于硬性限制。

### 5.1 Apollo EM规划框架

在 Apollo 中有一个 EM 规划框架来处理不同的场景，下图展示处理一个换道场景。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812183424633.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

在蓝线和红线交点处发现前方有车辆行驶缓慢，可能要进行换道处理。
在 Apollo EM 规划框架中，对换道和继续在本车道行驶分别规划出一条轨迹，只有换道之后的 Trajectory 要比本车道的 Trajectory 好的情况下才换道。
在 Apollo 的 EM planner中，决定哪个道比较好的模块叫做 Reference Line Decider，中间的并行模块是通过 Path Speed Iterative 的方式并行实现的。

### 5.2 优化决策问题

优化决策问题本身是一个 3D optimization 问题，其中包含了三个维度，需要生成 SLT 。
三维空间的优化相对比较复杂，基本思想是降维处理，先在一个维度上进行优化，然后在优化的基础上再对其它维度进行优化，并持续迭代以获得局部最优解。
常用的方法有两种：**离散化**的方式和 **Expectation Maximization**（期望最大化）。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812203021439.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

对于无人车，Apollo 上的 EM planner 对 Path-Speed 进行迭代优化。首先，生成一条 Optimal Path ，在最优路径的基础上生成 Optimal Speed Profile 。在下一个迭代周期，在优化后的 Speed 的基础上，进一步优化 Path，依次类推。它分了四步走，其中分为两步 E step 和 M step 。
这种算法的缺点：迭代算法的本质是贪心算法，不一定能收敛到全局最优解。

#### 非线性优化问题

对于非线性优化问题，通常先用动态规划找一个粗略解，然后用二次规划找出一个最优解。
以路径规划为例，假设前方有一个障碍物，首先做出从左边还是右边的避让决策，然后通过 QP 生成一条平滑的曲线去避让障碍物。对于速度而言，先通过动态规划的方式给出一个粗略的解，然后再通过二次规划的方式给出一个更平滑的解。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812203304871.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812203536892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)
在决策规划里动态规划 Path：先确定主车的位置，然后往前排撒若干点，基于撒点网络得到一个代价最低的路径，这时候的路径不够平滑。然后利用二次规划方法，按照问题抽象、模型建立和优化求解的步骤生成一条平滑的轨迹。这里不要求函数必须是凸函数。

对于速度的优化，同样是类似的，如下图所示：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812203727432.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

#### 规划问题解决逆行

对于逆行的处理，首先根据当前 Speed Profile 去估计当前逆行障碍物的位置，然后再修正 Path，根据修正之后的 Path 再来处理 Speed，例如需要减速。减速之后，估计需要重新改变路径，依此类推，直到得到理想的规划轨迹。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812204051116.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

目前，百度 Apollo 无人车项目的规划模块进展如下图所示，支持在城市和高速等环境下的多种驾驶场景处理，包括直行、转向、路口、停车等。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200812204254372.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTc3NDYx,size_16,color_FFFFFF,t_70#pic_center)

### 5.3强化学习和数据驱动方法

决策问题通常用 POMDP 加上一些机器学习的技术来解决。
解决好规划问题，需要把两个方面做好，一个是数据闭环（Data Driven），另一个是基于规则的方法。数据驱动是在基于规则的闭环里面的小闭环。Rule Based 的方法可以对遇到的新案例，很快给出解决方案。

在基于规则的方法的基础上，对问题形成一定的认识，通过把问题抽象成更加通用的问题，定义目标函数来进一步优化问题。

数据驱动的方法就是通过大量的案例统计分析，得到模型，使得遇到类似问题的时候，不需要过多的考虑，直接套用数据驱动的模型获得结果，Data Driven 的方法其实就是基于经验的方法，只不过这些经验是模型通过大量的样本数据学习得到的。