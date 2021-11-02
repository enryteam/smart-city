# 基于 ETC 专用短程通信的车路协同 第 2 部分：应用层数据交互格式

# 1 范围

本文件定义了基于专用短程通信（5.8GHz DSRC（ETC））的车路协同（I2V）系列应用中的术语和定义，以及数据集和数据交互格式等内容。 

本文件适用于基于5.8GHz DSRC系统的应用场景开发、验证及商用。 

# 2 规范性引用文件 

下列文件中的内容通过文中的规范性引用而构成本文件必不可少的条款。其中，注日期的引用文件，仅该日期对应的版本适用于本文件；不注日期的引用文件，其最新版本（包括所有的修改单）适用于本文件。

GB 2312 信息交换用汉字编码字符集 基本集 

GB 5768.2—2009 道路交通标志和标线 第2部分：道路交通标志 

GB/T 14886 道路交通信号灯设置与安装规范 

GB/T 20851.4—2019 电子收费 专用短程通信 第4部分：设备应用 

GB/T 29100—2012 道路交通信息服务 交通事件分类与编码 

T/ITS XXX—202X 基于ETC专用短程通信的车路协同 第1部分：应用集及应用数据交互需求 

# 3 术语和定义 

## 3.1 术语 

T/ITS XXX—202X 《基于ETC专用短程通信的车路协同 第1部分：应用集及应用数据交互需求》界定的术语和定义适用于本文件。 

## 3.2 缩略语 

下列缩略语适用于本文件。 

ASN.1：抽象语法标记（Abstract Syntax Notation One） 

B-KE：广播内核(Broad cast Kernel) 

DE：数据元素（Data Element） 

DF：数据帧（Data Frame） 

DSRC：专用短程通信（Dedicate Short Range Communication） 

ETC：电子收费（Electronic Toll Collection） 

ETC2.0：基于ETC专用短程通信的车路协同（Vehicle-Infrastructure Cooperative System Based On Electronic Toll Collection Dedicated Short Range Communication） 

I2V：路侧设施与车载单元通讯（Infrastructure to Vehicle） 

I-KE：初始化内核(Initialization Kernel)

OBU：车载单元（On-Board Unit） 

RSI：路侧交通消息（Road Side Information） 

RSM：路侧单元消息（Road Side Message） 

RSU：路侧单元（Road Side Unit） 

RTE：道路交通事件（Road Traffic Event） 

RTS：道路交通标志（Road Traffic Sign） 

SDU：服务数据单元（Service Data Unit） 

T-KE：传送内核(Transfer Kernel) 

UPER：非对齐压缩编码规则（Unaligned Packet Encoding Rules） 

# 4 ETC2.0 通信协议架构 

## 4.1 系统介绍 

基于ETC专用短程通信（5.8GHz DSRC）的无线通信技术，实现了智能运输系统的车路子系统之间的信息交互，从而实现道路安全、通行效率、信息服务等不同的应用。通信方式上，本文件对应的消息交互可采用广播类通信方式，也可以采用专用链路，后者具有更好的安全性，但交互效率略低。

![image-20211102162023802](https://gitee.com/er-huomeng/l-img/raw/master/image-20211102162023802.png)

## 4.2 协议栈架构 

ETC专用短程通信协议栈架构见图2，主要由物理层、数据链路层和应用层组成。应用层核心包含T-KE、B-KE、I-KE，T-KE提供I-KE以及应用所需的数据传输基础。 

面向车路协同的拓展应用消息定义在应用层SDU中，不对数据链路层和物理层做任何调整。由于ETC的数据交互速率较低，而车路协同信息量较大，在技术实现方式上采用全新消息编码，以用最少的字节传递尽量丰富的信息。

![Snipaste_2021-11-02_16-20-47](https://gitee.com/er-huomeng/l-img/raw/master/Snipaste_2021-11-02_16-20-47.png)

# 5 面向车路协同应用的协议扩展需求 

## 5.1 专有链路模式 

为在专用链路上支持ETC2.0车路协同应用，需要在已有的ACTION原语上进行扩展，用于传送播报的消息。ACTION原语采用ASN.1标准定义：

![image-20211102162126233](https://gitee.com/er-huomeng/l-img/raw/master/image-20211102162126233.png)

![image-20211102162137945](https://gitee.com/er-huomeng/l-img/raw/master/image-20211102162137945.png)

新增的车路协同消息集嵌套在actionParameter中。 

### 5.1.1 基本要求 

5.1.1.1 OBU 与 RSU 之间的 ETC 车路协同应用接口应符合 GB/T 20851.4—2019 的规定。 

5.1.1.2 为支持 ETC2.0 车路协同应用，对应用层服务原语 ACTION 扩展接口，新增 SetTrafficInfo 和GetTrafficInfo 原语，其中 ActionType 扩展定义： 

——ActionType = 7：SetTrafficInfo 

——ActionType = 8：GetTrafficInfo 

5.1.1.3 SetTrafficInfo 原语 

本原语用于完成OBU和RSU之间的双向认证，同时，通过该原语可安全的实现交通调度信息的发送以及对订阅信息等其他个性化信息的写入。 

5.1.1.4 GetTrafficInfo 原语 

本原语用于完成OBU和RSU之间的双向认证，同时，通过该原语可对返回的信息进行完整性保护。 

GetTrafficInfo主要用于获取订阅信息，其他信息根据实际应用场景可选。 

## 5.2 广播模式 

广播模式可采用ETC专用短程通信的BST信标服务信道进行消息的播报，BST的ASN.1定义如下：

![image-20211102162220368](https://gitee.com/er-huomeng/l-img/raw/master/image-20211102162220368.png)

新增的车路协同消息集嵌套在nonmandapplications中。 

# 6 应用层车路协同消息集格式

## 6.1 基本定义 

在应用层中新增面向车路协同应用的消息层，消息层中的数据集格式采用ASN.1标准进行定义，遵循“消息帧-消息体-数据帧-数据元素”层层嵌套的逻辑。 

数据编解码方式遵循UPER。 

## 6.2 消息层数据集定义 

本文件定义的消息层数据集，主要由1个消息帧格式，3个最基本的消息体以及相应的数据帧和数据元素组成。消息集的定义尽量适配LTE-V2X中消息集的定义。

![image-20211102162257857](https://gitee.com/er-huomeng/l-img/raw/master/image-20211102162257857.png)

### 6.2.1 消息帧 

消息帧是单个消息的统一打包格式。消息帧由不同类别的消息体组成，并支持扩展。

```ASN.1
-- Main message frame 
MessageFrame ::= CHOICE { 
	rsiETCFrame ETCRoadSideInformation, 
	-- 路侧消息播报 
	
	spatETCFrame ETCSPAT, 
	-- 红绿灯播报 
	
	msgETCFrame ETCMessage, 
	-- 纯文本消息播报 
	
	... 
}
```

### 6.2.2 消息体 

#### 6.2.2.1 Msg_ETCRSI 

【定义】

由路侧单元向周围车载单元发布的交通事件信息以及交通标志标牌信息。 

其中，交通事件信息当前支持国标GB/T 29100；交通标志信息当前支持国标GB 5768.2-2009。 

该消息帧能够打包一个或多个交通事件信息或者交通标志信息，同时包含发送该消息的路侧单元编号以及参考位置坐标。

路侧单元将交通事件类型、优先级、紧急程度等交通事件信息，以及MEC边缘计算或云平台对这些信息进行分析判断之后得出的交通决策结果，打包为本消息体所定义的格式，由路侧单元广播给周边车辆，供车辆驾驶员参考执行。 

与一般V2X业务流程不同的是，ETC2.0的RSI，路侧单元并不是仅仅把所收集的交通参与者信息发送给OBU，而是把交通决策结果也下发给OBU。这是因为ETC2.0场景下的OBU车载终端功能比较简单，不适合进行复杂的分析运算，因此把分析和判断处理放在MEC边缘计算和云平台。 

Msg_ETCRSI中的bearing方向角由MEC配置和下发，用作设定RSU播报事件需要覆盖的车道及播报方向，限定消息针对一个方向行驶的车辆，避免来向车辆或与该事件不相关车辆收到事件播报的情况。

```ASN.1
ETCRoadSideInformation ::= SEQUENCE { 
	id OCTET STRING (SIZE(4)), 
	-- RSU ID 
	idMsg INTEGER (0..255), 
	-- RSU发送给OBU的message ID，由MEC生成，防止相同消息重复接收 
	bearing BearingDataType, 
	-- 方向角，用于事件对应行驶路径方向判断 
	-- 正北为0，顺时针增加到360度 
	-- 方向角有效值0~360度，其中在传输过程中，将值扩大了100倍，即对应有效 值为0~36000，超出此范围内的值表示任意方向或者为无效 
	rtes ETCRTEList OPTIONAL, 
	-- All the rte data packed in this message 
	--包含全部道路交通事件数据 
	rtss ETCRTSList OPTIONAL, 
	-- All the rts data packed in this message 
	-- 包含全部道路交通标牌数据 
	... 
	}
```

#### 6.2.2.2 Msg_ETCSPAT 

【定义】

信号灯消息。包含了一个或多个路口信号灯的当前状态信息。结合路口位置信息，为车辆提供实时的前方信号灯相位信息。

```ASN.1
ETCSPAT ::= SEQUENCE { 
	id OCTET STRING (SIZE(4)), 
	-- RSU ID
    idSpat INTEGER (0..255), 
    -- 灯色消息ID，由MEC生成防止相同消息重复接收 
    bearing BearingDataType, 
    -- 方向角 
    spats SPATInfoList, 
    -- 灯色组信息 
    pos Position3D OPTIONAL,
    -- 路口位置信息 
    ... 
}
```

#### 6.2.2.3 Msg_ETCMSG 

【定义】

适用于由路侧单元向周围车载单元发布的本文类信息，适用于当ETCRSI消息不能准确描述事件信息时，用ETCMSG的文本类信息进行事件描述，如路名信息、事件影响范围信息等。

```ASN.1
ETCMessage ::= SEQUENCE { 
	id OCTET STRING (SIZE(4)), 
	-- RSU ID 
	idMsg INTEGER (0..255), 
	-- RSU发送给OBU的message ID，由MEC生成，防止相同消息重复接收 
	eventScen EventScenarios OPTIONAL, 
	-- Event scenarios 
	eventType EventType OPTIONAL, 
	-- 需要结合eventScen类型来综合判断 
	bearing BearingDataType, 
	-- 方向角 
	priority RSIPriority OPTIONAL, 
	-- The urgency of this message 
	--消息紧急程度 
	execNecessity ExecutionType OPTIONAL, 
	-- Necessity of executing suggestions 
	--执行建议必要性说明 
	description Description OPTIONAL, 
	-- Additional description to this message 
	--消息的附加说明 
	... 
}
```

### 6.2.3 数据帧（Data Frame） 

数据帧由其他数据单元或数据类型组合而成，具有特定的实际意义。是消息体的组成部分。 

#### 6.2.3.1 DF_ ETCRTEData 

【定义】

定义道路交通事件信息。交通事件分类当前支持国标GB/T 29100。该数据帧中，包含该交通事件的事件ID、ETC2.0应用场景、优先级、执行必要性、事件类型、发生区域、建议措施等。还可以用文本的形式，对事件信息进行补充描述或说明。 

其中，eventScen事件场景，为T/ITS XXXX—202X《基于ETC专用短程通信的车路协同 第1部分： 应用集及应用数据交互需求》中所定义的ETC2.0应用场景。

eventType事件类型，包括GB/T 29100中定义的交通事件类型，GB 5768.2—2009交通标志信息等，与eventScen有一定对应关系。如eventScen为恶劣交通环境感知预警时，eventType可为GB/T 29100—2012团雾、横风、暴雨等事件类型。

```ASN.1
ETCRTEData ::= SEQUENCE { 
	rteId INTEGER (0..255), 
	-- local ID of this rte information set by RSU 
	--RSU配置的RTE信息ID（本地的） 
	eventScen EventScenarios, 
	-- ETC2.0 event Scenarios defined in Part 1 
	--本文件第一部分定义的事件场景 
	priority RSIPriority OPTIONAL, 
	-- The urgency of this RSI data, a relative 
	-- degree of merit compared with other RSI data 
	--RSI数据紧急程度，参考其他RSI数据的相对值 
	execNecessity ExecutionType OPTIONAL, 
	-- Necessity of executing suggestions 
	--执行建议必要性说明 
	eventType EventType, 
	-- Type of event 
	-- need comprehensive justification combining eventScen 
	--事件类型，结合事件场景综合判断 
	suggestions Suggestions OPTIONAL, 
	-- Suggested action with regards to the event 
	--针对本事件的建议措施 
	eventPos PositionDescription OPTIONAL, 
	-- The position where the event happens 
	--事件发生的位置 
	description Description OPTIONAL, 
	-- Additional description to this event 
	--本事件附加说明 
	... 
}
```

#### 6.2.3.2 DF_ ETCRTEList 

【定义】

定义道路交通事件集合。 

至少包含1个道路交通事件信息，最多包含8个。

```ASN.1
ETCRTEList ::= SEQUENCE (SIZE(1..8)) OF ETCRTEData 
	--Road Traffic Event List 
	--道路交通事件列表
```

#### 6.2.3.3 DF_ ETCRTSData 

【定义】

定义道路交通标志信息。交通标志信息当前支持GB 5768.2—2009，包含其中所有标志内容。该数据帧中，可以用文本的形式，对相关的交通标志进行补充描述或说明。

```ASN.1
ETCRTSData ::= SEQUENCE { 
	rtsId INTEGER (0..255), 
	-- local ID of this rts information set by RSU 
	--由RSU配置的RTS信息ID号（本地的） 
	signType SignType, 
	-- Type of sign, according to China GB 5768.2—2009 
	--标识类型（参考GB 5768.2—2009） 
	description Description OPTIONAL, 
	-- Additional description to the sign 
	--标识附加说明 
	priority RSIPriority OPTIONAL, 
	-- The urgency of this RSI data, a relative 
	-- degree of merit compared with other RSI data 
	--RSI数据紧急程度，参考其他RSI数据的相对值 
	execNecessity ExecutionType OPTIONAL, 
	-- Execution necessity --执行必要性说明 
	signPos PositionDescription OPTIONAL, 
	-- Position of the traffic sign 
	--交通标识位置信息 
	... 
	}
```

#### 6.2.3.4 DF_ ETCRTSList 

【定义】

定义道路交通标志集合。 

至少包含1个道路交通标志信息，最多包含16个。

```ASN.1
RTSList ::= SEQUENCE (SIZE(1..16)) OF ETCRTSData
```

#### 6.2.3.5 DF_Description 

【定义】

定义文本描述信息。提供两种编码形式。 

提供ASCII字符文本形式，支持长度1字节到256字节。 

提供中文编码形式，符合GB 2312的编码规则，1个中文字符由2字节信息编码，支持长度1到128个中文字符。

```ASN.1
Description ::= CHOICE{ 
	textString IA5String (SIZE(1..256)), 
	-- ASCII text 
	--文本采用ASCII编码 
	textGB2312 OCTET STRING (SIZE(2..256)) 
	-- text using Chinese-character encoding GB 2312—1980 
	--中文编码格式使用GB 2312—1980 
	}
```

#### 6.2.3.6 DF_EventType 

【定义】

定义需要播报的事件类型，与EventScenarios形成对应；如eventScen为恶劣交通环境感知预警时，eventType可为TrafficEnvironment 中对应的团雾、横风、暴雨等事件类型（参考GB/T 29100-2012）。

```ASN.1
EventType ::= CHOICE { 
	vulRoadUser VulnerableRoadUser, 
	-- 1 对应于弱势交通参与者碰撞预警场景； 
	trfcEnv TrafficEnvironment, 
	-- 2 对应于恶劣交通环境感知预警场景； 
	trafficType TrafficType, 
	-- 3 对应于前方事故预警场景； 
	rampMerge RampMerge, 
	-- 4 对应于匝道合流预警场景，定义汇入类型； 
	congestionDegree CongestionDegree, 
	-- 5 对应于前方拥堵提醒场景，用于定义拥堵严重程度； 
	vehicleClass VehicleClassification, 
	-- 6 对应于特殊车辆提醒场景； 
	tollType TollType, 
	-- 9 对应于收费道路提醒（如拥堵收费）场景，用于定义收费类型 
	trafficControlType TrafficControlType; 
	--10 对应于交通调度管理场景，用于定义交通管制类型 
	intelligentStation IntelligentStation, 
	--11 对应于智慧场站指引场景，指示场站类型； 
	}
```

注：“7”（红绿灯信息播报）和“8”（车内标牌）通过专用报文下发，此处不再定义。 

#### 6.2.3.7 DF_PositionDescription

【定义】

定义交通事件发生的空间位置。 

——EventLane：事件定位（所属道路）。定义事件起始位置属于左起第几条车道。 

——LanesOccupied 事件定位（占用车道数）。定义事件占用车道数量。 

——EventDistance：事件定位（纵向：与 RSU 位置）。定义事件起点距离 RSU 的纵向距离。 

——Radius：事件定位（半径影响范围）。定义事件影响的范围。

——Position3D（可选）：事件三维位置坐标。（事件的经纬度、高程） 

——经纬度采用 wgs84 参考坐标系，下同。

```ASN.1
PositionDescription:: = SEQUENCE { 
	lane EventLane, 
	-- The path No. (from left) where the event happens 
	-- 0：未使用，忽略该值 
	lanesOccupied LanesOccupied, 
	-- No. of lanes the event occupied 
	-- 0：未使用，忽略该值 
	eventDistance EventDistance, 
	-- 定义事件起点距离RSU的纵向距离 
	-- 0: 未使用，忽略该值 
	eventRadius Radius, 
	-- 定义事件影响的范围 
	-- 0: 未使用，忽略该值 
	description Description OPTIONAL, 
	-- 描述信息，某些通过简单方式难以定位位置的，可以使用文本来描述 
	coordinate Position3D OPTIONAL, 
	-- 事件发生位置，经纬度表示 
	... 
	}
```

#### 6.2.3.8 DF_ Position3D 

【定义】

定义事件的三维的GPS坐标位置，经纬度和高程；该三维坐标位置信息由RSU发送给OBU，当ETC2.0 OBU与CAN总线相连（前装OBU），或配合地图（后装OBU）后精确显示事件定位时使用。

```ASN.1
Position3D ::= SEQUENCE { 
	lat Latitude, 
	-- in 1/10th micro degrees 
	--单位：1e-7度 
	lon Longitude, 
	-- in 1/10th micro degrees 
	--单位：1e-7度 
	elevation Elevation, 
	-- in 10 cm units 
	--单位：0.1米（m） 
	}
```

#### 6.2.3.9 DF_ SPATInfoList 

【定义】

定义信号灯灯色集合。 

至少包含1组信号灯灯色信息，最多包含8组。

```ASN.1
SPATInfoList ::= SEQUENCE (SIZE(1..8)) OF SPATInformation 
-- SPAT List 
--灯色信息列表
```

#### 6.2.3.10 DF_SPATInformation 

【定义】

信号灯灯色信息，包括灯组类型、灯色状态及当前状态剩余秒数。

```ASN.1
SPATInformation ::= SEQUENCE { 
	lightType LightType, 
	-- 灯组类型，当前十字路口，发送灯色信息的信号灯 
	lightState LightState, 
	-- 灯色状态 
	currentLeftTime SpatTimeDataType, 
	-- 剩余时间，单位：秒(s) 
	... 
	}
```

### 6.2.4 数据元素（Data Element） 

数据元素是消息体或数据单元的组成部分。它由基本数据类型定义产生，具有实际物理意义。 

#### 6.2.4.1 DE_ BearingDataType 

【定义】

定义方向角的数据类型。

```ASN.1
BearingDataType ::= INTEGER(0..36000)
```

#### 6.2.4.2 DE_ Suggestions 

【定义】

建议措施。定义针对本交通事件，建议相关车辆采取的执行措施。

```ASN.1
Suggestions ::= ENUMERATED { 
	unavailable (0), 
	-- 0：无效状态 
	stop (1), 
	-- 1：停车 
	slow (2), 
	-- 2：慢行 
	detour (3), 
	-- 3：绕道
	yield (4), 
	-- 4：让行 
	moveToLeft (5), 
	-- 5：靠左缓行 
	moveToRight (6), 
	-- 6：靠右缓行 
	pullOverToTheLeft (7), 
	-- 7：靠左停车 
	pullOverToTheRight (8), 
	-- 8：靠右停车 
	... 
	}
```

#### 6.2.4.3 DE_ EventScenarios 

【定义】

定义T/ITS XXXX—202X《基于ETC专用短程通信的车路协同 第1部分：应用集及应用数据交互需求》中所定义的应用场景。

```ASN.1
Scenari EventScenarios ::= ENUMERATED { 
	unknown (0), 
	-- 0：未定义； 
	vulnerableRoadUserCollisionWarning (1), 
	-- 1：弱势交通参与者碰撞预警； 
	severeTrafficEnvironmentWarning (2), 
	-- 2：恶劣交通环境感知预警； 
	trafficAheadWarning (3), 
	-- 3：前方事故预警； 
	rampMergingWarning (4), 
	-- 4：匝道合流预警； 
	trafficJamWarning (5), 
	-- 5：前方拥堵提醒； 
	emergencyVehicleWarning (6), 
	-- 6：特殊车辆提醒及优先通行； 
	signalPhaseandTimingBroadcasting (7), 
	-- 7：保留，红绿灯信息播报； 
	in-VehicleSignage (8), 
	-- 8：保留，车内标牌； 
	congestionTollWarning (9), 
	-- 9：拥堵收费提醒； 
	vehicleManagement (10), 
	--10：车辆调度与管理； 
	intelligentStationGuiding (11),
	--11：智慧场站指引； 
	... 
	}
```

#### 6.2.4.4 DE_ RSIPriority 

【定义】

消息优先级。定义消息的优先级属于紧急、一般还是次要。

```ASN.1
RSIPriority ::= ENUMERATED{ 
	unknown (0), 
	-- 0：未定义； 
	urgent (1), 
	-- 1：紧急的； 
	ordinary (2), 
	-- 2：一般； 
	minor (3), 
	-- 3：优先级低 
	... 
	}
```

#### 6.2.4.5 DE_ ExecutionType 

【定义】

执行必要性。定义OBU按照RSU下发的交通决策执行的必要性等级。

```ASN.1
ExecutionType ::= ENUMERATED{ 
	unknown (0), 
	-- 0：未定义； 
	required (1), 
	-- 1：必须执行 
	suggested (2), 
	-- 2：建议执行 
	optional (3), 
	-- 3：自由决定 
	... 
	}
```

#### 6.2.4.6 DE_ VulnerableRoadUser 

【定义】

定义弱势交通参与者类型，包括行人、自行车驾驶人、电动车驾驶人、摩托车驾驶人。

```ASN.1
VulnerableRoadUser ::= ENUMERATED{ 
	unknow (0), 
	pedestrian (1),
	--1：行人； 
	bicycleRider (2), 
	--2：自行车（含三轮车）驾驶人； 
	electricBikeRider (3), 
	--3：电动自行车驾驶人； 
	motorcycleRider(4), 
	--4：摩托车（含三轮摩托车）驾驶人； 
	... 
	}
```

#### 6.2.4.7 DE_ TrafficEnvironment 

【定义】

定义道路交通环境的类型，见附录A.1。 

其中，道路交通环境类型包括恶劣天气、异常路况。GB/T 29100-2012中定义的事件分类代码作为该值的千位和百位，交通事件分类顺序码作为该值的十位和个位。

```ASN.1
TrafficEnvironment ::= INTEGER (0..65535) 
-- Traffic environment type according to AppendixA.1 and China GB/T 29100-2012 
--交通环境类型（见附录 A.1 与 GB/T 29100-2012）
```

#### 6.2.4.8 DE_ TrafficType 

【定义】

定义道路交通事件的类型，见附录A.2。 

其中，道路交通事件参考GB/T 29100—2012中定义的交通事故。GB/T 29100—2012中定义的事件分类代码作为该值的千位和百位，交通事件分类顺序码作为该值的十位和个位。

```ASN.1
TrafficType ::= INTEGER (0..65535) 
-- Traffic event type according to AppendixA.2 and China GB/T 29100-2012 
--交通事件类型（见附录 A.2 与 GB/T 29100-2012）
```

#### 6.2.4.9 DE_ VehicleClassification 

【定义】

定义特殊车辆类型。紧急车辆类型参考《收费公路联网收费技术要求》中车种定义，包括普通车、公务车、军警车、紧急车、免费、车队等。

```ASN.1
VehicleClassification ::= INTEGER (0..255) 
-- 参考《收费公路联网收费技术要求》定义车辆种类 
-- 0：普通车；6：公务车；8：军警车；10：紧急车；12：免费；14：车队
```

#### 6.2.4.10 DE_ TollType 

【定义】

定义收费类型，用于拥堵收费等场景定义。

```ASN.1
TollType ::= ENUMERATED{ 
	unknow (0), 
	--0：未知类型 
	heavyTraffic (1), 
	--1：拥堵收费； 
	forbiddenFine (2), 
	--2：进入限制区域罚款； 
	... 
	}
```

6.2.4.11 DE_ TrafficControlType 

【定义】

定义交通管制类型。

```ASN.1
TrafficControlType ::= ENUMERATED{ 
	unknow (0), 
	--0：未知类型； 
	roadClosed (1), 
	--1：封路； 
	laneLimitation（2）, 
	--2：车道禁行； 
	VehicleTypeLimitation (3), 
	--3：车辆类型限行； 
	tailNumberLimitation (4), 
	--4：尾号限行； 
	timeLimitation（5） 
	--5：时段限行管制； 
	... 
	}
```

#### 6.2.4.12 DE_ SignType 

【定义】

定义道路交通标志的类型. 

数值 0 表示未知类型，或文本描述信息。大于 0 数值表示交通标志标牌信息，其编号参照国标 GB5768.2—2009 中“交通标志中文名称索引”表序号。

```ASN.1
SignType ::= INTEGER (0..65535) 
-- Value 0 means unknown type or using text description 
-- Traffic sign types refer to China GB 5768.2—2009 
--0 表示位置或文本描述，交通标识参考 GB 5768.2—2009
```

#### 6.2.4.13 DE_ CongestionDegree

【定义】

交通拥堵程度。定义交通事件发生路段的拥堵程度。

```ASN.1
CongestionDegree ::= ENUMERATED { 
	unavailable (0), 
	-- Not Equipped or unavailable 
	--信息不可用； 
	unimpeded (1), 
	--1：畅通； 
	basicallyUnblocked (2), 
	--2：基本畅通； 
	lightCongestion(3), 
	--3：轻度拥堵； 
	moderateCongestion (4), 
	--4：中度拥堵； 
	severeCongestion (5), 
	--5：严重拥堵； 
	... 
	}
```

#### 6.2.4.14 DE_IntelligentStation 

【定义】

定义智慧场站类型。（如停车场、加油站、充电站、服务区）。

```ASN.1
IntelligentStation ::= ENUMERATED { 
	undefined (0), 
	--0：未定义； 
	parkingLot(1), 
	--1：停车场； 
	gasStation(2), 
	--2：加油站； 
	chargingStation(3), 
	--3：充电站； 
	servicePoint(4), 
	--4：服务区； 
	parGas(5), 
	--5：停车场+加油站； 
	parGasCharg (6), 
	--6：停车场+加油站+充电站； 
	svrGas(7), 
	--7：服务区+加油站； 
	svrCharg (8),
	--8：服务区+充电站； 
	svrGasCharg (9), 
	--9：服务区+加油站+充电站； 
	... 
	}
```

#### 6.2.4.15 DE_RampMerge 

【定义】

定义匝道合流的情况（汇入/汇出）。

```ASN.1
RampMerge ::= ENUMERATED { 
	undefined (0), 
	--0：未定义； 
	otherVehicleAboutToMerge(1), 
	--1：定义主车在主路行驶，其他车辆从匝道汇入的情况； 
	aboutToMerge(2), 
	--2：定义主车即将从匝道汇入主路的情况； 
	collisionWarning(3), 
	--3：汇出碰撞安全提醒，如分流处有违停车辆、慢速车辆挡道，提醒后来车辆； 
	}
```

#### 6.2.4.16 DE_Latitude 

【定义】

定义纬度数值，北纬为正，南纬为负。 

分辨率 1e-7°。

```ASN.1
Latitude ::= INTEGER(-900000000..900000001) 
-- Units of 1/10 micro degree 
-- Providing a range of plus-minus 90 degrees 
--单位：1e-7 度，范围正负 90 度
```

#### 6.2.4.17 DE_ Longitude 

【定义】

定义经度数值。东经为正，西经为负。 

分辨率为 1e-7°。

```ASN.1
Longitude ::= INTEGER (-1800000000..1800000001) 
-- Units of 1/10 micro degree 
-- Providing a range of plus-minus 180 degrees 
--单位：1e-7 度，范围正负 180 度
```

#### 6.2.4.18 DE_Elevation 

【定义】

定义事件海拔高程。 

分辨率为 0.1 米(m)。数值-4096 表示无效数值。

```ASN.1
Elevation ::= INTEGER (-4096..61439) 
-- In units of 10 cm steps above or below the reference ellipsoid 
-- Providing a range of -409.5 to + 6143.9 meters 
-- The value -4096 shall be used when Unknown is to be sent 
--单位：0.1 米（m），范围-409.5 到 6143.9 米（m），-409.6 表示未知
```

#### 6.2.4.19 DE_ EventDistance 

【定义】

EventDistance：事件定位（纵向：与 RSU 位置）。定义事件起点距离 RSU 的纵向距离。

```ASN.1
EventDistance ::= INTEGER (-32768..32767) 
-- 距离，单位：米（m） 
-- 注意：当为负数的时候，表示事件位置在 RSU 定向的反方向上，如提示后方有紧 急车辆，注意避让。 
-- 0：未定义
```

#### 6.2.4.20 DE_ EventLane （一个字节，127 车道） 

【定义】

事件定位（所属道路）。定义事件所处道路属于左起第几条车道。

```ASN.1
EventLane ::= INTEGER (0..127)
```

#### 6.2.4.21 DE_ LanesOccupied 

【定义】

LanesOccupied 事件定位（占用车道数）。定义事件占用车道数量。

```ASN.1
LanesOccupied ::= INTEGER (0..127) -- 0：未定义
```

#### 6.2.4.22 DE_ Radius 

【定义】

事件定位（绝对值半径大小）。定义事件影响的半径范围。

```ASN.1
Radius ::= INTEGER (0..65535) 
-- Define radius 
-- Unit is 1m 
-- 0：未定义，单位：米(m)
```

#### 6.2.4.23 DE_ SpatTimeDataType 

【定义】

当前灯色剩余时间，单位：秒（s）。

```ASN.1
SpatTimeDataType ::= INTEGER (0..65535)
```

#### 6.2.4.24 DE_ LightType 

【定义】

信号灯类型。

```ASN.1
LightType ::= ENUMERATED { 
	unavailable (0), 
	--0：未知或错误 
	pedestrianType0 (1), 
	--1：行人； 
	pedestrianType1 (2), 
	--2：行人一段； 
	pedestrianType2 (3), 
	--3：行人二段； 
	vehicleType0 (4), 
	--4：机动车满屏； 
	vehicleType1 (5), 
	--5：机动车左转； 
	vehicleType2 (6), 
	--6：机动车直行； 
	vehicleType3 (7), 
	--7：机动车右转； 
	vehicleType4 (8), 
	--8：机动车掉头； 
	transitType0 (9), 
	--9：公交满屏； 
	transitType1 (10), 
	--10：公交左转； 
	transitType2 (11), 
	--11：公交直行； 
	transitType3 (12), 
	--12：公交右转； 
	nonMotorType0 (13), 
	--13：非机动车满屏； 
	nonMotorType1 (14), 
	--14：非机动车左转；
	nonMotorType2 (15), 
	--15：非机动车直行； 
	nonMotorType3 (16), 
	--16：非机动车右转； 
	tidalLane (17), 
	--17：潮汐车道； 
	leftTurnScreen (18), 
	--18：借道左转屏； 
	rightTurnScreen (19), 
	--19：借道右转屏； 
	leftVariableLaneScreen (20), 
	--20：可变车道屏（左转）； 
	lineVariableLaneScreen (21), 
	--21：可变车道屏（直行）； 
	leftlineVariableLaneScreen (22), 
	--22：可变车道屏（左转+直行）； 
	... 
	}
```

#### 6.2.4.25 DE_ LightState 

【定义】

定义信号灯相位的灯色状态。支持 GB 14886 规定的红、绿、黄三种信号灯灯色，以及亮灯、闪烁和熄灭三种状态。对于绿灯状态，在应用实现时应参考实际路口的情况，选择采用通行允许相位(permissive-green)或通行保护相位(protected-green)。

```ASN.1
LightState ::= ENUMERATED { 
	unavailable (0), 
	-- This state is used for unknown or error 
	--未知错误 
	dark (1), 
	-- The signal is dark (unlit) 
	--信号灯处于熄灭状态 
	
	-- Reds 
	--红灯相关状态 
	flashing-red (2), 
	-- Reserved for special scenarios 
	--保留 
	red (3), 
	-- Driver Action: 
	-- Stop vehicle at stop line. 
	-- Do not proceed.
	--驾驶员动作：停止线前停车，勿越线。 
	
	-- Greens --绿色灯相关状态 
	flashing-green (4), 
	-- Reserved for special scenarios
    --保留 
    permissive-green (5), 
    -- Driver Action: 
    -- Proceed with caution, 
    -- must yield to all conflicting traffic 
    -- Conflicting traffic may be present 
    -- in the intersection conflict area 
    --驾驶员动作：谨慎通过路口。注意路口可能有其他方向绿灯通行车辆行驶。 
    protected-green (6), 
    -- Driver Action: 
    -- Proceed, tossing caution to the wind, 
    -- in indicated (allowed) direction. 
    --驾驶员动作：按指示灯通行，谨慎通过路口。 
    -- Yellows / Ambers 
    -- The vehicle is not allowed to cross the stop bar if it is possible 
    -- to stop without danger. 
    --黄灯。未通过停止线的车禁止继续通行。 
    yellow (7),
    -- Driver Action: 
    -- Prepare to stop. 
    -- Proceed if unable to stop, 
    -- in indicated direction (to connected lane) 
    -- Clear Intersection. 
    --驾驶员动作：随时准备停车，观察安全后谨慎驶离路口。若无停车条件继续谨 慎驶离路口。 
    flashing-yellow (8) , 
    -- Driver Action: 
    -- Proceed with caution, 
    -- Conflicting traffic may be present 
    -- in the intersection conflict area 
    --驾驶员动作：谨慎驾驶，在交叉路口留意可能的其他方向绿灯通行车辆。 
    ... 
    }
```

# 附录A 交通事件索引

## A.1 DE_TrafficEnvironment（交通环境索引）类型及取值

表A.1给出了交通环境索引类型及取值。

![image-20211102161552569](https://gitee.com/er-huomeng/l-img/raw/master/image-20211102161552569.png)

![image-20211102161602290](https://gitee.com/er-huomeng/l-img/raw/master/image-20211102161602290.png)

## A.2 DE_TrafficType（交通事故索引）类型及取值 

表A.2给出了交通环境索引类型及取值。

![image-20211102161617488](https://gitee.com/er-huomeng/l-img/raw/master/image-20211102161617488.png)

