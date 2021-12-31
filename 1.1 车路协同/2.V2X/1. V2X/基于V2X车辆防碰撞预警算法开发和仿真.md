- [2020 中国汽车年会 基于V2X车辆防碰撞预警算法开发和仿真]([PowerPoint Presentation (mathworks.cn)](https://ww2.mathworks.cn/content/dam/mathworks/mathworks-dot-com/company/events/conferences/automotive-conference-china/2020/vehicle-anti-collision-early-warning-algorithm-development-and-simulation-base-on-v2x.pdf))

杨波  广州汽车集团股份有限公司汽车工程研究院

## 一、V2X介绍

V2X（Vehicle to everything)，即车联网。通过无线通讯技术，将车-路-人-云等智能终端形成联网，使汽车具 备复杂环境感知，兼具智能决策、协同控制的能力，为未来出行提供安全、便捷、舒适的服务。

![image-20211231092559177](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092559177.png)

本课题研究领域行业内发展趋势

![image-20211231092617472](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092617472.png)

## 二、V2X-ACC算法

（1）基于Simulink和Automated Driving Toolbox工具箱的ADAS算法开发流程

![image-20211231092643085](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092643085.png)

（2）基于Simulink和Automated Driving Toolbox的V2X-ACC算法开发思路（Simulink demo演示）

![image-20211231092659373](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092659373.png)

（3）基于Simulink和Automated Driving Toolbox的V2X-ACC算法开发——替换摄像头、雷达为V2X（模拟）传感器数据

![image-20211231092713742](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092713742.png)

（4）模拟V2X传感器，获得包含场景车车速、位置、角速度等信息的V2X信号，在Vehicle and MIO模块中进行车辆场景融合 与最重要目标车辆(Most Important Object，MIO )的筛选和跟踪。

![image-20211231092727805](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092727805.png)

## 三、V2X-ACC控制参数寻优

（1）基于PSO （ Partical Swarm Optimization ,PSO ）寻优ACC控制参数

通过对设置的控制参数进行PSO优化，可获得在ACC控制中提升驾驶的舒适性已经路径跟踪的准确性。

![image-20211231092755210](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092755210.png)

（2）优化前后仿真数据对比

通过PSO优化前后数据对比，可以看出，优化后ACC控制中，Accelerate变化更加平滑，提升了ACC驾驶的舒适 性，同时安全性也优于优化前。

![image-20211231092812392](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092812392.png)

## 四、基于Simulink和PreScan的联合仿真

（1）基于PreScan和Simulink的联合仿真流程

![image-20211231092831109](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092831109.png)

（2）PreScan场景建模

![image-20211231092846237](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092846237.png)

（3）基于PreScan的Simulink 预警算法开发

![image-20211231092858802](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092858802.png)

![image-20211231092917249](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092917249.png)

（4）V2X信号的组装与广播传输

​	![image-20211231092939807](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231092939807.png)

（5）V2X信号接收与算法结果展示

![image-20211231093001009](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231093001009.png)

（6）V2X预警GUI显示

![image-20211231093015965](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20211231093015965.png)