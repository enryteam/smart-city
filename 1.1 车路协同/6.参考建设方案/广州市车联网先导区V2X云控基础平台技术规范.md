# 广州市车联网先导区V2X云控基础平台技术规范

# 缩略语

下列缩略语适用于本文件。

ABS：制动防抱死系统（Anti-Lock Braking System）

BSM：基本安全消息（Basic Safety Message）

EBW：紧急制动预警（Emergency Brake Warning）

ESP：车身电子稳定系统（Electronic Stability Program）

LDW：车道偏离预警系统（Lane Departure Warning）

RSM：路侧单元消息(Road Side Message)

RSI：路侧单元信息(Road Side Information)

SPAT：信号灯消息(Signal Phase And Timing Message)

TCS：牵引力控制系统（Traction Control System）

VIN：车辆识别码（Vehicle ID Number）

JSON：Javascript 对象简谱 （Javascript Object Notation ）

Protobuf：序列化数据结构协议 (Protocol Buffer)

MQTT ：消 息队列遥 测传输（ Message Queuing TelemetryTransport） 

# 云控基础平台架构及组成

本文件所指的云控基础平台可以集成车端、路侧、公共服务信息平台、第三方平台各种数据、服务、用户等各类资源，在此基础上提供车路协同应用数据集成分析、应用支撑能力和基础应用能力，以支撑各种自动驾驶、智能交通管理、智慧出行、公共安全等应用，是构建产业生态重要基础。

## 建设内容

云控基础平台总体架构见图1，主要分为区域子系统与中心子系统。

a） 路侧协同设施部署于路侧，通过通信网络接入区域子系统; 

b） 区域子系统接入中心子系统; 

c） 云控基础平台与地图、交管、气象、急救、警务等公共服务信息平台、其他第三方平台相连，进行对外部数据交互。

![image-20210812154830893](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812154830893.png)

## 云基础设施要求

云基础设施为V2X云控基础平台的各子系统提供虚拟化的计算、存储和网络资源，以及提供存储框架、计算框架等支撑能力。要求云基础设施对物理资源无锁定，采用高可用架构，具备资源弹性伸缩、数据容灾备份能力，并提供灵活高效的组网能力。

## 区域子系统功能与组成

区域子系统见图2，提供面向区域级交通监管以及域内车辆管理等提供服务，是单个或多个路侧协同设施信息的汇聚点。

![image-20210812154911329](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812154911329.png)

区域子系统组成可以有如下方式：

a) 由边缘云和区域云组成，边缘云向下与路侧协同设施连接，向上与区域云连接。

b) 由边缘云组成，边缘云向下与路侧协同设施连接，向上与中 心子系统连接。

c) 由区域云组成，区域云向下与路侧协同设施连接，向上与中 心子系统连接。

![image-20210812154933561](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812154933561.png)

### 平台基础能力

平台应采用功能模块化设计，并能够进行服务化封装，以方便不同功能模块之间的相互调用。基础平台应具有较强的弹性可扩展能力，以适应功能模块、数据资源、应用能力等的不断发展。

资源连接层：应实现区域子系统与路侧协同设施、中心子系统的互联互通，提供与路侧协同设施、中心子系统的接口。

数据处理层：应提供对各类数据的初步清洗、存储，并将数据与主题相关联，使数据进入相应的主题数据库。

数据分析层：应提供数据报表、可视化、知识库、数据分析工具及数据开放功能，为各类决策的产生提供支持数据可视化、数据挖掘功能。

### 基础应用能力 

可提供面向区域级交通监管、域内车辆管理、安全预警等服务。

交通监管：基于智能网联数据，对交通状态进行监控、管理，进行交通信号优化、交通态势分析、交通流预测、智慧公交线路优化等功能提升，从而提高交通安全性，优化交通通行效率。

车辆管理：实现各场景下的自动驾驶车队或第三方车队管理能力，并为其提供车辆管理、线路管理、线路下发、消息通知、远程控制等多种功能的应用支撑。

安全预警：为区域车辆提供安全预警。

## 中心子系统功能与组成

中心子系统汇聚各类系统的数据，提供融合、开放、共享的智能网联基础数据服务。中心子系统是区域子系统的数据汇聚点，可对接公安、交管、气象等各类与智能网联相关的政府业务平台，对接车企与车辆运营企业的车联网服务等第三方平台。中心子系统对海量数据进行结构化整理、存储，并通过统一的注册、审核、 发布、更新机制，将数据共享给产业链各方。具备全局性交通规划、区域协调能力。

![image-20210812155310251](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812155310251.png)

### 平台基础能力

开放接口服务：与外部平台实现互联互通，开放数据接口，接入道路管理系统、交通信号管理系统、实时路况、视频监控、高精度地图等交通信息，并提供 API 访问接口。

资源连接层：应实现中心子系统与区域子系统的互联互通，提供与区域子系统的接口。

数据处理层：应提供对各类数据的初步清洗、存储，并将数据与主题相关联，使数据进入相应的主题数据库。

数据共享层：应提供物理数据、经营数据、能力数据、用户数据、产品数据相关的主题数据库，供数据分析层调用。

数据分析层：应提供数据报表、可视化、知识库、数据分析工具及数据开放功能，为各类决策的产生提供支持数据可视化、数据挖掘功能。

### 综合应用能力

中心子系统需具备与智能交通管控平台及交通管控设备等进行信息交互的能力，服务于交通及产业。

交通监管：基于智能网联数据，对交通状态进行监控、管理，进行交通信号优化、交通态势分析、交通流预测、智慧公交线路优化、出行服务平台等功能提升，从而提高交通安全性，优化交通通行效率。

交通执法：基于开放共享的智能网联基础数据，实现有效支持各类交通主题的数字化云端执法服务，为政府部门、生产运营部门提供预警预判和管控纠察等基础数据。

车辆管理：应支持接入各场景下的自动驾驶车队或第三方车队管理平台，并为其提供运营展示、地图管理、账号管理、车辆管理、线路管理、线路下发、消息通知、远程控制等多种功能的应用支撑。

产业服务：为整车企业、一级供应商、科技生态企业等提供统一的标准化的智能网联数据和服务共享，推动数字交通、自动驾驶、智慧物流、智慧泊车等更多综合性车联网商业化应用。

测试服务：应具有测试管理、测试监控、远程控制、仿真测试、测试数据统计分析等功能。测试车辆在各个测试场景中的实时运行信息汇总上传到中心子系统，运用系统智能判别和人工评测的方式，对测试车辆的各项运行指标进行综合数据分析，并为云控应用场景验证提供试验测试依据。

# 云控基础平台信息交互数据定义与格式

为了实现中心子系统或区域子系统对路侧协同设施的配置、路侧协同设施上报数据的采集和分发，以及对路侧协同设施的运维管理等功能。制定包括车辆基本安全信息、交通运行信息等类型数据。

## 云控基础平台信息交互数据集

信息交互对象之间上行/下发的数据集如表 1 所示。

![image-20210812155447096](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812155447096.png)

## 云控基础平台信息交互数据格式

### 数据交换协议 

#### 路侧协同设施与区域子系统协议

路侧协同设施与区域子系统采用 MQTT/HTTP 协议通信，数据格式为 JSON/Protobuf/ASN.1。

#### 区域子系统与中心子系统协议 

区域子系统与中心子系统采用 MQTT/HTTP 协议通信，数据格式为 JSON/Protobuf。

### 数据分类格式

#### 应答

应答数据为上报数据的确认消息如表 2 所示。

![image-20210812155737423](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812155737423.png)

#### 车辆事件预警信息

##### 紧急制动事件预警

紧急制动事件信息定义如表 3 所示。

![image-20210812155836777](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812155836777.png)

##### 异常车辆事件预警

异常车辆事件信息定义如表 5 所示。

![image-20210812160243776](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812160243776.png)

异常车辆事件预警原因如表 6 所示。

![image-20210812160259406](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812160259406.png)

##### 交通事件/标志信息 RSI

交通事件/标志信息 RSI 定义如表 7 所示。

![image-20210812160317176](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812160317176.png)

交通事件类型如表 8 所示。 

![image-20210812160539175](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812160539175.png)

字段 Broadcast 如表 9 所示。

![image-20210812160550750](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812160550750.png)

交通事件/标志信息 RSI 数据下发删除定义如表 10 所示。

![image-20210812160804871](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812160804871.png)

##### 信号灯信息 SPAT

信号灯信息 SPAT 定义如表 11 所示。

![image-20210812160825663](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812160825663.png)

字段 Intersectionstate 说明定义如表 12 所示。

![image-20210812160842806](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812160842806.png)

字段 Phase 说明定义如表 13 所示。

![image-20210812160907975](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812160907975.png)

字段 Phasestate 说明定义如表 14 所示。

![image-20210812160919630](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812160919630.png)

字段 Timechangedetails 说明定义如表 15 所示。

![image-20210812160936279](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812160936279.png)

##### 设备信息查询接收

上层系统查询相关设备信息定义如表 16 所示。

![image-20210812160950967](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812160950967.png)

##### 设备信息上报

路侧协同设施上报相关设备信息，如表 17 所示。

上报频率：系统启动时和设备发生变化时主动上报，以及上层查询时进行上报。

![image-20210812161014935](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812161014935.png)

#### 交通运行信息

##### 路段信息

路段信息对象的具体定义如表 18 所示。

![image-20210812161035134](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812161035134.png)

##### 路口信息

路口信息对象的具体定义如表 19 所示。

![image-20210812161050033](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812161050033.png)

##### 区域信息

区域信息对象的具体定义如表 20 所示。

![image-20210812161108624](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812161108624.png)

##### 路段实时路况

路段实时路况对象的具体定义如表 21 所示。

![image-20210812161123247](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812161123247.png)

#### 业务配置下发

中心子系统/区域子系统包含全部区域的业务配置数据，且中心子系统/区域子系统可向路侧协同设施下发业务配置对其进行更新覆盖，路侧协同设施下发的业务配置上报到中心子系统/区域子系统进行存储，包括对 RSM、SPAT 消息的配置，配置为路侧协同设施上报这些数据的规则，路侧协同设施根据下发的业务配置全量覆盖本地配置并根据配置的规则执行，具体定义如表 22 所示。

![image-20210812161144303](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812161144303.png)

字段 Rsi 定义如表 23 所示。

![image-20210812161156934](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812161156934.png)

字段 Spatconfig 定义如表 24 所示。

![image-20210812161206016](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812161206016.png)

字段 Devconfig 定义如表 25 所示。

![image-20210812161219111](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812161219111.png)

#### 地图信息 MAP 下发

地图信息 MAP 下发定义如表 26 所示。

![image-20210812161235792](https://gitee.com/er-huomeng/l-img/raw/master/img/image-20210812161235792.png)

# 平台组网通信要求

## 路侧协同设施与区域子系统通信要求

a) 采用无线网络通信时延＜200ms，采用有线网络通信时延<100ms

b) 通信可靠性高于 99.9%；

## 区域子系统与中心子系统通信要求

a) 网络通信平均时延＜100ms；

b) 通信可靠性高于 99.9%； 

# 云控基础平台性能要求

a) 服务可用性不低于 99.9%，满足自动宕机迁移、自动快照备份等要求。

b) 服务的数据应有本地副本，数据持久性不低于 99.999%。

c) 满足资源弹性、自由配置要求，CPU、内存、带宽等关键资源可随时升级，升级配置数据不丢失，业务暂停时间可控。

d) 中心子系统软件架构应具备动态扩展接入不少于 200 万车辆的能力；区域子系统软件架构应具备动态扩展接入不少于 20 万车辆的能力。

# 云控基础平台安全要求

## 云基础设施安全可信要求

应满足租户隔离、存储安全、访问控制、运维审计、漏洞管理功能。

## 数据安全要求

a) 一般要求：保证数据可销毁性、数据可迁移性、数据私密性、数据完整性、数据备份和恢复功能；

b) 接入安全：提供面向连接对象和接入认证鉴权机制，提供安全的数据传送通道，提供数据传输和存储的加密机制。

c) 监控与分析数据保护：禁止对员工和授权用户的监控，或者在监控前需要通知用户或者获得用户的许可；禁止跨地理边界传输个人可识别信息（PII），或者在某个区域存储或者分析这类信息；敏感数据需要防止被篡改。

d) 配置和管理数据保护：安全管理维护不同时间安全的连贯性，不因操作过程而受到影响。安全元数据，例如连接状态和特征（加密

的或者认证过的），收集设备安全控制状态并分享给运营管理系统。

## 鉴权要求

云控基础平台应支持多 CA 下发及鉴权机制，支持与第三方平台的 Token 校验。