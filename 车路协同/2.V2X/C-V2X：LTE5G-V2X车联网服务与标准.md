C-V2X：LTE/5G-V2X车联网服务与标准：http://iov.sicrc.cn/index.php/archives/13.html

# 第一部分：DSRC与C-V2X标准化背景

## 1. 车联网标准化组织

- 国际：
  - IEEE（美国电气电子工程师学会）
  - ETSI（欧洲电信标准协会）
  - 3GPP（移动通信伙伴联盟）
  - ARIB（日本电波产业协会）
  - TTA（韩国电信技术协会）
  - IMDA（新加坡资讯通信媒体发展局）
  - 5GAA（5G Automotive Association）
  - ETSI（ETSI制定了基于DSRC的标准ITS-G5，同时作为3GPP的创建伙伴，ETSI也会从3GPP的技术标准成果中直接转化引用）
- 国内：
  - CCSA（中国通信标准化协会）
  - C-ITS（中国智能交通产业联盟）
  - SAE-China（中国汽车工程学会)
  - NTCAS（全国汽车标准化委员会）
  - TIAA（车载信息服务产业应用联盟）
  - TC/ITS（全国智能运输系统标准化技术委员会）
  - 全国道路交通管理标准化技术委员会
  - IMT-2020（5G）推进组C-V2X工作组
  - CAICV（中国智能网联汽车产业创新联盟）

## 2. DSRC标准背景

**DSRC（Dedicated Short Range Communications，专用短程通信技术）**

2004年开始标准化，由IEEE基于WIFI制定，协议族包括：

- IEEE 802.11p，定义DSRC物理标准
- IEEE  1609，车载环境无线接入标准系列（WAVE），定义网络架构和流程
- SAE J2735和SAE J2945，定义消息包中携带的信息，主要是汽车上的传感器信息，例如位置、行进方向、速度和刹车信息等

DSRC协议族：

![DSRC协议族.jpg](http://iov.sicrc.cn/usr/uploads/2020/02/2235718831.jpg)

DSRC的主要支持方式美国高速公路安全管理局（NHTSA），其目标是：

- 安全方面，中轻型车辆将避免80%的交通事故，重型车避免71%的事故
- 效率方面，交通堵塞将减少60%，短途运输效率提高70%，现有道路通行能力提高2~3倍
- 便捷方面，停车次数可减少30%，行车时间降低13%至45%，实现降低油耗15%

美国希望在2021年达到50%新车安装DSRC，2022年达到75%新车安装DSRC，2023年开始100%新车安装DSRC。DSRC经过多年的测试与验证，可行性得到验证，同时网络、芯片等产业链相对成熟。

## 3. C-V2X标准背景

**C-V2X（Cellular-Vehicle-to-Everything，基于蜂窝技术的车联网通信）**

2015年开始标准化，由3GPP基于LTE制定，协议族包括：

- 3GPP SA1，业务需求
- 3GPP SA2，系统架构
- 3GPP SA3，安全
- 3GPP RAN，空口技术

标准化阶段：

- 第一阶段（LTE-V2X）：2017 年 3 月完成，对应LTE Rel-14版本 。面向基本的道路安全业务的通信需求，引入了工作在 5.9GHz 频段的

  直通链路（ PC5 接口）

  模式和

  公众移动蜂窝网 （Uu 接口）

  模式。

  - **PC5模式：**称为Sidelink（侧行链路或直通链路），用于车-车通信（V2V），车-路边基础设施通信（V2I），车-人通信（V2P），工作于专用频段；
  - **Uu模式：**包括Uplink和Downlink（上下行链路），用于车-网络/云通信（V2N/V2C），工作于运营商蜂窝网络频段。

- 第二阶段（LTE-eV2X）：2018 年 6 月完成，对应LTE  Rel-15版本。基于LTE技术满足部分5G-V2X增强业务需求（LTE-eV2X），主要是在 PC5  接口引入了载波聚合、高阶调制等技术以提升数据速率、并引入可降低时延的部分技术。 3GPP Release 15 的 5G  标准重点针对增强移动宽带场景，没有对 V2X 业务进行针对性设计和优化。

- 第三阶段（5G V2X）：基于5G  NR（5G新空口）技术实现全部或大部分5G-V2X增强业务需求，对应5G NR Rel-16，Rel-17版本。3GPP Release 16  于2019 年 3 月完成完成了 NR-V2X 的研究课题，重点是面向高级 V2X 业务的需求，研究基于 5G NR 的 PC5 接口技术和对  Uu 接口的增强，并开始 NR-V2X 标准化立项。主要标准化内容包括：

  - 基于 PC5 和 Uu 接口支持高级 V2X 业务；
  - 支持 LTE-V2X 和 NR-V2X 共存
  - PC5 接口支持单播、组播和广播三种模式， 以提供支撑不同业务的能力；
  - 支持 In-Coverage， Partial-Coverage 和 Out-of-Coverage；
  - 基于通用的架构支持直通链路在中低频和毫米波频段工作；
  - Uu 接口网络引入 V2X通信切片、边缘计算、 QoS 预测等特性，以满足车联网低时延、高可
    靠性、大带宽等需求

目前已经完成Rel-14 LTE-V2X和Rel-15 LTE-eV2X，正在进行5G NR Rel-16制定和Rel-17规划。

![3GPP_5G_V2X_Standard.png](http://iov.sicrc.cn/usr/uploads/2020/02/19407425.png)

目前涉及的5G V2X相关工作项目：

| **名称**                                                     | **特性及版本**                                              |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| Support  for V2V services based on LTE sidelink  (LTE_SL_V2V) | Rel-14  RAN work item on V2V services based on LTE sidelink |
| LTE-based  V2X Services (LTE_V2X)                            | Rel-14  RAN work item on LTE-based V2X                      |
| V2X  phase 2 based on LTE (LTE_eV2X)                         | Rel-15  RAN work item on LTE-based V2X enhancement          |
| Study  on Enhancement of 3GPP support for V2X services (FS_eV2X) | Rel-15  SA1 study item on eV2X service requirements         |
| Enhancement  of 3GPP support for V2X scenarios (eV2X)        | Rel-15  SA1 work item on eV2X service requirements          |
| Study  on evaluation methodology of new V2X use cases (FS_LTE_NR_V2X_eval) | Rel-15  RAN study item on eV2X evaluation methodology       |
| Study  on Improvement of V2X Service Handling (FS_V2XIMP)    | Rel-16  SA1 study item on eV2X service requirements         |
| Improvement  of V2X service Handling (V2XIMP)                | Rel-16  SA1 work item on eV2X service requirements          |
| Study  on architecture enhancements for 3GPP support of advanced V2X services  (FS_eV2XARC) | Rel-15/16  SA2 study item on eV2X architecture              |
| Architecture  enhancements for 3GPP support of advanced V2X services | Rel-16  SA2 work item on eV2X architecture                  |
| Study  on NR Vehicle-to-Everything (FS_NR_V2X)               | Rel-16  RAN study item on NR V2X feasibility                |
| 5G  V2X with NR sidelink（5G_V2X_NRSL）                      | Rel-16  RAN work item on 5G V2X with NR sidelink            |

2018年4月在华盛顿召开的5GAA会议上，福特发布了与大唐、高通的联合测试结果，给出DSRC和LTE-V2X实际道路测试性能。结果显示，在相同的测试环境下，通信距离在400米到1200米之间，LTE-V2X系统的误码率明显低于DSRC系统，而且C-V2X的通信性能在可靠性和稳定性方面均明显优于DSRC。基于此，福特最终放弃DSRC而选择C-V2X。

C-V2X包含Rel-14 LTE-V2X、Rel-15 LTE-eV2X和向后演进的NR-V2X，从后继演化角度看也比DSRC有明显优势。

## 4. 我国标准化进展

我国LTE-V2X相关空口、网络层、消息层和安全等核心技术标准已制定完成，标准体系初步形成。2018年11月，四标委签署了《关于加强汽车、智能交通、通信及交通管理C-V2X标准合作的框架协议》，加快LTE-V2X标准在汽车、交通、公安行业的应用。

| 分类         | 标准名称                                               | 标准类别         | 标准组织                | 升国标建议组织   |
| ------------ | ------------------------------------------------------ | ---------------- | ----------------------- | ---------------- |
| 总体         | 基于LTE的车联网无线通信技术 总体技术要求               | 行标、国标       | CCSA                    | 通标委           |
| 接入层       | 基于LTE的车联网无线通信技术 空口技术要求               | 行标、国标       | CCSA                    | 通标委           |
| 网络层       | 基于LTE的车联网无线通信技术 网络层技术要求             | 团标、行标、国标 | C-ITS、CCSA             | 通标委           |
| 消息层       | 基于LTE的车联网无线通信技术 消息层技术要求             | 团标、行标、国标 | C-ITS、SAE-C、CCSA      | 通标委           |
| 安全         | 基于LTE的车联网无线通信技术 安全技术要求               | 行标、国标       | CCSA                    | 通标委           |
| 安全         | 基于LTE的车联网无线通信技术安全证书管理系统技术要求    | 行标、国标       | CCSA                    | 通标委           |
| 应用（系统） | 基于LTE-V2X直连通信的车载信息交互系统技术要求          | 团标、国标       | SAE-C、C-ITS、SAC/TC114 | 汽标委           |
| 应用（系统） | 基于LTE-V2X直连通信的路侧单元系统技术要求              | 团标、国标       | SAE-C、C-ITS            | 交通/公安        |
| 应用（系统） | 面向LTE-V2X的多接入边缘计算 业务架构和总体需求         | 行标、国标       | CCSA                    | 通标委           |
| 应用（系统） | 面向LTE-V2X的多接入边缘计算 服务能力开放和接口技术要求 | 行标、国标       | CCSA                    | 通标委           |
| 功能应用     | 十字交叉路口预警、车辆编队行驶等功能应用               | 行标、国标       | 汽标委/交通/公安        | 汽标委/交通/公安 |

# 第二部分：C-V2X发展现状

## 1. 频点分配

**全球主要国家和地区已经分配了V2X（DSRC和C-V2X）通信工作频段：**

- 美国：5850-5925MHz，共75M带宽；1999年，FCC为IEEE 802.11p分配了7个信道（10MHz/信道）频率。
- 欧盟：5795-5805MHz，共10M带宽；2002年，ECC给车对路系统分配10MHz，有需要可扩展至5815MHz。
- 欧洲：5855-5925MHz，共70M带宽；2019年，非安全类Road ITS应用分配20MHz（5855-5875MHz），安全类ITS应用分配40MHz（Road ITS使用5875-5915MHz，Rail  ITS使用5915-5925MHz ，另外5925-5935MHz扩展用于Rail ITS）
- 日本：5770-5850MHz，共80M带宽；90年代末分配给DSRC，2012年另外划分755.5-764.5MHz（9MHz）给ITS道路安全应用。
- 韩国：5855-5925MHz，共70M带宽；2016年分配给802.11p。
- 新加坡：5875-5925MHz，共50M带宽；2017年分配给ITS。
- 中国：5905-5925MHz，共20M带宽。2018年分配给LTE-V2X。

## 2. 技术趋势

### 2.1 DSRC与C-V2X技术对比

从技术上，LTE-V2X比DSRC有明显优势。

![DSRC-LTEV-5G技术对比.png](http://iov.sicrc.cn/usr/uploads/2020/02/3925054252.png)

参考文献：陈山枝,胡金玲,时岩,赵丽.LTE-V2X车联网技术、标准与应用[J].电信科学,2018,34(04):1-11.

### 2.2 DSRC与C-V2X的商业趋势对比

[《5G车联网十大产业化趋势》](http://mp.weixin.qq.com/s?__biz=MzU3Mzk2ODczNw==&mid=2247483844&idx=1&sn=b6c1e352906519040ddd36b90fe6c5c7&chksm=fd38d9caca4f50dcab6871cface62947ef60c1be0b48938cb863da696562e1b8777c8afe0430&scene=21#wechat_redirect)文章对C-V2X商用进程做了预测：

- 基于LTE-V2X的车联网商用进程：2018年进行规模试验，2019年进行预商用测试，2020年正式迈入车联网（LTE-V2X）商用元年；
- 基于5G NR的车联网商用进程：2019年进行5G NR Uu技术试验，2020年进行5G NR PC5技术试验，2021年进行预商用测试，2022年正式迈入5G NR-V2X商用元年。

![DSRC-LTEV-5G技术对比.jpg](http://iov.sicrc.cn/usr/uploads/2020/02/983302968.jpg)

目前关于车联网的运营模式还不太清楚，各个企业都在进行实践。信通院在[《C-V2X业务演进白皮书》](http://www.caict.ac.cn/kxyj/qwfb/bps/201911/P020191104336556097939.pdf)中提出的车联网业务参与方能够提供的基础支撑能力主要包括：

|       业务应用参与方       |                  网联通信与网联协同智能支撑                  |                      道路感知与控制支撑                      |              业务流与数据支撑              |
| :------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------: |
|     通信运营商和供应商     | 提供基于CV2X和5G的“车-路-云”网联通信能力和网联协同智能计算能力（即MEC端的计算服务支撑和云端计算服务支撑） |                                                              | C-V2X网联相关数据，MEC业务使能平台相关数据 |
|        智能交通企业        |                                                              | 提供智能路侧设备RSU端的服务能力，包括智能路侧设备结合MEC平台提供的本地感知数据处理，制定本地交通策略的能力，智能路侧设备提供的道路交通状态感知能力等 |             道路以及交通大数据             |
| 自动驾驶平台与应用软件企业 |                                                              |                                                              |    算法平台，应用数据平台，业务应用软件    |
|          汽车厂商          |                                                              |                                                              |    汽车总线数据、车载数据服务平台(TSP)     |

**智能交通企业是车路协同相关应用的重要数据提供方和智慧道路建设和运营方。随着“智慧道路”逐步落地和MEC的引入，智能路侧设备作为C-V2X业务演进的重要载体，与人、车、路、交通数据中心协同，可以提供更加丰富和实时的道路静态和动态数据：例如各种感知信息（摄像头信息、路侧雷达信息、车端信息等）。结合交通管理中心下发的交通管理信息（例如交通管理数据库、交通违章数据库、高速公路管理数据库等）等还能够支持更丰富的安全、效率类业务。**  

在这里面，基于DSRC和C-V2X的路侧设备到底应该怎么运营，尚无法解决。

### 2.3 智能网联车分级

《[C-V2X 产业化路径和时间表研究](http://www.caicv.org.cn/index.php/newsInfo/downLoad?id=2301)》中定义的智能网联汽车网联化等级。

2019年12月由中国智能网联汽车产业创新联盟，IMT-2020（5G） 推进组 C-V2X 工作组，中国智能交通产业联盟，中国智慧交通管理产业联盟联合编写。  

| 网联化等级 | 等级名称           | 等级定义                                                     | 典型信息                                                     | 传输需求                   | 典型场景                                     | 车辆控制        |
| ---------- | ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------------- | -------------------------------------------- | --------------- |
| 1          | 网联辅助信息交互   | 基于车-路、车-云通信，实现导航、 道路状态、交通信号灯等辅助信息的获取以及车辆行驶与驾驶人操作等数据的上传 | 地图、交通流量、交通标志、油耗、里程等静态信息               | 传输实时性、可靠性要求较低 | 交通信息提醒、车载信     息娱乐服务、eCall等 | 人              |
| 2          | 网联协同感知       | 基于车-车、车-路、车-人、车-云通信，实时获取车辆周边交通环境信息，与车载传感器的感知信息融合，  作为自车决策与控制系统的输入 | 周边车辆/行人/非机动车位置、信号灯相位、道路预警等动态数字化信息 | 传输实时性、可靠性要求较高 | 道路湿滑提、紧急制动预警、特殊车辆避让等     | 人/自车         |
| 3          | 网联协同决策与控制 | 基于车-车、车-路、车-人、车-云通信，实时并可靠获取车辆周边交通环境信息及车辆决策信息，车-车、 车-路等各交通参与者之间信息进行交互融合，形成车-车、 车-路等各交通参与者之间的协同决策与控制 | 车-车、车-路、车-云间的协同控制信息                          | 传输实时性、可靠性要求最高 | 列队跟驰等                                   | 人/自车/他车/云 |

## 3. 业务形态

### 3.1 3GPP LTE-V2X定义的场景

3GPP发布了对LTE-V2X定义的27种场景（3GPP TR 22.885）。

| 缩写 | 含义                                |
| ---- | ----------------------------------- |
| CACC | Corporative Adaptive Cruise Control |
| HV   | Host Vehicle                        |
| ITS  | Intelligent Transport Systems       |
| RV   | Remote Vehicle                      |
| RSU  | Road Side Unit                      |
| TTC  | Time to Collision                   |
| V2I  | Vehicle-to-Infrastructure           |
| V2N  | Vehicle-to-Network                  |
| V2P  | Vehicle-to-Pedestrian               |
| V2V  | Vehicle-to-Vehicle                  |
| V2X  | Vehicle-to-Everything               |
| VRU  | Vulnerable Road User                |

#### 3.1.1 LTE-V2X场景

1. **Forward Collision Warning（FCW）：**碰撞提醒

   The FCW application is intended to ***warn the driver of the HV in case of an impending rear-end collision with a RV ahead in  traffic in the same lane and direction of travel\***. Using  the V2V Service, FCW is intended to help drivers in avoiding or  mitigating rear-end vehicle collisions in the forward path of travel.

2. **Control Loss Warning（CLW）：**失控提醒

   The CLW application ***enables a HV to broadcast a self-generated control loss event to surrounding RVs.\*** Upon receiving such event information, a RV determines the relevance of the event and provides a warning to the driver, if appropriate.

3. **V2V Use case for Emergency  Vehicle Warning（EVW）：**紧急车辆提醒

   Emergency vehicle warning service enables each vehicle to ***acquire the location, speed and direction information of a surrounding emergency vehicle\***  (e.g. ambulance) to assist safety operation like allowing ambulance path to get free.

4. **V2V Emergency Stop Use Case（ES）：** 应急停车

   This use case describes vehicles V2V communication used in case of ***emergency stop\*** to ***trigger safer behaviour for other cars\*** in proximity of the stationary vehicle. 

5. **Cooperative Adaptive Cruise  Control（CACC）：**加入或退出车队

   This use case describes the scenario whereby a vehicle with V2V capability ***joins and leaves a group of corporative-adaptive-cruise-control (CACC) vehicles\***. This provides convenience and safety benefits to participating vehicles and also has societal benefits to improve road congestion and fuel  efficiency.

6. **V2I Emergency Stop Use Case（ES）：**RSU发送应急停车

   This use case describes V2I communication where ***a Service RSU notifies vehicles in vicinity in case of emergency stop to trigger safer behaviour\***.

7. **Queue Warning（QW）：**排队提醒

   In a lot of situations, a queue of vehicles on the road may pose a  potential danger and cause delay of traffic, e.g. when a turning queue  extends to other lanes. Using the V2I Service, ***the queue information can be made available to other drivers beforehand\***. This minimizes the likelihood of crashes and allows for mitigation actions.

8. **Road safety  services（RSS）：**RSU转发道路安全报文

   V2X messages are delivered from one UE supporting V2I Service to  other UEs supporting V2I Service via an RSU which may be installed on  the road side.
   ***The RSU receives V2X messages transmitted  from UEs supporting V2I Service and transmits the received V2X messages  to UEs within a local area.\***
   A UE receives V2X messages  transmitted by the RSU. After processing the received V2X messages, the  UE notifies the driver of relevant information. 

9. **Automated Parking System（APS）：**停车推荐

   The Automated Parking System (APS) contains a database which provides real-time information to vehicles in a metropolitan area on  availability of parking spots, be it on the street or in public parking  garages. Connected vehicles help maintain the real-time database of the  occupancy of parking spaces, which can be accessed by means of  smartphones and connected vehicles. APS allows a driver to reserve an  available parking space, be guided to it via a navigation application,  and make a hands-free payment for parking.

10. **Wrong way driving warning（WWDW）：**开错路

    This use case describes V2V communication used between 2 vehicles driving in ***opposite directions\*** warning wrong way driving and trigger safer behaviour for cars in proximity. 

11. **V2X message  transfer under MNO control：**V2V转发V2X报文

    This use case describes the scenario where a given UE supporting V2V  Service sends V2X messages to other surrounding UEs and the given UE is  under E-UTRAN coverage.

12. **Pre-crash Sensing Warning（PSW）：**事故告警

    The pre-crash sensing warning application provides warnings to vehicles in imminent and unavoidable collision by ***exchanging vehicles attributes after non-avoidable crash is detected\***.Vehicle A and Vehicle B are supporting V2X Service and can communicate with each other using V2V Service.

13. **V2X in areas  outside network coverage：**V2X转发LTE

    This use case describes V2X communication when one or more vehicles  are located in an area not served by E-UTRAN which supports V2X Service. 

14. **V2X Road safety service via infrastructure：RSU检测道路安全事件**

    This use case describes the scenario where infrastructure nodes such as ***RSUs and traffic safety servers generate and distribute traffic safety-related messages for road safety\***. 

15. **V2N  Traffic Flow Optimisation：交通流优化**

    This use case describes vehicles V2N (Vehicle-to-Network)  communication to a centralised ITS server referred here to as “entity”  to optimise traffic flow when approaching intersections. This use case  addresses the situation when approaching the vehicle has to stop even  though there are no other cars around at an intersection or has to slow  down because of explicit traffic lights signal absence. Depending on the traffic situation which is based on ***the vehicles’ periodically transmitted messages this entity will provide\***, via LTE network entity, ***a green light to a car when approaching the intersection and an  indication of speed at which the green light will be met without having  to stop or miss the green light phase\***. 

    To enable this information about vehicles approaching traffic lights  has to be made available well in advance i.e. in most cases beyond ProSe range. When coming in ProSe range communication might be switched from  network to direct communication, if deemed useful.

    Compared to V2V communication within ProSe range the delay and  latency requirements are more relaxed due to the longer distances and  the non-safety related nature of this use case. 

16. **Curve Speed Warning（CSW）：**

    Curve speed warning application alerts the driver to manage the curve at an appropriate speed.

17. **Warning to Pedestrian  against Pedestrian Collision：行人碰撞预警**

    This use case is to provide information to vulnerable road users,  e.g. pedestrian or cyclist, of the presence of moving vehicles in case  of dangerous situation. As a result, ***warnings are provided to vulnerable road users to avoid collision with the moving vehicle\***.

18. **Vulnerable Road User (VRU) Safety：弱势交通群体**

    This use case describes the scenario whereby a vehicular and a  pedestrian are both equipped with V2P capabilities, and the vehicle  detects the pedestrian’s presence and alerts the driver, if an imminent  threat is present. This capability extends the safety benefit of V2X to  pedestrians and other vulnerable road users, e.g. bicyclists, wheelchair users, etc. 

19. **V2X by  UE-type RSU：**

    This use case describes the scenario where UE supporting V2X discovers and communicates with UE-type RSU. 

20. **V2X Minimum QoS：**

    This use case describes the scenario where E-UTRA(N) resource is not  enough for every UEs 10 Hz V2X message transmission. In addition, this  use case includes the scenario where emergency vehicle is supported. 

21. **Use case for V2X access when  roaming：**

    Mary is taking a road trip across the country. She has a car equipped with V2X capability, with service from her home network operator. On  her journey, Mary encounters a traffic jam in town not served by her  home network provider. The town has deployed V2X capabilities to  redirect traffic jams caused by a major infrastructure construction  project. The V2X capabilities must be able to communicate with devices  associated with multiple service providers.

22. **Pedestrian Road Safety via V2P awareness messages：**

    A pedestrian carries a UE, which is able to transmit awareness and  safety related V2P broadcast messages. There are two possible  approaches. 

    \-  Approach 1: The pedestrian UE performs risk assessment. (see use  case 5.18 Vulnerable Road User (VRU) Safety). The pedestrian UE sends a  notification message with position and speed to the vehicle in case of  danger. 

    \-  Approach 2: The pedestrian UE broadcasts itself awareness messages regarding location and speed. Risk assessment is performed by the  Vehicle UE. This approach is described in this Use Case.

23. **Mixed Use  Traffic Management：混合交通管理**

    There are a number of variables to be taken into account in a  scenario involving different types of vehicular traffic. The optimal  coverage range and frequency of message transmission depends on several  factors, including the relative velocity of the UEs, potential reaction  time of the various transportation modes (e.g., automobile, train,  bicycle, and pedestrian), traffic density, and any environmental  conditions. A V2X system would need the flexibility to adapt to changing attributes such as vehicular traffic density, rates of speed, angles of approach, and weather conditions which all may impact the optimal range and transmission rate in a specific situation. 

24. **Enhancing Positional Precision for traffic  participants：增强的交通参与者位置**

    To obtain their position vehicles usually use a GNSS such as GPS,  Galileo, Beidou, and Glonass. However, the publicly available precision  for a position fix for the most common system GPS is just around 15 m,  better values can be obtained and dependent on the radio conditions and  are thus not guaranteed.

    To compensate (or better: hide) this shortcoming navigation systems  use the geographical map they need anyhow for routing and match the  position fix with the nearest road and also average and extrapolate  position fixes over time.

    For assisted driving and even more autonomous driving this situation  is not acceptable, for both it would be good for the car to know whether it is in the middle of a lane with only an uncertainty of a few  centimeters.

25. **Privacy in the V2V communication environment：**

    The privacy or anonymity in the V2V communication environment is a  requirement deemed very important for user adoption of the V2V system.  Privacy refers to two aspects:

    \- prevention of association of certain vehicle (or driver) as seen by an observer and the safety messages it actually broadcasts.

    \- prevention of tracking of the journey of a certain vehicle between two geographical points.

26. **V2N Use Case  to provide overview to road traffic participants and interested  parties：为道路交通参与者提供路面状况**

    This use case describes a general use case for V2N communication that exercises the strength of 3GPP networks of providing excellent  coverage. In this use case, the existing eNb infrastructure is being  used to give road traffic participants (RTP) a field of view beyond what V2V, even in combination with RSUs, could provide.

    This use case will supplement V2V direct communication, which will be used in parallel and will be the only means of communication e.g. in  case there is no network coverage. In the use case described here each  road traffic participant (RTP), sends the CAM/DENM messages also to an  entity in the network - the road traffic server (RTS). The RTS could be  centralised, covering an entire country or decentralised, overlooking  only a small geographical area or a combination of both. If  decentralised, RTS need to communicate between each other but this is  out of scope for 3GPP.

27. **Remote diagnosis and just in time repair notification：**远程诊断

    A road side unit (RSU) having the capability to access an internet  will enable any passing by vehicle to report about its current  functional state to a local/remote diagnosis center and to receive “Just in time repair notification” if having subscribed to such service. A  Vehicle Service Centre located at the Car Repair Center needs to obtain  and analyze data from the vehicle periodically. Based on the analysis  result, it will notify to the vehicle owner showing what’s going on with the vehicle —in simple language and images together with some  maintenance suggestions. Also the Vehicle owner also has the ability to  initiate the data information collected to be wiped from the Repair  Centre. This will reduce the risk of vehicle failure while optimizing  the vehicle checks only when necessary, it also allows the Vehicle owner to still have control over their data.

#### 3.1.2 LTE-V2X场景分类

参考文献：李凤,房家奕,赵丽.3GPP LTE-V2X标准进展及技术介绍[J].电信网技术,2016(06):40-45.

![LTE-V2X_SA1规范.png](http://iov.sicrc.cn/usr/uploads/2020/02/46488261.png)

**这些场景中，大部分是V2V场景，依赖RSU边缘或服务端的并不多。另外定义的各种V2P的目前暂时还很难实现。**

其中定义的V2I和V2N的有一些可以借鉴。

### 3.2 3GPP 5G-V2X定义的场景

5G-V2X定义了25种（3GPP TR 22.886）应用场景。

#### 3.2.1 5G-V2X场景

1. **eV2X support for vehicle platooning：车列**

   车列是以紧密联系的方式操作一组车辆，使得该组车辆就像是彼此间有虚拟的绳子连接一样呈现出与火车类似的方式运动。  为了保持车辆之间的距离，车辆需要共享诸如速度、朝向、目的（比如刹车，加速）等的状态信息。通过车队的方式，总体的车辆距离减小了，整体油耗降低，并且需要的司机数量也可以减少。

   当车队以100km / h行驶时，车辆在36ms内移动1米。

   正常密度车队的车辆之间距离可能大于2米，考虑到往返时间和处理延迟，消息传输频率高达40Hz，应支持消息大小为300-400字节左右的25ms端到端延迟。

   高密度车队车辆之间的距离为1米，考虑到往返时间和处理延迟，消息传输频率高达100Hz，应该支持消息大小为50-1200字节左右，至少延迟10ms。

2. **Information exchange within platoon：车列内信息交流**

   车列管理者应实时更新小组成员上报的周边交通数据，并上报给RSU，并实时接收RSU信息，包括路况和远处的交通信息，并与车队成员分享。  所有车列成员也可以通过V2V共享该组内的信息。 所获得的所有信息将被用于构建高精度的动态驾驶地图。  车辆之间的信息交换可以看作是新型的“问答”方式。

3. **Automotive: sensor and state map sharing：传感器和状态图共享（SSMS）**

   可以共享原始或已处理的传感器数据，以建立集体态势感知。

   这个概念是在ETSI和ISO技术报告和标准中的局部动态映射的扩展，主要区别在于更高的时空保真度，基于低延迟通信服务支持高精确定位和控制。例如合作驾驶（车队），面向所有道路参与者的交叉路口安全服务——包括行人和紧急车辆通信。对于这些用例，高度分辨的传感器图像不一定需要被传输（参见[8]，其中智能节点执行机载处理和数据交换以获得共享或融合态势感知，于是车辆自主执行推理或战术机动规划操作）;然而，由于大量不同的连接传感器，预计SSMS需要大量的数据带宽。

   ***传感器和状态图共享可能是对自动驾驶或高级辅助驾驶是有用的，具体内容得跟车企协调\***

4. **eV2X support for remote driving：远程驾驶的eV2X支持**

   远程驾驶是一个概念，在这个概念中，车辆由人工操作员或云计算远程控制。

   自主驾驶需要大量的传感器和像对象识别这样复杂的算法，而使用通过人类远程操作的远程驾驶则能够使用少量的相同资源。

   ***针对远程驾驶，目前的观点是可能有价值，但是在开放道路环境下可能并不可控，目前的网络延迟还是太大，且存在可能被人盗用的风险。也许在专用环境下可行，比如租车？危险环境的驾驶？\***

5. **Automated cooperative driving for short distance grouping（CoSDG）：自动化合作驾驶**

   自动合作驾驶比Rel-14 V2X中描述的合作自适应巡航控制（CACC）要求更多的自动化。  CACC提供对车辆运动的纵向控制，而驾驶员仍然负责转向控制。  CACC是SAE（汽车工程师协会）[38]和NHTSA（美国国家高速公路交通安全管理局）自动驾驶规模[39]的一级自动化实例;或者由BASt。（德国联邦公路研究院）称为“辅助驾驶”，SAE也称为“驾驶员辅助”。自动合作驾驶提供“更紧密”或更低等待时间的纵向控制，使领导者能够与一组车辆进行通信和协调，从而实现紧密的跟随。此外，自动合作驾驶可能会增加横向控制或更高级别的自动化能力。自动化合作驾驶概念框架允许在不需要驾驶员干预的情况下创新地使用通信接入来解决复杂的道路交通情况。因此，自动协作驾驶使SAE 2级至5级自动化成为可能（[10]，[38]）。

   合作短距离分组（CoSdG）指的是车辆之间的距离非常小的情况（比如卡车），它创造了一种合法的追尾形式。时间间隔的距离可以等效为0.3s甚至更短，在80km / h时导致车辆之间的距离接近6.7m  [10]。先进的自动化协同驾驶技术与高度可靠的无线车对车通信系统相结合，可以实现低延迟的数据传输，从而使得超近距离的驾驶成为了可能。

   CoSdG与[12]中总结的当前车队实现不同，其中ITS-G5已经成功用于各种传输速率（10 - 50 Hz）。 CoSdG设想更紧密的间距和更低的延迟，使用可替代的技术可靠地完成任务。因此，CoSdG将显著改善线路的稳定性，效率和最终的安全性。

   ***感觉和车列没有本质不同\***

6. **Collective perception of environment（CPE）：协同式环境感知**

   车辆可以在相邻区域中彼此交换实时信息（基于车辆传感器信息或来自有能力的UE型RSU的传感器数据），可以增强对车辆周围环境的感知以避免事故[15]。

   高车辆密度场景下认为每公里有9840辆车（如美国高速公路上拥挤的交通道路——每方向5车道或每公路10车道，高达3条高速公路相互交叉的情况下）。

   信息特点：

   - 信息流量至少应包含1600个有效负载字节，以便传输与10个检测对象有关的信息，以支持来自本地环境感知的信息以及与实际车辆状态有关的信息[16]。
   - 信息应能通过多台其他车辆跟踪环境的变化情况，重复频率至少为5-10 Hz [16]。更新率被选择得足够高，使得车辆速度向量在更新之间不会变化太快。每辆车产生的信息必须传输到指定范围内的所有邻近车辆（城市50米，农村500米，公路1000米）[16]。

7. **Communication between vehicles of different 3GPP RATs：**为非5G V2X设备车辆共享

   根据原始设备制造商的选择，有些车辆配备仅支持LTE的模块，其他车辆可能配备支持NR（New Radio）的模块。 如果支持NR的车辆不能与支持LTE的车辆通话，则支持LTE的车辆可以被视为不具有V2X能力的另一车辆。

8. **Multi-PLMN environment：**多PLMN网

   多个不同运营商网络。

9. **Cooperative collision avoidance (CoCA) of connected automated vehicles(CoCA)：合作避撞**

   为了使车辆能够更好地评估事故发生的可能性，并协调除常规CAM、DENM安全信息、传感器数据、动作列表如刹车和加速指令之外的机动动作，车辆之间会交换横向和纵向控制指令来通过3GPP V2X通信进行交通流的应用层面协调。

   - 10Mbps的吞吐量[36]，以在邻近的UE之间交换CoCA应用消息从而在交叉点处执行协调的驾驶操纵。
   - 根据涉及的车辆数量，消息大小可达2 kB [37]，用以交换车辆之间的预先规划的轨迹信息
   - 在CoCA申请期限内进行常规机动协调的时间少于10 ms [2]。
   - 安全协调驾驶机动的可靠性可达99.99％[2]。 

10. **Information sharing for partial/conditional automated driving：部分/有条件的自动驾驶信息共享**

    信息共享包括协作感知和协作控制。

    - 协作感知：使用V2X通信共享本地感知数据（抽象数据和/或高分辨率传感器数据），以扩大车载传感器可检测范围的能力。在这里，每个车辆和/或RSU把其自己来自本地传感器（例如，相机，LIDAR，雷达等）的感知数据与接近的车辆共享。
    - 协作控制：共享粗略的驾驶意图（例如，在[x，y，z]处在T秒内改变车道或移动/停止/停车）以改变车道，在高速公路和环形交叉路口并道，穿过4向停车标志并通过V2X在所有相关车辆中达成共识。

    基本需求包括：

    - 数据速率：每个链路的协作感知速率为0.5 Mbps（60字节/对象，100个对象，10消息/秒）。 协作控制则是每个链路0.05 Mbps（几百个字节（例如500字节）/消息，10个消息/秒）。
    - 使用广播或多播，假定是周期性的（或事件触发的），低延迟的（100ms）
    - 相对车辆速度：城市：[0-100] km / h，郊区：[0-200] km / h，高速公路 ：[0-250]公里/小时（相同方向）
    - 在UE和RSU之间相对车速：城市：[0-50] km / h，郊区：[0-100] km / h，高速公路：[0- 250]公里/小时（相同方向）

11. **Information sharing for high/full automated driving：完全自动驾驶信息共享**

    数据速率：

    - 协作感知为每个链路50 Mbps（H.265 / HEVC HD摄像机〜10 Mbps + LIDAR〜35 Mbps（6个垂直角度，64个元素，[10] Hz水平旋转）+其他传感器数据）
    - 协作控制为每个链路3Mbps（计划轨迹〜2.5 Mbps（32字节/坐标，10 ms分辨率，10秒轨迹，[10]信息/秒）+其他意图数据）

12. **Information sharing for partial/conditional automated platooning：部分/有条件的车列信息共享**

    数据速率：

    - 协作感知每个链路2.5Mbps（60字节/对象，100个对象，50消息/秒） 
    - 协作控制每链路0.25 Mbps（几百个字节（例如，500字节）/消息，[50]个消息/秒）

13. **Information sharing for high/full automated platooning：完全自动驾驶车列信息共享**

    数据速率：

    - 协作感知为每个链路50 Mbps，需要考虑是否需要更高数据速率的消息，而不是全自动驾驶50Mbps所需的消息
    - 协作控制每链路15Mbps（计划轨迹〜12.5Mbps（32字节/坐标，10ms分辨率，10秒轨迹，[50]消息/秒）+其他意图数据）

14. **Dynamic ride sharing：**动态座位共享

    这种用例可以使车辆发布愿意与其他乘客共享座位，以及行人表示愿意乘坐拼车的旅行意向。车辆可以共享自己的信息，如当前已有乘客数量、空余座位、目的地、预计到达时间、间隔站等。行人可以共享自己的信息，例如目的地、一些个人信息和凭证等。

    两个参与者可以决定是否适合乘坐共享，并提出任何正面的调查结果，行人和/或司机。这种场景可以基于私家车辆、汇集、私人专用出租车、出租车、公共交通、校园交通或其他形式的动态座位共享。

    ***这个更倾向与共享租车类的应用，更适合移动互联网\***

15. **Use case on multi-RAT：**多接入点

    5G是支持多接入点的，这个跟业务没什么大关系

16. **Video data sharing for assisted and improved automated driving (VaD)：视频数据共享**

    驾驶员的视觉范围是在一些道路交通状况会受限，例如前方有卡车驾驶[ 26 ]。从一辆车向另一辆车发送的视频数据可以用于在这种需要保障安全情境下提醒司机。视频数据收集起来并通过有UE-type能力的RSU发送。

    但是，***共享预处理的数据，例如通过自动对象检测提取对象是不够的，因为驾驶员的驾驶决定取决于他们的驾驶能力和安全偏好\***（汽车之间的距离，相向而行车辆的速度）[ 2 ]。

    共享高分辨率视频数据更好地帮助驾驶员根据自己的安全偏好做出驾驶决策。然而，共享低分辨率视频数据是不够的，因为障碍是不可见的，可能会被忽略。此外，需要避免进行视频数据压缩，会导致更高的延迟[ 2 ]。

17. **Changing driving-mode：改变驾驶模式**

    根据车辆合作水平，驾驶模式大致可分为三类[2]。自主驾驶、车队（convoy）、车列（platooning），其中最大队列大小可达20 [ 29 ]。然而每个驾驶模式有各自的优势，但存在特殊的交通场景下，在当前采用的驾驶模式没有切换到其他驱动方式导致交通事故的情况。

    ***这个场景在我们支持车列的时候是有可能发生的\***

![C-V2X_车列改变.png](http://iov.sicrc.cn/usr/uploads/2020/02/3431883647.png)

1. **Tethering via Vehicle：**车辆网关

   这种场景下，使车辆为住户、行人等提供网络接入能力。车辆有几个参数是手持设备所没有的，如天线物理分布、有效功率、散热、设备尺寸的约束，多天线，利用一些或所有这些可能的设施，车辆可被视为一个高级别的网络设备。这种高级别的设备可用于为连接到车辆的使用者或车辆周围的行人提供代理网络。

   一个好处是以MNO通过关联活跃用户增加网络致密化，捆绑个人用户并降低网络开销。***其对车路协同的需求不大\***

2. **Use case out of 5G coverage：**移动切换

   移动到5G网络之外

3. **Emergency trajectory alignment：应急轨迹校准**

   应急轨迹校准(EtrA)信息用于补充自动驾驶[31]。

   - 车辆从车载传感器获得道路上障碍物信息(例如路上的行人、遗失物品、鹿过马路等)，计算行车路线，以避免意外。
   - 通知其他车辆这一安全紧急情况。
   - 接近的车辆开始调整轨迹，协同反应。

4. **Teleoperated support (TeSo)：遥控驾驶**

   遥控驾驶（TsSo）是支持远程控制自动驾驶车辆。***遥控驾驶的商业模式到底怎么用还不太清楚\***

   遥控驾驶需要端到端延迟小于20ms，25 Mbps上行链路用于发送视频和传感器数据，1Mbps的下行数据链路用于接收应用相关控制和命令消息，99.999%的可靠性。

5. **Intersection safety information provisioning for urban driving：城市十字路口交通安全信息服务**

   交通事故发生在车辆和行人拥挤的十字路口。为车辆提供安全信息，防止交通事故的发生，辅助车辆通过交叉口时的协同自动驾驶功能。

   ***交叉口安全信息包括精确的数字地图、交通信号信息、行人车辆移动状态信息和位置信息，一般以LDM (Local Dynamic map)表示。\***该业务由道路雷达、交通信号、LDM服务器和RSU组成的交叉口安全信息系统进行。LDM服务器通过道路雷达和交通信号监控道路情况，生成LDM信息并通过RSU(4)传递给UE。

   通过分析LDM消息大小、激活车辆数量和交叉口交通模型的自动车辆速度，可以估计3GPP系统支持交叉口安全信息供应的能力:

   - 十字路口交通模型

     十字路口有四个方向，每个方向有两条车道。通信覆盖250m，每个方向50辆车加入通信。车辆的最大数量为200辆，自动驾驶车辆的平均速度为每小时60公里

   - LDM消息大小和传输速率

     LDM消息由静态地图信息、交通信号相位信息、移动目标信息(行人或车辆)组成。LDM消息大小估计为400~500字节。

     > The static map with the size 500m x 500m may have 300bytes  approximately. The moving objects with ID and a certain speed will have  less than 100byets. The total LDM message will have 400~500 bytes*.*

     自动车辆以60km/h的速度移动，每秒移动16m。对于安全应用，LDM消息的传输速率至少为10，这意味着LDM消息将以1.6m的间隔接收。自动车辆控制应用中LDM报文的传输速率应大于50，即车辆控制步长为32 cm。

   - 分组数据速率和可靠性

     根据给定的条件，200辆车，LDM消息传递大小为450字节，消息传输速率为100，所需的数据速率将按450字节x 8位x 200辆车x 50条消息每秒计算。大概是36Mbps。需要将分组传输效率考虑到60% ~70%。因此，分组数据速率将为50Mbps。

![C-V2X_LDM.png](http://iov.sicrc.cn/usr/uploads/2020/02/3243960446.png)

1. **Cooperative lane change (CLC) of automated vehicles：协同车道变换**

   在多车道公路上，车辆可以改变车道。为了保证安全高效的换道，制定车辆之间车道变换计划是有必要的。协同车道变换V2X方案涉及交换他们预定的轨迹来协调他们的横向和纵向控制的车辆（方向）（加速/减速）以确保顺利完成换道操作。***这好像也算是安全消息类的\***

2. **Proposal for secure software update for electronic control unit：**ECU升级

   汽车电子控制单元（ECU）是一个通用的软件模块，它控制汽车系统中的电子设备；它从方向盘到刹车控制自动驾驶的任何东西，它将成为汽车的关键部分，它可能需要定期的软件更新。这些更新受到重大安全影响，是汽车工业中的一个重要议题。***这好像更多的是移动互联网服务，且更重要的是安全问题\***

3. **3D video composition for V2X scenario：3D视频**

   这些设备有一个摄像头，他们拍摄环境视频，然后把这个视频发送到服务器。服务器可以在云中或在UE的连接点附近（即移动边缘计算（MEC））。服务器/  MEC随后将处理接收到的视频，并结合这些信息创建一个环境的3D视频。然后，3D视频可以用于不同场景中的分析，例如在赛车比赛中与最终用户共享视频，评估执法可能发生的事故等。

   该位置信息允许服务器准确地表示车辆、行人和该区域内的任何物体的位置、相对速度和距离。

#### 3.2.2 5G-V2X场景分类

5G-V2X TR 22.886主要定义了与自动驾驶、高级辅助驾驶等相关的功能，包括车辆编队、高级驾驶、扩展传感器、远程驾驶等，加上基础功能，共25种应用场景。

![5G-V2X_规范.png](http://iov.sicrc.cn/usr/uploads/2020/02/3700855424.png)

- **车辆编队/车列：**实现多车自动编队行驶。编队中的所有车辆接收头车周期性发出的数据，以便进行编队操作。车列的头车可以由有经验的驾驶员驾驶，跟随车由自动驾驶控制，可以降低整个编队的油耗，提高效率。这里面需要考虑的问题包括：
  - ***车列中的后车如果是自动驾驶车，且支持解散编队，是不是需要超视距认知前车信息？这样与扩展传感器就类似了吧？边缘侧如果能提供更丰富的信息，应该就跟高级驾驶类似了。\***
  - ***如果是同一个公司的车列，当其通过红绿灯路口等时候，就需要考虑整个车列的通行，而不应该中断，否则重组车列会遇到麻烦。这就需要路口提供LDM的时候要考虑更多信息。\***
- **高级驾驶：**实现半自动或全自动驾驶。每辆车或RSU将其通过传感器获得的数据共享给周边车辆，从而允许车辆协调它们的运动轨迹或操作。此外，每辆 车都与周边车辆共享其驾驶意图。这个场景可以提高驾驶安全性，提高交通效率。高级驾驶里面最重要的几个应用：
  - Information Sharing系列，应该可以通过V2I2V来实现
  - ***Intersection Safety Information Provisioning，路侧红绿灯和雷达等传感器的整合\***
  - 3D video composition，路侧摄像头也可以提供给车辆
- **扩展传感器：**实现本地传感器采集的数据或实时视频数据在车辆、RSU、行人设备和V2X应用服务器之间的交换。这些数据的交互等效于扩展了车辆传感 器的探测范围，从而使车辆增强了对自身环境的感知能力，并使车辆对周边情况能有更全面的了解。
  - ***关键是传感器的信息以什么形式传递给车辆\***
- **远程驾驶：**实现驾驶员或驾驶程序远程驾驶车辆。该场景可用于乘客无法驾驶车辆、车辆处于危险环境等本地驾驶条件受限的情况，也可用于公共运输等行驶轨迹相对固定的场景。
  - ***这一点的商业驾驶还存疑，可能适合专用场景，不适合开放道路场景\***

### 3.2 信通院定义的C-V2X场景

来源：信通院[《C-V2X业务演进白皮书》](http://www.caict.ac.cn/kxyj/qwfb/bps/201911/P020191104336556097939.pdf)（2019.10）

#### 3.2.1 驾驶安全场景

1. **车辆汇入汇出**
   车辆汇入汇出是指主车（HV）与远车（RV）分别位于匝道入口/出口两侧，HV预备从匝道汇入主道。

   车辆汇入汇出特别适用于高速公路、快速路等路段的开放道路入口汇入汇出场景，辅助高速公路及快速路管理，在保证安全的前提下，通过选择合理的汇入时间、汇入位置和汇入速度，减少汇入车辆对主线车流的影响，提高高速公路及快速路的匝道处通行效率。

   车辆汇入汇出也包括车辆换道行驶场景。

   ***交汇区和交通路口应该是车路协同最重要的场景\***

2. **编队行驶**

   编队行驶是通过C-V2X等无线通信技术将同向行驶的车辆进行连接，尾随的车辆可接收到前面车辆加速、刹车等信息，并在最短的时间内做出反应。

   编队的通信主要包括编队内部车辆间通信和编队与外部（智能路侧设备RSU或者其他车辆）的通信。当RSU广播道路信息时,  可以根据车道方向采用定向或非定向的方式。通常车队头车是自动驾驶等级为L0-L3级别的车辆，跟随车辆是基于实时信息交互并保持稳定车距的自动驾驶L3-L4级别成员车辆。

   在编队行驶中，列队中靠后的车辆能做出和前面车辆对应的行动。无人驾驶车辆之间的刹车和加速几乎可以同步，远远超过了人类驾驶员的反应时间，从而可以获得更高的安全性和更近的车距。  

3. **协作式车队管理**
   协作式车队管理是指车队的车头从云端及周边车辆获取安全、交通环境、车载传感器等信息，形成车队行驶策略，从而完成整个车队的动态管理，确保车队安全、高效出行。

   协作式车队管理适用于在网络覆盖下的城市及郊区道路。该应用能够有效提升车队管理效率，保证车队车头信息获取的全面性，既能够从云端获取基于整体交通状况的行驶建议，又能通过车队内车辆间信息的共享交互实现近距离安全行驶，并且能够实时进行车队内及车队间灵活调控，实现安全与效率的同时提升。

   协作式车队管理的主要场景包括车队加入/离开、车队融合/拆分等 。

   ***重点考虑车队、车列行驶在路口、交汇区等地方的影响\***

#### 3.2.2 交通效率场景

1. **基于车路协同的交叉口通行**

   基于车路协同的交叉口通行是指主车（HV）驶向交叉路口：

   - HV向V2X服务器（可以位于云端或者位于边缘）发送车辆行驶信息，V2X服务器根据车辆行驶信息、目标交叉路口的交通信息、其他车辆上报的行驶信息，为HV生成通过交叉路口的通行调度信息，并发送给HV；
   - HV通过路侧RSU获取相关感知信息、其他车辆信息、V2X服务器的云端信息等，自身生成调度信息。
   - HV可按照通行调度信息，结合V2X功能感知的、以及其它车载传感器感知的周边环境信息，控制HV通过交叉路口。

   基于车路协同的交叉口通行从全局最优的角度为车辆分配入口车道、出口车道、以及引导车速等信息，能够提高通行效率，实现辅助驾驶，为智慧交通管理与控制提供助力。  

   ***交汇区与交叉路口最重要\***

2. **基于实时网联数据的交通信号配时动态优化**

   基于实时网联数据信号配时动态优化是指车辆通过C-V2X实时上报驾驶相关信息，路口交通信号控制器结合交通、车辆通行等信息进行交叉路口交通信号时长或者信号变化的调整，如果有条件可以结合交通控制中心的背景数据和方案进行优化。

   本应用适用于城市及郊区普通道路及公路的信号控制交叉路口、信号控制匝道的入口、干道多交叉路口、区域内多交叉路口等的信号协同控制优化。相对于目前的静态或半静态的交通信号调整，结合C-V2X提供的交通实时感知数据，在网联车与其他常规车辆混合的交通环境下，或者完全联网汽车环境下的实时网联数据信号配时动态优化，在保证安全性的前提下提升信号控制交叉口及匝道交通控制的效率。

   ***动态配时优化与车列等一起考虑\***

3. **交叉口动态车道管理**

   交叉口动态车道管理是针对交叉口的拥堵问题，通过动态划分交叉口处的车道功能，实现对交叉口进口道的空间资源进行实时地合理分配。

   交叉口动态车道管理应用需要的基本系统由智能车载单元（OBU/T-BOX）和智能路侧设备（RSU）实现。智能路侧设备收集车辆的状态数据包括位置、速度、转向等等，实时确定交叉口的各个流向的交通需求，计算合理的车道功能划分结果，并发送给智能车载单元，进而诱导网联车辆行驶至对应车道，该应用通过动态的车道管理提高交叉口的运行效率。

   ***这个与红绿灯优化类似，是交通管理的重要方式\***

4. **高速公路专用道柔性管理** 

   高速公路专用道柔性管理是指在高速公路上为远车（RV）设置专用车道，RV在专用道行驶时广播当前状态及出清距离或RSU广播路段占用状态；或RV通过向云平台发送行驶规划路径中专用车道出清请求，云端根据RV行驶规划路径，提前对规划路径中的RSU及其他车辆发送出清请求，主车（HV）收到RV、RSU或云平台消息后，若判断自身位于RV的出清距离内，则离开专用道。 

   专用道柔性管理适用于高速公路、快速路等路段的道路通行管理，以满足紧急车辆的快速通行需求，通过对社会车辆的避让管理产生动态的专用道，改善紧急车辆的行程时间。   

   ***专用车道管理可以考虑公交道、专用道是不是提供给物流、市政、网约大巴车等车辆\***

5. **基于车路协同的主被动电子收费**
   基于车路协同的电子收费是指以车载单元（OBU）作为支付终端，对车辆在道路行驶所产生的费用，以及车主所消费的商品或者服务进行账务支付的一种服务方式。主要包括：

   - 主动式：HV通过V2I 的方式将支付请求发送给接收路侧单元（RSU），随后与路侧单元（RSU）建立专用通信链路的P2P 单播会话，完成相应电子支付流程。
   - 被动式：路侧单元（RSU）通过I2V 的方式将支付场景（如ETC、交通罚款）的支付服务和活动状态进行广播，随后接入服务的HV 与路侧单元（RSU）建立专用通信链路的P2P 单播会话，完成相应电子支付流程。  

   基于车路协同，汽车通过车载终端与路侧单元的数据交互，使其成为金融支付终端，具备移动支付和主动支付的能力，在保证支付安全的条件下减少付费时间，有效地提高了付费和车辆通行效率。  

   ***这一场景和ETC存在重合，特别是车辆已经推广ETC的前提下，有抢ETC饭碗的嫌疑。\***

#### 3.2.3 信息服务场景

1. **车辆路径引导**
   车辆路径引导是指基于云端/服务端、路侧端或MEC平台端，根据出行车辆的需求，基于地图信息、历史信息、车辆实时状态、驾驶人行为信息以及交通基础设施信息、路网交通状态信息、综合感知信息等，预测交通状况，计算出行车辆行驶策略，通过C-V2X网络为出行车辆提供准确、实时、高效的出行路径规划和行驶引导。

   车辆路径引导场景可分为全局路径引导和局部路段引导。

   - 全局路径引导是指对车辆出行线路的路径规划；随着C-V2X和5G通信基础设施的部署和应用，地图服务商、出行服务商可以获得更加精准、广泛的细粒度数据，例如复杂立交桥的垂直位置和行驶信息，因而可以提供更加精准的全局路径引导。
   - **局部路段引导**是指在某一路段或某一特定场景为车辆提供精细化的速度和行驶车道引导。随着5G - MEC - LTE-V2X设施的部署和应用，路侧RSU - MEC可以获得更细粒度、更实时的交通流数据，基于路侧RSU -  MEC的局部路段引导服务可以做的更精准，使得车道级引导、基于红绿灯信息的车速引导等也能获得广泛应用。  

   ***局部引导可以和自动驾驶的运动规划结合\***

   1. **电动汽车动态路径规划** 

   电动汽车路径规划是指电动汽车（EV）出行时，考虑到电池电量、出发点和目的地位置、充电站（CS）信息、交通路况信息，为电动汽车出行路线、充电行驶路线做出规划以及动态调整。

   电动汽车动态路径规划综合考虑充电站信息和交通路况感知信息进行路径规划，能够减少电动汽车行程时间、充电等待时间，提高道路通行效率、充电站服务能力，缓解电动汽车用户的里程焦虑问题，进一步促进电动汽车在我国的普及。  

   - 在有智能路侧单元（RSU）的情况下：RSU广播充电站信息，交通路况感知信息，电动汽车通过接收此类信息，更新本地动态地图，由车载单元计算行驶路线；或者电动汽车将本地信息(电池电量、出发点和目的地位置)上传RSU，由RSU为电动汽车计算行驶路线。
   - 在没有RSU的情况下：电动汽车通过车车通信互相传递充电站信息和交通路况感知信息，由车载单元计算行驶路线。
   - 在有蜂窝网覆盖的情况下：电动汽车也可以通过蜂窝网络向远程服务器获取充电站信息和交通路况感知信息来进行行车路线规划。  

   ***这个与路线规划类似，可能更适合移动互联网服务\***

   1. **基于车路协同的远程软件升级**
      基于车路协同的远程软件（OTA）升级是基于V2X OTA平台，在无线网络信号良好时，智能车载设备通过无线网络获取升级包；无线网络信号不良时，智能车载设备通过智能路侧设备（RSU）获取升级包。

   其中V2X OTA平台，既可以在已有的V2X公有平台基础上扩展，也可以独立部署。智能路侧设备本身可以利用V2N升级，但只能从单一的数据来源获取升级包 。

   ***这一场景实际可以扩展到地图更新等场景，但不认为其应该支持车载其他固件的升级，关键软件的OTA应该使用基站网络的长连接，不应该使用RSU的短连接。\***

   1. **智能停车引导**
      智能停车引导是指针对停车场的停车管理系统中存在的车位查找困难、车位状态管理不方便和成本高、停车定位导航不方便、车辆自主代客泊车难度大等问题，结合V2X智能路侧设备、V2X云平台、V2X智能车载终端，实现室外停车库车位状态管理、车位申请与授权、停车导航入库、车位查找、动静态障碍物躲避、泊车路径规划、自主泊车入位等功能 。

   ***这个跟远程驾驶结合可能有用，单纯的车位引导是纯移动互联网服务\***

#### 3.2.4 IMT2020定义的场景

IMT2020场景与信通院场景大部分是一致的。

| 序号 | 场景                                                         |
| ---- | ------------------------------------------------------------ |
| 1    | 车辆汇入汇出控制 Vehicle  merging control                    |
| 2    | 慢行交通轨迹识别及行为分析 VRU                               |
| 3    | 基于车辆控制的交叉口通行控制 Intersection traffic control    |
| 4    | 车辆路径引导 Eco-driving  navigation                         |
| 5    | 动态车道管理 Dynamic  lane management                        |
| 6    | 基于实时网联数据信号配时动态优化 Traffic Signal Dynamic Optimization |
| 7    | 智能停车引导 Intelligent  parking                            |
| 8    | 车辆编队行驶 Platooning                                      |
| 9    | 协作式车队管理 Cooperative  platooning management            |
| 10   | 专用道柔性管理 Dynamic  dedicated lane                       |
| 11   | 拥堵收费/电子收费 Electronic  Payment system                 |
| 12   | 电动汽车动态路径规划和充电路径规划 Navigation for electronic vehicle |
| 13   | 协作式远程升级 Cooperative  OTA                              |
| 14   | 基于V2X的自动驾驶整车在环仿真 V2X based online vehicle simulation |
| 15   | 远程遥控驾驶  Remote driving with condition                  |
| 16   | 面向自动驾驶车辆的协同式感知  Cooperative  perception for L4 vehicle |
| 17   | 基于路侧控制的自动驾驶车辆无信号交叉路口通行 intersection traffic control for  L4 vehicle |
| 18   | 自动驾驶车辆“脱困” Abnormal L4 Vehicle assistance            |
| 19   | 面向自动驾驶车辆的高精地图动态更新 HD map update for L4 vehicle |

### 3.3 智能网联汽车定义的C-V2X场景

智能网联汽车联盟与信通院联合制定的《[C-V2X 产业化路径和时间表研究白皮书](http://www.caicv.org.cn/index.php/newsInfo/downLoad?id=2301)》中，总结了一些应用场景。

#### 3.3.1 场景分类与实现方式

![C-V2X_智能网联车场景1.png](http://iov.sicrc.cn/usr/uploads/2020/02/2640306766.png)
![C-V2X_智能网联车场景2.png](http://iov.sicrc.cn/usr/uploads/2020/02/2689828504.png)
![C-V2X_智能网联车场景3.png](http://iov.sicrc.cn/usr/uploads/2020/02/1421997675.png)
![C-V2X_智能网联车场景4.png](http://iov.sicrc.cn/usr/uploads/2020/02/3372746237.png)
![C-V2X_智能网联车场景5.png](http://iov.sicrc.cn/usr/uploads/2020/02/428784475.png)

#### 3.3.2 基础服务场景

在基础业务场景阶段， 大部分应用的实现都基于车辆、 道路设施等参与者之间的实时状态共享。 在利用 C-V2X 信息交互实现状态共享的基础上， 再自主进行决策或辅助。  

![C-V2X_智能网联车场景6.png](http://iov.sicrc.cn/usr/uploads/2020/02/994973988.png)
![C-V2X_智能网联车场景7.png](http://iov.sicrc.cn/usr/uploads/2020/02/4266373477.png)

#### 3.3.3 增强服务场景

C-V2X的引入能够为智能网联汽车带来两方面好处：

- C-V2X 与智能网联汽车相结合，能有效地提高交通系统，例如道路、交通控制系统等的感知粒度、信息实时双向交互的能力；
- C-V2X 能提升智能网联车辆本身的感知、协同控制能力，对驾驶环境的感知范围在时间和空间方面都有长足的拓展。

车-路-云协同促使未来车联网业务演进将从四个方面持续推进：出行发生端的共享出行业务， 出行阶段的安全出行和交通效率两类业务， 以及贯穿整个出行过程的信息服务类业务。

从个性上看， 安全出行和效率出行会向精细化方向发展，信息服务业务则继续作为其他业务的载体与其他业务互相融合， 协同支持各种增强的车联网业务。  

![C-V2X_智能网联车场景8.png](http://iov.sicrc.cn/usr/uploads/2020/02/1033061385.png)

### 3.4 中国汽车工程学会定义的场景

参考《合作式智能运输系统车用通信系统应用层及应用数据交互标准》（T/CSAE 53-2017），其定义了17种场景，这些场景与LTE-V2X定义的第一阶段场景非常类似，绝大部分是通过V2V来实现的。

| 序号 | 类别     | 通信方式  | 应用名称               |
| ---- | -------- | --------- | ---------------------- |
| 1    | 安全     | V2V       | 前向碰撞预警           |
| 2    | 安全     | V2V/V2I   | 交叉路口碰撞预警       |
| 3    | 安全     | V2V/V2I   | 左转辅助               |
| 4    | 安全     | V2V       | 盲区预警／变道辅助     |
| 5    | 安全     | V2V       | 逆向超车预警           |
| 6    | 安全     | V2V-Event | 紧急制动预警           |
| 7    | 安全     | V2V-Event | 异常车辆提醒           |
| 8    | 安全     | V2V-Event | 车辆失控预警           |
| 9    | 安全     | V2I       | 道路危险状况提示       |
| 10   | 安全     | V2I       | 限速预警               |
| 11   | 安全     | V2I       | 闯红灯预警             |
| 12   | 安全     | V2P/V2I   | 弱势交通参与者碰撞预警 |
| 13   | 效率     | V2I       | 绿波车速引导           |
| 14   | 效率     | V2I       | 车内标牌               |
| 15   | 效率     | V2I       | 前方拥堵提醒           |
| 16   | 效率     | V2V       | 紧急车辆提醒           |
| 17   | 信息服务 | V2I       | 汽车近场支付           |

这一规范的优点是定义了详细的消息结构，可操作性比较强。

### 3.5 中国电信提出的C-V2X场景

中国电信认为的C-V2X业务与形态如下：

![C-V2X能力需求.png](http://iov.sicrc.cn/usr/uploads/2020/02/379432304.png)

信通院、中国电信、大唐等都提出基于边缘计算来支持C-V2X业务，电信运营商的边缘计算部署方式及性能如下：

![C-V2X-MEC需求.png](http://iov.sicrc.cn/usr/uploads/2020/02/889686756.png)

## 4. 技术需求

### 4.1 LTE-V2X技术需求

TR 22.885定义的27种应用场景主要实现辅助驾驶功能，包括主动安全（例如碰撞预警、紧急刹车等）、交通效率（例如车速引导）、信息服务等方面。整合各种典型用例，对LTE-V2X有如下技术需求：

![LTE-V2X技术需求.png](http://iov.sicrc.cn/usr/uploads/2020/02/3157202523.png)

参考文献：

1. 李凤,房家奕,赵丽.3GPP LTE-V2X标准进展及技术介绍[J].电信网技术,2016(06):40-45.
2. TR 22.885

### 4.2 5G V2X技术需求

TR 22.886主要实现自动驾驶功能，包括车辆编队、高级驾驶、扩展传感器、远程驾驶四大类功能。加上基础功能，共25种应用场景，对5G V2X有如下需求：

| 用例          | 时延(ms) | 可靠性（%） | 数据速率(Mbps) |
| ------------- | -------- | ----------- | -------------- |
| 车辆编队/车列 | 10       | 99.99       | 65             |
| 高级驾驶      | 3        | 99.999      | 53             |
| 扩展传感器    | 3        | 99.999      | 1000           |
| 远程驾驶      | 5        | 99.999      | UL 25  DL 1    |

参考文献：

1. TR 22.886

### 4.3 中国汽车工程学会标准的技术需求

汽车工程学会在T/CSAE 53-2017中定义了17个场景，这几个场景的技术需求包括：

| 应用                                   | 频率( Hz ) | 最大时延( ms ) | 定位精度( m ) | 通信范围( m ) | 分类           | 适用技术         |
| -------------------------------------- | ---------- | -------------- | ------------- | ------------- | -------------- | ---------------- |
| 前向碰撞预警                           | 10         | 100            | 1.5           | 300           | 低时延、高频率 | LTE-V/DSRC/5G    |
| 盲区预警／变道辅助                     | 10         | 100            | 1.5           | 150           | 低时延、高频率 | LTE-V/DSRC/5G    |
| 紧急制动预警                           | 10         | 100            | 1.5           | 150           | 低时延、高频率 | LTE-V/DSRC/5G    |
| 逆向超车碰撞预警                       | 10         | 100            | 1.5           | 300           | 低时延、高频率 | LTE-V/DSRC/5G    |
| 同红灯预警                             | 10         | 100            | 1.5           | 150           | 低时延、高频率 | LTE-V/DSRC/5G    |
| 交叉路口碰撞预警                       | 10         | 100            | 5             | 150           | 低时延、高频率 | LTE-V/DSRC/5G    |
| 左转辅助                               | 10         | 100            | 5             | 150           | 低时延、高频率 | LTE-V/DSRC/5G    |
| 高优先级车辆让行 ／紧急 车辆信号优先权 | 10         | 100            | 5             | 300           | 低时延、高频率 | LTE-V/DSRC/5G    |
| 弱势交通参与者预警                     | 10         | 100            | 5             | 150           | 低时延、高频率 | LTE-V/DSRC/5G    |
| 车辆失控预警                           | 10         | 100            | 5             | 300           | 低时延、高频率 | LTE-V/DSRC/5G    |
| 异常车辆提醒                           | 10         | 100            | 5             | 150           | 低时延、高频率 | LTE-V/DSRC/5G    |
| 道路危险状况提示                       | 10         | 100            | 5             | 300           | 低时延、高频率 | LTE-V/DSRC/5G    |
| 基于信号灯的车速引导                   | 2          | 200            | 1.5           | 150           | 高时延、低频率 | 4G/LTE-V/DSRC/5G |
| 限速预警                               | 1          | 500            | 5             | 300           | 高时延、低频率 | 4G/LTE-V/DSRC/5G |
| 车内标牌                               | 1          | 500            | 5             | 150           | 高时延、低频率 | 4G/LTE-V/DSRC/5G |
| 前方拥堵提醒                           | 1          | 500            | 5             | 150           | 高时延、低频率 | 4G/LTE-V/DSRC/5G |
| 汽车近场支付                           | 1          | 500            | 5             | 150           | 高时延、低频率 | 4G/LTE-V/DSRC/5G |

该需求依据的数据更新频率、系统延迟参照 SAE J2735、J2945/l 及 NHTSA VSC-A 性能指标说明。

其中，车辆制动过程：

![TCSAE-53-2017-汽车制动过程.png](http://iov.sicrc.cn/usr/uploads/2020/02/2754096219.png)

基于汽车制动动力学的最小安全距离模型：

![image-20210527084742633](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527084742633.png)

据此，要求通信距离 >= 300m，定位精度 <=1.5m。

参考文献：

1. 《合作式智能运输系统车用通信系统应用层及应用数据交互标准》（T/CSAE 53-2017）