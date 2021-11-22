团体标准    				合作式智能运输系统	车用通信系统	应用层及应用数据交互标准（第一阶段）

## 一、术语和定义

### 术语

#### 合作式智能运输系统 cooperative intel l i gent transportat ion systems,C-|TS

合作式智能运输系统是通过人、车、路信息交互,实现车辆和基础设施之间、车辆与车辆之间、车辆与人之间的智能协同与配合的一种智能运输系统。

#### 系统延迟 system delay

从远车或路侧单元等设备发送通信数据后,到主车接收该数据并通过网络层进行信息处理后传递给应用层的时间。本文件中特指应用层端到端的延迟时间。

#### 主车 host vehicle,HV

装有车载单元且运行应用程序的目标车辆。

#### 远车 remote vehicle,R

与主车配合能定时广播V2X消息的背景车辆。

#### 车载单元 on- board unit,OBU

安装在车辆上的可实现V2X通信，支持V2X应用的硬件单元。

#### 路侧单元 road side unit,RSU

安装在路边的可实现V2X通信，支持V2X应用的硬件单元。

### V2X

车载单元与其他设备通信,包括但不限于车载单元之间通信(V2V),车载单元与路侧单元通信(V2I)车载单元与行人设备通信(V2P),车载单元与网络之间通信(V2N)。

### 缩略语

下列缩略语适用于本文件

4G:第四代移动通信技术(the4 th Generation mobile communication technology)

5G:第五代移动通信技术(the5 th Generation mobile communication technology)

ABS:制动防抱死系统(Anti-1 ock Braking System)

ADS:应用数据交换服务( Application Data- Exchange Service)

API:应用程序编程接口( Application Programming Interface

ASN.1:抽象语法记法( Abstract Syntax Notation One)

AwW:异常车辆提醒( Abnormal vehicle Warning)

BSM:基本安全消息( Basic safety Message

BSW:盲区预警( Blind Spot Warning)

CAV:防撞距离( Collision Avoidance Range)

CLW:车辆失控预警( Control lost Warning

CSAE:中国汽车工程学会( Society of Automotive Engineers of China)

C-ITS:中国智能交通产业联盟( China Its Industry Alliance)

DE:数据元素( Data element)

F:数据帧( Data frame

DAE:专用短程通信管理实体( DSRC Management Entity

DNPW:逆向超车预警( Do Not Pass Warning)

DSM:专用短程通信短消息( DSRC Short Message)

DSRC:专用短程通信( Dedicated Short Range Communications)

DTI:到交叉口的距离( Distance-to- Intersection)

EBW:紧急制动预警( Emergency Brake Warning)

ESP:车身电子稳定系统( Electronic Stability Program)

ETC:电子不停车收费系统( Electronic Toll collection)

ETSI:欧洲电信标准化协会( European Telecommunications Standardtitute)

EwW:紧急车辆提醒( Emergency Vehicle Warning)

FCW:前向碰撞预警( Forward Collision Warning)

GB:中国国家标准( Guo biao( Nation standard))

GLOSA:绿波车速引导( Green Light0 ptimal speed advisory)

GNSS:全球导航卫星系统( Global Navigation Satellite System)

GPS:全球定位系统( Global Positioning System)

HLN:道路危险状况预警( Hazardous location Warning)

HMI:人机交互界面( Human Machine Interface)

主车( Host vehi）

ICw:交叉路口碰撞预警( Intersection Collision Warning)

ID:标识( Identification)

ISO:国际标准化组织( International Standards Organization)

TS:智能交通系统( Intelligent Transportation Systems)

IVS:车内标牌(In- Vehicle signage)

LCW:变道预警( Lane Change Warning

LDW:车道偏离预警( Lane departure Warning)

LTA:左转辅助( Left Turn assistant)

TE-V2X:基于LTE的车联网无线通信技术( LtE Vehicle to Everything)

NHTSA:美国高速公路安全管理局( National Highway Traffic Safety Administration)

OBU:车载单元(On- Board unit)

P2P:点对点( Point to point)

RSA:路侧单元发布的交通事件消息( Road side alert

RSM:路侧单元消息( Road Side message)

RSU:路侧单元( Road side unit)

RV:远车( Remote vehicle)

SAE:美国汽车工程师学会( Society of Automotive Engineers)

SLW:限速预警( Speed Limit Warning)

SPAT:信号灯消息( Signal phase and Timing Message)

SPI:服务提供者接口( Service provider interface)

SW:闯红灯预警( Signal Violation Warning)

TC:目标分类( Target Classification)

TCS:牵引力控制系统( Traction Control System)

TJW:前方拥堵提醒( Traffic Jam Warning

TTC:碰撞预计时间(Time-to- Collision)

TTI:到达交叉口预计时间(Time-to- Intersection)

UPER:非对齐压缩编码规则( Unaligned Packet Encoding Rules)

V2I:车载单元与路侧单元通信( Vehicle to infrastructure)

V2P:车载单元与行人设备通信( Vehicle to pedestrians

V2V:车载单元之间通信( Vehicle to vehicle)

V2X:车载单元与其他设备通信( Vehicle to Everything)

VIN:车辆识别码( Vehicle id number)

VNFP:汽车近场支付( Vehicle near- Field payment)

VRUCW:弱势交通参与者碰撞预警( Vulnerable road User Collision Warning)

## 二、合作式智能运输系统车用通信系统

### 1. 系统介绍

合作式智能运输系统车用通信系统，旨在通过智能运输系统各子系统之间的信息交互，实现道路安全、通行效率、信息服务等各类应用。为此，不同厂商车辆之间，以及这些车辆与其所能到达的区域范围内的道路基础设施之间，必须实现互联互通。本文件的目的，是通过定义信息交互的消息集、数据帧与数据元素，来实现车用通信系统在应用层的互联互通。

![image-20210527090141913](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090141913.png)

——定位系统:该子系统通常包含全球导航卫星系统(GNSS, Global Navigation Satellite System接收器,用以提供车辆的位置、方向、速度和时间等信息。该子系统可以通过车速信号、惯性测量单元、差分定位系统等技术来实现增强定位；

——车载设备处理单元:运行程序以生成需要发送的空中信号,以及处理接收的空中信号；

——天线:实现射频信号的接收和发送。

车载设备通过接口与应用电子控制单元相连,应用电子控制单元中运行程序实现车用通信系统的应用,并通过人机交互界面(HMI, Human machine interface)来实现对驾驶员的提醒,包括图像、声音、振动等方式。在某些场合,应用电子控制单元和车载设备处理单元在一个物理设备中实现。

## 三、车用通信系统基础应用

### 1. 需求分析

本文件选择涵盖安全、效率、信息服务三大类的17个典型应用作为一期应用。选择过程详见附录A。表1为本文将选择的17个一期应用列表。

![image-20210527090325824](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090325824.png)

### 2. 应用定义及基本要求

#### 2.1 前向碰撞预警

##### 2.1.1 应用定义和预期效果

**前向碰撞预警**(FCW: Forward Collision Warning)是指,主车(Ⅳ)在车道上行驶,与在正前方同一车道的远车(RV)存在追尾碰撞危险时,FCw应用将对ⅣV驾驶员进行预警。本应用适用于普通道路或高速公路等车辆追尾碰撞危险的预警。

FCW应用辅助驾驶员避免或减轻前向碰撞,提高道路行驶安全。



##### 2.1.2 主要场景



##### 2.1.3 系统基本原理



##### 2.1.4 通信方式



##### 2.1.5 基本性能要求



##### 2.1.6 数据交互需求







![image-20210527090426195](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090426195.png)

![image-20210527090459728](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090459728.png)

![image-20210527090509438](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090509438.png)

![image-20210527090524523](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090524523.png)

![image-20210527090556928](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090556928.png)

![image-20210527090609728](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090609728.png)

![image-20210527090634047](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090634047.png)

#### 2.2 交叉路口碰撞预警

应用定义和预期效果

![image-20210527090710144](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090710144.png)

![image-20210527090719328](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090719328.png)

![image-20210527090735840](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090735840.png)

![image-20210527090747447](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090747447.png)

![image-20210527090800599](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090800599.png)

#### 2.3 左转辅助

![image-20210527090829832](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090829832.png)

![image-20210527090909679](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090909679.png)

![image-20210527090920767](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090920767.png)

![image-20210527090929683](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527090929683.png)

#### 2.4 盲区预警/变道预警

![image-20210527091000792](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091000792.png)

![image-20210527091014656](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091014656.png)

![image-20210527091022849](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091022849.png)

![image-20210527091041409](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091041409.png)

#### 2.5 逆向超车预警

![image-20210527091101303](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091101303.png)

![image-20210527091113487](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091113487.png)

![image-20210527091125887](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091125887.png)

![image-20210527091137569](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091137569.png)

#### 2.6 紧急制动预警

![image-20210527091156748](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091156748.png)

![image-20210527091207103](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091207103.png)

![image-20210527091217592](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091217592.png)

![image-20210527091231072](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091231072.png)

![image-20210527091242560](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091242560.png)

![image-20210527091251551](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091251551.png)

#### 2.7 异常车辆提醒

![image-20210527091325851](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091325851.png)

![image-20210527091344641](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091344641.png)

![image-20210527091354800](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091354800.png)

![image-20210527091404599](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091404599.png)

#### 2.8 车辆失控预警

![image-20210527091422713](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091422713.png)

![image-20210527091435975](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091435975.png)

![image-20210527091444512](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091444512.png)

![image-20210527091455032](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091455032.png)

#### 2.9 道路危险状况提示

![image-20210527091522376](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091522376.png)

![image-20210527091531104](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091531104.png)

![image-20210527091542616](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091542616.png)

#### 2.10 限速预警

![image-20210527091559608](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091559608.png)

![image-20210527091607771](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091607771.png)

#### 2.11 闯红灯预警

![image-20210527091639103](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091639103.png)

![image-20210527091646640](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091646640.png)

![image-20210527091658268](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091658268.png)

![image-20210527091709177](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091709177.png)

![image-20210527091716945](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091716945.png)

#### 2.12 弱势交通参与者碰撞预警

![image-20210527091822801](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091822801.png)

![image-20210527091849817](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091849817.png)

![image-20210527091858952](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091858952.png)

![image-20210527091907801](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091907801.png)

![image-20210527091917420](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091917420.png)

![image-20210527091932571](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091932571.png)

![image-20210527091938551](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091938551.png)

#### 2.13 绿波车速引导

![image-20210527091957290](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527091957290.png)

![image-20210527092005824](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092005824.png)

![image-20210527092015000](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092015000.png)

![image-20210527092027400](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092027400.png)

#### 2.14 车内标牌

![image-20210527092106400](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092106400.png)

![image-20210527092116265](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092116265.png)

![image-20210527092125514](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092125514.png)

#### 2.15 前方拥堵提醒

![image-20210527092145601](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092145601.png)

![image-20210527092154487](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092154487.png)

![image-20210527092203057](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092203057.png)

#### 2.16 紧急车辆提醒

![image-20210527092222776](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092222776.png)

![image-20210527092234674](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092234674.png)

![image-20210527092241559](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092241559.png)

![image-20210527092248623](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092248623.png)

#### 2.17 汽车近场支付

![image-20210527092334088](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092334088.png)

![image-20210527092410360](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092410360.png)

![image-20210527092419985](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092419985.png)

![image-20210527092434644](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092434644.png)

![image-20210527092443577](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092443577.png)



## 应用层交互数据集



![image-20210527092646028](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092646028.png)

![image-20210527092702055](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092702055.png)

### 1. 消息体

### 1.1 Msg_BSM

定义
车辆基本安全消息。是使用最广泛的一个应用层消息,用来在车辆之间交换安全状态数据。车辆通过该消息的广播,将自身的实时状态告知周围车辆,以此支持一系列协同安全等应用。

![image-20210527092748496](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092748496.png)

### 1.2 Msg_MAP

![image-20210527092809128](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092809128.png)

![image-20210527092837298](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092837298.png)

### 1.3 Msg_RSI

![image-20210527092854241](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092854241.png)

![image-20210527092904976](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092904976.png)

### 1.4 Msg_RSM

![image-20210527092926595](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092926595.png)

### 1.5 Msg_SPAT

![image-20210527092953547](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527092953547.png)

![image-20210527093002808](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093002808.png)

### 2. 数据帧

数据帧由其他数据单元或数据类型组合而成，具有特定的实际意义。是消息体的组成部分。

### 2.1 DF_AccelerationSet4Way

![image-20210527093052362](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093052362.png)

### 2.2 DF_BrakeSystemStatus

![image-20210527093115753](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093115753.png)

![image-20210527093132817](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093132817.png)

### 2.3 DF_ConnectingLane

![image-20210527093155364](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093155364.png)

### 2.4 DF_Connection

![image-20210527093220939](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093220939.png)

![image-20210527093228744](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093228744.png)

### 2.5 DF_ConnectsToList

![image-20210527093245992](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093245992.png)

### 2.6 DF_Description

![image-20210527093307257](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093307257.png)

### 2.7 DF_FullPositionVector

![image-20210527093324939](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093324939.png)

### 2.8 DF_IntersectionState

![image-20210527093349256](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093349256.png)

![image-20210527093400736](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093400736.png)



### 2.9 DF_IntersectionStateList

![image-20210527093423302](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093423302.png)

### 2.10 DF_Lane

![image-20210527093439225](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093439225.png)

### 2.11 DF_LaneAttributes

![image-20210527093504834](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093504834.png)

### 2.12 DF_LaneList

![image-20210527093520416](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093520416.png)

### 2.13 DF_LaneTypeAttributes

![image-20210527093542161](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093542161.png)

### 2.14 DF_Link

![image-20210527093554928](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093554928.png)

![image-20210527093601665](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093601665.png)

### 2.15 DF_LinkList

![image-20210527093620448](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093620448.png)

### 2.16 DF_MotionConfidenceSet

![image-20210527093642530](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093642530.png)

![image-20210527093648963](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093648963.png)

### 2.17 DF_Movement

![image-20210527093704617](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093704617.png)

### 2.18 DF_MovementList

![image-20210527093720290](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093720290.png)

### 2.19 DF_Node

![image-20210527093734705](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093734705.png)

![image-20210527093743320](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093743320.png)

### 2.20 DF_NodeList

![image-20210527093800266](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093800266.png)

### 2.21 DF_NodeReferenceID

![image-20210527093815975](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093815975.png)

![image-20210527093822642](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093822642.png)

### 2.22 DF_ParticipantData

![image-20210527093846546](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093846546.png)

### 2.23 DF_ParticipantList

![image-20210527093915201](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093915201.png)

![image-20210527093921545](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093921545.png)

### 2.24 DF_PathHistory

![image-20210527093937359](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093937359.png)

### 2.25 DF_PathHistoryPoint

![image-20210527093958776](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527093958776.png)

### 2.26 DF_PathHistoryPointList

![image-20210527094021756](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094021756.png)

### 2.27 DF_PathPointList

![image-20210527094048438](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094048438.png)

### 2.28 DF_PathPrediction

![image-20210527094107713](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094107713.png)

### 2.29 DF_Phase

![image-20210527094121601](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094121601.png)

![image-20210527094128035](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094128035.png)

### 2.30 DF_PhaseList

![image-20210527094143656](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094143656.png)

### 2.31 DF_PhaseState

![image-20210527094158939](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094158939.png)

### 2.32 DF_PhaseStateList

![image-20210527094218496](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094218496.png)

### 2.33 DF_PointList

![image-20210527094231911](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094231911.png)

### 2.34 DF_Position-LL-24B

![image-20210527094251135](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094251135.png)

### 2.35 DF_Position-LL-28B

![image-20210527094313077](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094313077.png)

![image-20210527094319215](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094319215.png)

### 2.36 DF_Position-LL-32B

![image-20210527094336695](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094336695.png)

### 2.37 DF_Position-LL-36B

![image-20210527094356479](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094356479.png)

### 2.38 DF_Position-LL-44B

![image-20210527094416359](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094416359.png)

![image-20210527094425287](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094425287.png)

### 2.39 DF_Position_LL-48B

![image-20210527094442104](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094442104.png)

### 2.40 DF_Position-LLmD-64b

![image-20210527094500496](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094500496.png)

### 2.41 DF_Position3D

![image-20210527094515487](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094515487.png)

![image-20210527094521713](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094521713.png)

### 2.42 DF_PositionalAccuracy

![image-20210527094539195](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094539195.png)

### 2.43 DF_PositionConfidenceSet

![image-20210527094559764](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094559764.png)

### 2.44 DF_PositionOffsetLL

![image-20210527094646691](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094646691.png)

![image-20210527094658951](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094658951.png)

### 2.45 DF_PositionOffsetLLV

![image-20210527094718792](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094718792.png)

### 2.46 DF_ReferenceLink

![image-20210527094733175](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094733175.png)

![image-20210527094738955](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094738955.png)

### 2.47 DF_ReferenceLinkList

![image-20210527094753856](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094753856.png)

### 2.48 DF_ReferencePath

![image-20210527094810569](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094810569.png)

### 2.49 DF_ReferencePathList

![image-20210527094826695](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094826695.png)

![image-20210527094831855](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094831855.png)

### 2.50 DF_RegulatorySpeedLimit

![image-20210527094851441](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094851441.png)

### 2.51 DF_RSITimeDetails

![image-20210527094912600](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094912600.png)

### 2.52 DF_RTEData

![image-20210527094932515](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094932515.png)

![image-20210527094940289](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094940289.png)

![image-20210527094948250](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527094948250.png)

### 2.53 DF_RTEList

![image-20210527095004017](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095004017.png)

### 2.54 DF_RTSData

![image-20210527095026071](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095026071.png)

![image-20210527095032602](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095032602.png)

### 2.55 DF_RTSList

![image-20210527095048781](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095048781.png)

### 2.56 DF_RoadPoint

![image-20210527095103266](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095103266.png)

### 2.57 DF_SignalState

![image-20210527095120499](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095120499.png)

### 2.58 DF_SpeedLimitList

![image-20210527095137992](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095137992.png)

![image-20210527095144569](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095144569.png)

### 2.59 DF_TimeChangeDetails

![image-20210527095202051](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095202051.png)

### 2.60 DF_TimeCountingDown

![image-20210527095253242](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095253242.png)

![](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095229191.png)

![image-20210527095304123](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095304123.png)

### 2.61 DF_UTCTiming

![image-20210527095323908](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095323908.png)

![image-20210527095329657](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095329657.png)

![image-20210527095337473](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095337473.png)

### 2.62 DF_VehicleClassification

![image-20210527095355457](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095355457.png)

### 2.63 DF_VehicleEmergencyExtensions

![image-20210527095418781](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095418781.png)

### 2.64 DF_VehicleSafetyExtensions

![image-20210527095442016](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095442016.png)

### 2.65 DF_VehicleSize

![image-20210527095456329](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095456329.png)

### 2.66 DF_VerticalOffset

![image-20210527095514213](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095514213.png)

### 3. 数据元素

![image-20210527095605370](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095605370.png)

## 应用层数据交互标准及接口规范

![image-20210527095801459](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095801459.png)

### 1. API接口

![image-20210527095821789](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095821789.png)

![image-20210527095831221](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095831221.png)

![image-20210527095840299](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095840299.png)

#### API接口功能描述

![image-20210527095903649](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095903649.png)

![image-20210527095914147](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095914147.png)

![image-20210527095924786](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095924786.png)

![image-20210527095932876](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095932876.png)

![image-20210527095943075](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095943075.png)

![image-20210527095952227](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527095952227.png)

![image-20210527100000827](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527100000827.png)

![image-20210527100010266](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527100010266.png)

![image-20210527100018562](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527100018562.png)

![image-20210527100025881](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527100025881.png)

### 2. SPI接口

![image-20210527100043321](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527100043321.png)

## 附录B 一期应用按通信需求分类表

![image-20210527100213826](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527100213826.png)

## 附录C 前向碰撞预警（FCW）基本性能指标依据

![image-20210527100305761](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527100305761.png)

![image-20210527100314209](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527100314209.png)

![image-20210527100324129](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210527100324129.png)