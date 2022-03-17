- [车路协同与5G、激光雷达、T-box关系网 (qq.com)](https://mp.weixin.qq.com/s/qbb8zVW1RsiaENm7byDKVw)

## 1 什么是“车路协同”？

车路协同是采用先进的无线通信和新一代互联网等技术，全方位实施车车、车路动态实时信息交互，并在全时空动态交通信息采集与融合的基础上，开展车辆主动安全控制和道路协同管理，充分实现人、车、路的有效协同，保证交通安全，提高通行效率，从而形成的安全、高效和环保的道路交通系统。

如果你觉得这个定义太复杂，那么我通俗的解释下：

**车路协同是将车与车、车与路的信息相连通。车可以将拥堵信息、实时路况等，传给交通控制中心；交通控制中心又可以将实时更新的信号灯数据、车流量信息、绿波信号、事故信息等，传给路上行驶的汽车。**

交通是一个动态变化的过程，为了达到合理配置资源、合理化规划的目的，必须实时不断地交换信息。

**V2X车联网技术支持道路交通安全类应用需要通过及时可靠的车—车、车—路通信将车辆的状态信息（特别是车辆的位置、速度、行驶方向信息）通知给周围的车辆，通过协作的方式来感知碰撞风险，所涉及的关键技术包括能够支持车辆在高速移动的环境下实时可靠通信的无线通信技术、车辆状态特别是车辆位置的感知技术、海量车辆状态数据处理分析技术。**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/xQlREtFaQSgq6TFDBG5rxulsVdFyPfSCakDLZp6fWghALSzA2yia7lSyMYlKkx6EVycRXk98ygybSDnu9DJzw3A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

*车与车之间（V2V）、车与路之间（V2I）、车与人之间（V2P）、车与网络之间（V2N）*

车与车、车与路之间的实时通讯，就可以尽量避免拥堵，尽量减少驾驶员急刹车等危险操作。只要合理控制行驶路线及速度，就能实现出行效率和安全的双重保障。

再举个例子：如果你驾车通过多个红绿灯路口，你一定希望预判到前方红绿灯的倒计时，同时，能够尽量赶上绿灯驶过最好。

车路协同出现以后，你的车辆能够显示前方路口信号灯颜色与倒计时。同时，车路协同也会尽量提供给你绿波信号，让你了解一路绿灯大概需要什么样的车速。

这是不是会增加你的幸福感，也会提升你的开车效率？

## 2 车路协同与5G

2020年9月，5G汽车联盟5GAA提出了C-V2X通信技术路线图：

5GAA大规模部署C-V2X通信技术路线图

![图片](https://mmbiz.qpic.cn/mmbiz_png/QOjQHZibD2yAMCLLpIcNKK1FywssKnnFyxgIH5119VFZ8tribtNN4VpVGCshdPY2peTZf0fLcZ6TUiaa9FzCibhKbg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

10月23日，湖南湘江新区智能系统测试区首次实现了基于5G的车路协同及车车协同的V2X应用测试，这在中南地区尚属首次。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/QOjQHZibD2yAMCLLpIcNKK1FywssKnnFyR1AWYN895jQKREInJ2KVJ608PCUlYrqXKMIBlia0Wy4FTJOiaYiaXnCRA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

*V2P行人检测场景演示*

本次测试由湖南湘江智能科技创新中心联合中国移动通信集团湖南有限公司长沙分公司、华为技术有限公司、长沙智能驾驶研究院共同进行。在测试区演示现场，记者观看了基于5G网络技术的智能网联汽车V2X应用场景演示，包括了前向碰撞预警、逆向超车预警、紧急制动预警、变更车道盲区预警和紧急车辆提醒、异常车辆提醒、行人检测预警、道路危险预警和车内标牌等多项场景演示。

此次演示验证了5G网络的大带宽和低时延的能力，通过5G技术在车联网领域的运用，能够帮助驾驶员规避危险，提升驾驶效率，也可以将数据上行传输以供智能网联汽车实现进一步的数据融合和协同控制。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/QOjQHZibD2yAMCLLpIcNKK1FywssKnnFy0ia1enmYjbsJ8HsXabibFn5OV6wg4FrV8r2aICvOcrictgAxtX8lZfiblQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

*本次测试由湖南湘江智能科技创新中心联合中国移动通信集团湖南有限公司长沙分公司、华为技术有限公司、长沙智能驾驶研究院共同进行*

## 3 车路协同与激光雷达

智能交通和智慧城市需要大量丰富准确全面的交通参与者实时信息，以确保道路交通安全。

激光雷达是一种利用红外激光来测距的主动传感器，通过主动发射激光探测，实时采集三维空间数据信息，而且可以基本无视外界环境的变化，测距精度高(±2cm~±3cm)，具有探测距离远、精度高、光线环境适应性好等优点。

相比其他传感器，激光雷达能更快速且准确的获取场景中的空间距离，速度，相对位移等信息。毫无疑问，融入激光雷达的车路协同路侧感知系统是突破毫米波+摄像头组合感知能力局限性的关键手段之一。

V2X中，激光雷达既可以应用于智能汽车，也可以应用于交通设施。为智能汽车配备支持车路协同应用的激光雷达，便可在驾驶车辆行进的过程中同时从各种其他来源（车、人、道路基础设施、网络等）收集信息，并通过智能车控系统将所得信息反馈至驾驶员，驾驶员可通过反馈信息提前做出预防措施，有效提升行驶安全性和交通效率。

为交通设施装配支持车路协同应用的激光雷达，使其具有“上帝视角“，实现城市交通动态精准感知与智能向导，相关数据分析，智慧交通可使车辆安全事故率降低20％以上，交通堵塞减少约60％，短途运输效率提高近70％，现有道路网的通行能力提高2—3倍。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/xQlREtFaQShJcU6WzN5wVwkzOEVyhILicIvSdjLlUicewmxib93jR6AW0M9JzGEEFlhPk3nNqicn8ycdSzfJEHkJbw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)



*激光雷达可以架设在路端，从较高位置监测道路环境*

目前激光雷达V2X已经应用广泛使用于公共交叉路口和高速公路。通过加装激光雷达和其他路侧感知设备，全维度还原路口信息，对该区域的行人、车辆进行感知识别，实时监测违法违章现象并发出碰撞预警，有效减少事故发生率，预防逃费套牌等违法违章现象。而在智能汽车上的激光雷达应用也已经通过在智能驾驶乘用车、商用车、物流车、机器人各应用领域的大量案例呈现了优异的应用效果。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/xQlREtFaQSgq6TFDBG5rxulsVdFyPfSCQ3qhiceU1G8yoDLDhlpgUupia2YRAk1ax1HBoh7qnnA17ECfXBQOsDbA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

*激光雷达可以安装在智能汽车中，进行实时信息交换*

## 4 车路协同与T-box

在车载智能终端方面，**V2X可以与车载娱乐系统TBOX融合，也可以与ADAS或自动驾驶平台融合**，不同的Tier1、主机厂已在开发相应产品，具体来看，C-V2X在硬件方面的产品形态包括：

C-V2X+T-BOX车载终端可以融合4G/5G模块、C-V2X模组、CAN控制器、GNSS等技术和产品，博泰推出了5G C-V2X T-BOX，采用华为MH5000模组，博泰从2009年开始就在通信模块上与华为形成深度合作，从最初的华为MU203模块一直到4G、4.5G C-V2X、5G C-V2X；2020年“新四跨”活动上，博泰车联网与华为、北汽等组成的演示车队完成了数十项V2I（车与路）、V2V（车与车）场景演示，**并展示了AR导航，ADAS高级驾驶辅助系统、高精度车道级导航地图等应用。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/QOjQHZibD2yAMCLLpIcNKK1FywssKnnFy5gWtwgYMbQhib71ALTdELxcX4Xr47lWDJN87HNUniceET1mAtEh857yA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

高集成的多合一智能天线，集成 GNSS定位模块+4G/5G+V2X 等，也可以考虑进一步集成UWB / WIFI / 蓝牙无钥匙进入等功能模块，2020年底上市的红旗E-HS9搭载了和东软联合研发的C-V2X智能天线。

“ETC+T-BOX+C-V2X”多合一终端，如千方科技在乘用车现有4G/5G T-Box平台上集成车规级ETC模组，C-V2X PC5模组，打通ETC、V2X与车载导航系统、ADAS系统连接。

AR导航和AR HUD技术将进一步增强ADAS、V2V和V2I通信技术的融合，将成为V2X的重要展示界面，长城WEY旗下“摩卡”已量产搭载了高通8155座舱芯片、5G+V2X和AR-HUD。

C-V2X还可以与自动驾驶域控制器融合，作为自动驾驶的冗余传感器。高通 Snapdragon Ride硬件堆栈由涵盖规划、定位（Qualcomm Vision Enhanced）、感知（摄像头、雷达、LiDAR、传感器融合，C-V2X），V2X软件支持基于SAE和ETSI标准的ITS协议栈，同时也支持第三方ITS协议栈。

![图片](https://mmbiz.qpic.cn/mmbiz_png/QOjQHZibD2yAMCLLpIcNKK1FywssKnnFy1e4hQkfuLeeKSvnLkxhzotj9XpeTMr6VEY9pocuLPDhNrUIl4ebvgQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

小结：总体而言，现阶段OEM厂商量产车型大多采用V2X模组与TBOX融合的技术方案，目前可以把5G+LTE-V2X+WiFi+GNSS功能集成在一个模组里，价格约2,000元左右；

未来价格将进一步下降至1,000-1,500元，基于R16/R17的5G NR 产品价格会略高一些。乐观预计到2025年国内乘用车前装C-V2X终端市场规模将超过100亿元人民币。