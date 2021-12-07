- [V2X与ITS的前世今生](https://mp.weixin.qq.com/s?__biz=MzI5NzExMTY0Mg==&mid=2650616516&idx=2&sn=0738177ed2859a6588c56003fa28d929&scene=19#wechat_redirect)

V2X可以简单分为两大类，**一类是以智能交通（ITS）为核心的，发起者自然是政府机构。另一类是以智能驾驶为核心的，发起者主要是汽车厂家和电信运营商。**另一种分法就是按通讯方式，一类是**DSRC**，一类是**C-V2X**。DSRC主要是针对智能交通应用的，欧美日都选择以DSRC的智能交通技术路线，某种意义上讲DSRC与C-V2X并非水火不容，C-V2X更侧重智能驾驶。

早在1994年，美国高速公路管理局推出**先进高速系统AHS研究课题**，1997年成立智能汽车计划小组研究智能交通，2005年完成研究任务，提出了完整的ITS体系。

同时在1999年，FCC就为ITS划分了一个5850MHz-5925MHz频带，决定用当时最先进的基于802.11a的技术。并分成七个独立的频道，分别为频道172、174、176、178、180、182、184；各频道均为10MHz。频道178为控制频道(Control Channel，CCH)，负责WAVE服务广播讯框(WAVE Service  Advertisement，WSA)封包；其他频道则为服务频道(Service Channel，SCH)，只能传递WAVE短信息(WAVE  Short Message，WSM)封包。

同时在2003年，全球八大车厂丰田、日产、福特、通用、戴姆勒、克莱斯勒、大众、宝马成立VSCC车辆安全通讯联盟开展DSRC车端的研究，2005年通用演示了第一个V2V系统。之后经过8年的完善，2013年DSRC形成了完备的体系。

2014年2月，欧洲标准组织ETSI与CEN宣布完成第一阶段基于DSRC的ITS标准，底层为IEEE 802.11P，上层为IEEE1609，同时还有SAE J2375和J2945两个标准定义通讯格式。

2014年8月，美国交通部试图强制立法推广DSRC为核心的ITS，但直到今天也没用完成强制立法。

欧洲方面，ITS系统源自1973年英国运输与道路研究所（TRRL）的SCOOT(Split, Cycle and Offset Optimization Technique)，更早SCOOT模型基础原自TRANSYT  (TrafficNetwork Study  Tool)，采用了同样的周期流分布图（CFP）的建模方式和相近的目标函数。不过有了显著的改进，TRANSYT的CFP是以历史的平均交通流计算的；而SCOOT是联机模型，CFP是实时测量的。

SCOOT的核心就是如何控制交通信号灯，中国的北京、青岛、成都、重庆、大连就采用西门子的SCOOT系统。  当时的技术无法利用传感器高效计算实时交通流量，因此意义不大。但这是ITS的基础方法论，SCOOT后来被德国西门子全盘继承，并衍生出SPAT（Signal Phase and Timing）。

SCOOT是跨整个路网进行交通号志变换时机的最佳化，仅倚赖工程师预先以固定且有限数量的可行程序进行配置，无法弹性对应即时路况与个别交叉路口的流量变化。

西门子在2018年推出Follow AI也就是下一代SCOOT，它首先会建立复杂的一般性规则，接着可针对每个特定的交叉路口进行个性化的适地性处理，Flow  AI根据内建的回环(loop)侦测即时的交通流，并运用云端AI即时产生近乎无限数量的交通号志变换时机选项。

欧洲ITS标准主要分5个工作组 (WG).

- WG1 (Application Requirements and Services)：ITS中基础应用需求与服务，并制定Applications与Facilities两层之通讯协议。 
- WG2 (Architecture and Cross Layer)：发展适合所有ITS之通讯架构与跨层管理协议，并扮演欧洲ITS通讯架构之协调者角色。 
- WG3 (Transport and Network)： 规范Networking和Transport两层之协议，并利用车载网络特有之地理位置信息特性，发展制定GeoNetworking及IPv6相关协议。
- WG4 (Media and Medium Related)： 规范MAC和PHY两层相关之标准，其将欧洲ITS使用之频谱划分为ITS-G5A、ITS-G5B与ITS-G5C三个部分，并兼顾其中之兼容性。
- WG5 (Security)：制定ITS相关之安全性议题，此草案为车载安全通讯标准制定之基准，规范车载环境中威胁、弱点与风险分析，该草案已于2017年3月正式出版。

目前ETSI正着手制定第二版标准，主要涵盖更多使用案例(Use Cases)，包括自动跟车(Platooning)、协同式可适应性巡航控制(Cooperative Adaptive Cruise  Control, C-ACC)，以及弱势道路使用者(Vulnerable Road Users, VRU)等。

![image-20211207143314776](https://gitee.com/er-huomeng/img/raw/master/image-20211207143314776.png)

- 信道技术层（ Access layer）：本层提供物理层与介质访问控制层服务，对应 OSI通信协议模型的物理层和数据链路层。
- 网络传输层（ Networking &Transport layer）：本层提供数据路由与传输服务，对应 OSI 通信协议模型的网络层和传输层。
- 服务设施层（ Facilities layer）： 本层为多个应用提供高层数据传输协议与信息管理服务，对应 OSI 通信协议模型的会话层、表示层和应用层。

除此之外， ITS-S 还分为以下功能层：

- 应用层（ Application layer）： 应用层模块表示 ITS-S 应用程序利用 ITS-S 的服务来连接一个或多个其他 ITS-S 应用程序。两个或多个互补的 ITS-S 应用程序组成了一个向 ITS 用户提供服务的应用。
- 管理层（ Management layer）：负责管理 ITS-S 的通信以及站内数据交换服务。
- 安全（ Security Entity）：为 OSI 通信协议栈各层提供安全服务。

CAM与DENM是智能交通系统中最重要的两种信息协议栈标准。

Decentralized Environmental Notification  Message，分散环境通知信息，主要用于道路危险预警应用，是事件触发型信息，一旦通过车载设备检测到了安全隐患事件(例如前方车辆紧急刹车、道路施工警告等)，车载ITS的相关应用就立即发射DENM信息。接收车辆可对比车辆自身位置与行车路线，判断事件对自车的关联性并预测可能的碰撞风险，以及提前通知驾驶员采取有效的措施。根据事件地点和类型，可能要求接收到DENM信息的车辆向外转发。

CAM(Cooperative Awareness Message)，合作感知信息，这是时间触发信息，提供车辆的速度、位置、方向灯以及交通信号系统如交通信号灯的状态，天气提醒等信息。

![image-20211207143109581](https://gitee.com/er-huomeng/img/raw/master/image-20211207143109581.png)

ETSI 在 2013 年发布了道路危险警告（ RHW） 应用 ， ITS-S 通过 RHW 应用检测到道路危险情况并触发生成相应的 DENM 消息，之后 ITS-S 会将这一 DENM 消息发送出去，通知一定区域范围内的其他车辆。

1、 原始 ITS-S 检测到事件后要生成描述该事件用例的 DENM 并将其发送给该用例对应的目的区域内的其他 ITS-S。

2、 DENM 传输的开始和终止由应用层的 ITS-S 应用程序控制。

3、 只要事件存在， DENM 就会持续发送。

4、处在目的区域内的 ITS-S 需要将接收到的 DENM 转发给其它 ITS-S。

5、 DENM 传输过程的终止， ITS-S 判断 DENM 的有效期字段， 在到达 DENM 有效期时 ITS-S 停止发送该消息， 或者在未到达有效期时但已经检测到危险事件已经解除则可以由 ITS-S 应用程序请求生成一个通知事件已经终止的 DENM。

6、 若收到 DENM 的 ITS-S 根据消息内容判断事件与自身有关，则做出适当的警告给使用者。

这个CAM应用类似于长沙智能驾驶研究院发布的“V2X+交叉路口”解决方案，能够车载传感器所不能覆盖的范围，也就是NLOS。

不同的是欧洲早在2011年就已经做了完整的技术规范。路侧传感器可以是摄像头、毫米波雷达或激光雷达。激光雷达最合适，因为能见度差的情况下反而是最易发生交通事故的时候。1550纳米波长的激光雷达几乎可以像毫米波雷达那样全天候工作，同时激光雷达的分辨率较高。

![image-20211207143146841](https://gitee.com/er-huomeng/img/raw/master/image-20211207143146841.png)

欧洲ITS整体框架

这其中承载整个系统的关键是LDM，即Local Dynamic Map。

![image-20211207143139073](https://gitee.com/er-huomeng/img/raw/master/image-20211207143139073.png)

典型LDM的4层结构，最上层基本就是V2X信息。欧洲ETSI在2014年对LDM做了详细标准，也就是ETSI EN302895 V1.1.1，车辆通讯基础应用设置之LDM。

