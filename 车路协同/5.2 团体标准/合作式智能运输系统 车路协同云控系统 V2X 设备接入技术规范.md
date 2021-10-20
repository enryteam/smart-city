# 合作式智能运输系统 车路协同云控系统 V2X 设备接入技术规范

# 引 言 

本文件是围绕智能网联汽车测试示范互通性与互认性，调研和梳理合作式智能运输系统现有数据监控的需求，梳理主流车路协同应用分类，定义监控数据类型及划数据项采集范围，建立传输机制并规范传输协议，作为国家标准的补充与扩展，支撑车联网应用和车联网设备之间搭建高效、稳定、安全的应用平台，降低车联网企业研发、运营和运维成本，提高车联网项目的落地能力，促进车路协同产业发展。

# 1 范围

本文件规定了合作式智能运输系统车路协同云控系统V2X设备接入要求和对应的交互数据技术要求。 

本标准适用于基于LTE的车联网无线通信技术消息层的设计与开发。 

本文件适用于合作式智能运输系统车路协同云控系统V2X设备接入的设计与开发。

# 2 规范性引用文件 

下列文件对于本文件的应用是必不可少的。凡是注日期的引用文件，仅注日期的版本适用于本文件。 

凡是不注日期的引用文件，其最新版本（包括所有的修改单）适用于本文件。 

YD/T 3709-2020 基于LTE的车联网无线通信技术 消息层技术要求 

T/CSAE 53-2020 合作式智能运输系统 车用通信系统 应用层及应用数据交互标准 

T/ITS 0097-2018 合作式智能运输系统 通信架构 

T/CSAE 157-2020 合作式智能运输系统 车用通信系统 应用层及应用数据交互标准

# 3 术语和定义 

下列术语和定义适用于本文件 

## 3.1 术语 

### 3.1.1 合作式智能运输系统 cooperative intelligent transportation system，C-ITS 

合作式智能运输系统是智能运输系统的一种，包含各智能运输系统站之间交流和分享信息的工具， 旨在提供建议或采取措施提高独立智能运输系统范围之外的安全性、可持续性、效率和舒适性。 

### 3.1.2 车路协同云控平台 car road collaboration cloud control platform 

车联网V2X云控平台主要是面向智能网联汽车“车路云一体”数字化设施建设，是智慧交通的综合管理支撑平台，解决智能网联汽车存在的信息孤岛，难以互联协同、有效管控的问题，通过定义互相可靠的信息交互规则，实现车与车、车与基础设施、车与平台之间数据的互联互通。将各种实时的动态信息汇集到V2X云控平台，通过对多源数据的建模分析，为辅助驾驶和自动驾驶提供安全、可靠的规划决策。提高驾驶的安全性和通行效率，同时提供个性化的内容服务。 

### 3.1.3 物联网 internet of things，IOT 

物联网是一个基于互联网、传统电信网等信息承载体，让所有能够被独立寻址的普通物理对象实现互联互通的网络。它具有普通对象设备化、自治终端互联化和普适服务智能化3个重要特征。具体来说，物联网的体系自下而上可以分成五个层级，分别是感知层、接入层、网络层、服务管理层以及应用层。

一句话概括：把所有物品通过信息传感设备与互联网连接起来，进行信息交换，即物物相息，以实现智 

能化识别和管理。 

### 3.1.4 车联网 internet of vehicles，IOV 

车联网的概念源于物联网，即车辆物联网，是以行驶中的车辆为信息感知对象，借助新一代信息通信技术，实现车与X（即车与车、人、路、服务平台）之间的网络连接，提升车辆整体的智能驾驶水平， 为用户提供安全、舒适、智能、高效的驾驶感受与交通服务，同时提高交通运行效率，提升社会交通服务的智能化水平。 

### 3.1.5 物模型 thing specification language，TSL 

物模型指将物理空间中的实体数字化，并在云端构建的该实体的数据模型，用于描述实体的功能。 TSL是一个JSON格式的文件。它是物理空间中的实体，如传感器、车载装置、楼宇、工厂等在云端的数字化表示，从属性、功能和事件三个维度，分别描述了该实体是什么、能做什么、可以对外提供哪些信息。定义了物模型的这三个维度，即完成了产品功能的定义。 

### 3.1.6 V2X 

车载单元与其他设备通信，包括但不限于车载单元之间通信（V2V），车载单元与路侧单元通信（V2I）， 车载单元与行人设备通信（V2P），车载单元与网络之间通信（V2N）。 

## 3.2 缩略语 

下列缩略语适用于本文件。 

ASN.1：抽象语法标记（Abstract Syntax Notation One） 

BSM：基本安全消息 (Basic Safety Message) 

C-ITS 合作式智能运输系统 (Cooperative Intelligent Transportation System) 

CLPMM：编队管理消息（Connectionless Platooning Management Message） 

OBU：车载单元（On-Board Unit） 

PAM：停车场地图（Parking Area Map） 

PSM：个体安全消息（Personal Safety Message） 

PSU：个人服务单元(Personal Service Unit) 

RSC：路侧协调消息（Road Side Coordination） 

RSI：路侧单元发布的交通事件消息 Road Side Information 

RSM：路侧单元消息 (Road Side Message) 

RSU：路侧单元（Road Side Unit） 

RTS: 道路收费服务（Road Tolling Service） 

SDS：感知数据共享（Sensor Data Sharing） 

SPAT：信号灯相位与配时消息（Signal Phase and Timing Message） 

SSM：感知共享消息（Sensor Sharing Message）

TSL: 物模型 (Thing Specification Language) 

UPER：非对齐压缩编码规则（Unaligned Packet Encoding Rules） 

V2I：车载单元与路侧单元通讯（Vehicle to Infrastructure） 

V2P：车载单元与行人设备通讯（Vehicle to Pedestrians） 

V2V：车载单元之间通讯（Vehicle to Vehicle） 

V2X：车载单元与其他设备通讯（Vehicle to Everything） 

VIR：车辆意图和请求（Vehicle Intention And Request） 

VPM：车辆支付消息（Vehicle Payment Message） 

VRU：弱势交通参与者（Vulnerable Road User） 

VRUSP: 弱势交通参与者安全通行（Vulnerable Road User Safe Passing） 

# 4  合作式智能运输系统 车路协同云控系统 

## 4.1 系统介绍 

合作式智能运输系统-车路协同云控系统为V2X设备提供安全可靠的连接通信能力，向下连接海量V2X设备，支撑V2X设备数据采集上云；向上提供云端API，服务端通过调用云端API将指令下发至V2X设备端，实现设备管理、远程控制、监控运维等能力，详见图1。V2X设备与平台之间通过物模型（物模型是指将物理空间中的实体数字化，并在云端构建该实体的数据模型）实现消息通信。物模型可以屏蔽底层设备差异，让软件开发者基于平台提供的标准API进行开发，让硬件开发者基于平台提供的标准协议开发，从而达到软硬开发解耦的目的使用物模型接入物联网平台，简化接入流程和软硬件开发，同时可以更好地支持设备的扩展。

![image-20211013184406898](https://gitee.com/er-huomeng/l-img/raw/master/image-20211013184406898.png)

## 4.2  应用层与交互数据 

本文件围绕智能网联汽车测试示范互通性与互认性，调研和梳理合作式智能运输系统现有数据监控的需求，界定监控数据类型及采集数据项范围，定义V2X设备监控管理的应用以及支撑这些应用的交互消息集合（数据帧、数据元素、数据结构和具体的编码方式等）。

本文件通过对主流物联网平台的分析，定义在实现V2X设备监控管理应用时，V2X设备和云控平台间的信息交互内容与交互协议等。为了降低整体产业开发成本和周期，本文件不指定具体的通信协议，用户可以使用开放协议（如MQTT、Coap、HTTPS等物联网传输协议）自主接入V2X设备，实现设备上报属性和事件信息，平台下发设置属性和调用服务指令；不限定具体的数据格式，使用ASN.1记录V2X设备物模型数据内容，用户可以选择ASN.1格式或相应的其他数据格式（如JSON、XML等）。 

# 5 车路协同云控系统 V2X 设备接入应用 

## 5.1 设备认证 

设备接入系统之前，需通过身份认证，车路协同云控系统应支持使用设备密钥和X.509证书等方式进行身份认证，并使用 TLS/DTLS 保证通道安全。 

## 5.2 设备影子 

系统提供设备影子功能，用于缓存设备状态。设备在线时，可以直接获取云端指令；设备离线后， 再次上线可以主动拉取云端指令。 

## 5.3 远程登陆 

系统支持远程登录功能，用户可以远程控制和管理设备。远程连接基于SSH技术实现，方便用户远程登录设备进行设备控制和管理（其使用的用户名和密码是设备的用户名与密码）。 

## 5.4 远程重启 

系统支持的远程重启功能，用户可以远程重启设备。 

## 5.5 远程配置 

系统支持的远程配置功能，用户可以在线远程更新设备的系统参数、网络参数等配置信息。 

## 5.6 远程升级 

系统支持OTA升级与管理服务。 

## 5.7 日志上报 

系统支持设备本地日志的上报，用户可以在线查询V2X设备本地日志，进行故障分析。 

## 5.8 PC5 通信统计 

系统支持V2X设备上报PC5接口的通信数据，用户可以在线分析PC5接口的信道忙率、单向时延、 

丢包率等指标。 

# 6 消息层交互数据技术要求 

## 6.1 消息层基本介绍和要求 

消息层数据集用ASN.1标准进行定义，遵循“消息帧-消息体-数据帧-数据元素”层层嵌套的逻辑进行制定。

数据集交互的编解码方式遵循非对齐压缩编码规则UPER（Unaligned Packet Encoding Rules）。 

## 6.2 消息层数据集定义 

基于车联网开发领域设计的合作式智能运输系统车路协同云控系统V2X设备接入，消息层所涉及的 数据集，主要由1个消息帧格式，3个基本的消息体以及相应的数据帧和数据元素组成，详见图2。

![image-20211013184520620](https://gitee.com/er-huomeng/l-img/raw/master/image-20211013184520620.png)

### 6.2.1 消息帧 

消息帧是单个应用层消息的统一打包格式，是数据编解码的唯一操作对象。消息帧由不同类别的消息体组成，并支持扩展。

```ASN.1
【ASN.1 代码】 
-- Main message frame 
MessageFrame ::= SEQUENCE { 
    timestamp INTEGER, 
    messageId NumericString, 
    deviceId NumericString, 
    payload Payload 
}
Payload ::= CHOICE { 
    property Property, 
    funtion Function, 
    event Event 
}
```

### 6.2.2 消息体（Message） 

#### 6.2.2.1 Msg_Property 

【定义】

属性。一般用于描述设备运行时的状态，如设备 SN、当前 CPU 使用率、环境监测设备所读取的当前环境温度等。平台可主动下发消息获取设备属性,设备也通过事件上报属性等。

```ASN.1
【ASN.1 代码】 
Property ::= CHOICE {
    reportProperty ReportProperty,
    readPropertyRequest ReadPropertyRequest, 
    readPropertyResponse ReadPropertyResponse, 
    writePropertyRequest WritePropertyRequest, 
    writePropertyResponse WritePropertyResponse 
}
```

#### 6.2.2.2 Msg_Function 

【定义】

功能一般指可被外部调用的能力或方法，可设置输入参数和输出参数。相比于属性，功能可通过一条指令实现更复杂的业务逻辑，如执行某项特定的任务。平台可主动调用设备功能,例如: 播放语音,开关操作等。 

```ASN.1
【ASN.1 代码】 
Function ::= SEQUENCE { 
    funtionId FUNTION-ID-AND-TYPE.&id ({FunctionTypes}), 
	parameters FUNTION-ID-AND-TYPE.&Type ({FunctionTypes} {@.funtionId}), 
	...
}

FUNTION-ID-AND-TYPE ::= CLASS { 
    &id FuntionId UNIQUE, 
    &Type 
}

WITH SYNTAX { 
    &Type IDENTIFIED BY &id 
}

FunctionTypes FUNTION-ID-AND-TYPE ::= { 
    {LogReport IDENTIFIED BY logSwitch} | 
	{RemoteLogin IDENTIFIED BY remoteLogin} | 
	{RemoteRestart IDENTIFIED BY remoteRestart} | 
	{PC5CommStatistics IDENTIFIED BY commStatistics} | 
	{RemoteConfig IDENTIFIED BY remoteConfig} | 
	{Fota IDENTIFIED BY fota}, 
	... 
}

FuntionId ::= ENUMERATED {remoteLogin, remoteRestart, remoteConfig, commStatistics, logSwitch, fota, ...} 

remoteLogin FuntionId ::= remoteLogin
remoteRestart FuntionId ::= remoteRestart 
remoteConfig FuntionId ::= remoteConfig 
commStatistics FuntionId ::= commStatistics 
logSwitch FuntionId ::= logSwitch fota FuntionId ::= fota
```

#### 6.2.2.3 Msg_Event 

【定义】

事件一般包含需要被外部感知和处理的通知信息，可包含多个输出参数。如，某项任务完成的信息， 或者设备发生故障或告警时的温度等，事件可以被订阅和推送。

```ASN.1
【ASN.1 代码】 
Event ::= SEQUENCE { 
    eventId EVENT-ID-AND-TYPE.&id ({EventTypes}), 
	data EVENT-ID-AND-TYPE.&Type ({EventTypes} {@.eventId}), 
	... 
}

EVENT-ID-AND-TYPE ::= CLASS { 
    &id EventId UNIQUE, 
    &Type 
}

WITH SYNTAX { 
    &Type IDENTIFIED BY &id 
}

EventTypes EVENT-ID-AND-TYPE ::= { 
    {PC5CommRecord IDENTIFIED BY pC5CommRecord} | 
	{UpgradeProgressReport IDENTIFIED BY upgradeProgress}, 
	... 
}

EventId ::= ENUMERATED {pC5CommRecord, upgradeProgress, ...} 

pC5CommRecord EventId ::= pC5CommRecord 
upgradeProgress EventId ::= upgradeProgress
```

### 6.2.3 数据帧（Data Frame） 

数据帧由其他数据单元或数据类型组合而成，具有特定的实际意义。是消息体的组成部分。

#### 6.2.3.1 DF_PropertyKVPList 

【定义】

定义 V2X 设备属性列表。

```ASN.1
【ASN.1 代码】 
PropertyKVPList ::= SEQUENCE OF PropertyKVP
```

#### 6.2.3.2 DF_PropertyKVP 

【定义】

定义 V2X 设备设备属性。

```ASN.1
【ASN.1 代码】 
PropertyKVP ::= SEQUENCE { 
    id PROPERTY-ID-AND-TYPE.&id ({PropertyTypes}), 
	value PROPERTY-ID-AND-TYPE.&Type ({PropertyTypes} {@.id}), 
	... 
}

PROPERTY-ID-AND-TYPE ::= CLASS { 
    &id PropertyId UNIQUE, 
    &Type 
}

WITH SYNTAX { 
    &Type IDENTIFIED BY &id 
}

PropertyTypes PROPERTY-ID-AND-TYPE ::= { 
    {DeviceBasicInfo IDENTIFIED BY basic} | 
	{DeviceHealthInfo IDENTIFIED BY health} | 
	{DevicePerformanceInfo IDENTIFIED BY performance} |
	{Cv2xMessageList IDENTIFIED BY cv2xMessages}, 
	... 
}

PropertyId ::= ENUMERATED {basic, health, performance, cv2xMessages, ...}
                           
basic PropertyId ::= basic health 
PropertyId ::= health performance 
PropertyId ::= performance cv2xMessages 
PropertyId ::= cv2xMessages
```

#### 6.2.3.3 DF_ReportProperty 

【定义】

定义 V2X 设备上报设备属性消息。

```ASN.1
【ASN.1 代码】 
ReportProperty ::= PropertyKVPList
```

#### 6.2.3.4 DF_ReadPropertyRequest 

【定义】

定义平台向 V2X 设备发起的读取属性请求消息。

```ASN.1
【ASN.1 代码】 
ReadPropertyRequest::=SEQUENCE OF PROPERTY-ID-AND-TYPE.&id ({PropertyTypes})
```

#### 6.2.3.5 DF_ReadPropertyResponse 

【定义】

定义平台向 V2X 设备发起的读取属性请求消息的回应消息。

```ASN.1
【ASN.1 代码】 
ReadPropertyResponse ::= SEQUENCE { 
    success BOOLEAN, 
    error UTF8String OPTIONAL, --失败原因 
    properties PropertyKVPList OPTIONAL 
}
```

#### 6.2.3.6 DF_WritePropertyRequest 

【定义】

定义平台向 V2X 设备发起的设置属性请求消息。

```ASN.1
【ASN.1 代码】 
WritePropertyRequest ::= PropertyKVP
```

#### 6.2.3.7 DF_WritePropertyResponse 

【定义】

定义平台向 V2X 设备发起的设置属性请求消息的回应消息。

```ASN.1
【ASN.1 代码】 
WritePropertyResponse ::= SEQUENCE { 
    success BOOLEAN, 
    error UTF8String OPTIONAL, --失败原因 
    properties PropertyKVP OPTIONAL
}
```

#### 6.2.3.8 DF_RemoteLogin 

【定义】

定义 V2X 设备远程登陆功能消息。

```ASN.1
【ASN.1 代码】 
RemoteLogin ::= CHOICE { 
    inputs RemoteLoginInputs, 
    outputs RemoteLoginOutputs 
}
```

#### 6.2.3.9 DF_RemoteRestart 

【定义】

定义 V2X 设备远程重启功能消息。

```ASN.1
【ASN.1 代码】 
RemoteRestart ::= CHOICE { 
    inputs RemoteRestartInputs, 
    outputs RemoteRestartOutputs 
}
```

#### 6.2.3.10 DF_RemoteConfig 

【定义】

定义 V2X 设备远程配置功能消息。

```ASN.1
【ASN.1 代码】 
RemoteConfig ::= CHOICE { 
    inputs RemoteConfigInputs,
    outputs RemoteConfigOutputs 
}
```

#### 6.2.3.11 DF_PC5CommStatistics 

【定义】

定义 V2X 设备 PC5 接口收发数据统计功能消息。 

```ASN.1
【ASN.1 代码】 
PC5CommStatistics ::= CHOICE { 
    inputs PC5CommStatisticsInputs, 
    outputs PC5CommStatisticsOutputs 
}
```

#### 6.2.3.12 DF_LogReportSwitch 

【定义】

定义 V2X 设备本地日志上报开关功能消息。

```ASN.1
【ASN.1 代码】 
LogReportSwitch ::= CHOICE { 
    inputs LogReportInputs, 
    outputs LogReportOutputs 
}
```

#### 6.2.3.13 DF_Fota 

【定义】

定义 V2X 设备 OTA 升级功能消息。

```ASN.1
【ASN.1 代码】 Fota ::= CHOICE { 
    inputs FotaInputs, 
    outputs FotaOutputs 
}
```

#### 6.2.3.14 DF_PC5CommRecord 

【定义】

定义 V2X 设备 PC5 接口通信数据记录事件消息。

```ASN.1
【ASN.1 代码】 
PC5CommRecord ::= SEQUENCE { 
    type PC5CommType, 
    id OCTET STRING (SIZE (8)), 
	--The temperary vehicle ID or RSU ID in the packet 
	sendOrRecvTime INTEGER, 
	signOrVerifyTime TIME OPTIONAL, 
	signOrVerifyResult BOOLEAN OPTIONAL, 
	cbr REAL, 
	dsmpPayload OCTET STRING 
}
```

#### 6.2.3.15 DF_UpgradeProgressReport 

【定义】

定义 V2X 设备 OTA 升级进度上报事件消息。

```ASN.1
【ASN.1 代码】 
UpgradeProgressReport ::= SEQUENCE { 
    firmwareId IA5String,
    progress INTEGER, 
    version UTF8String, 
    complete BOOLEAN OPTIONAL, 
    success BOOLEAN OPTIONAL, 
    error UTF8String OPTIONAL 
}
```

#### 6.2.3.16 DF_DeviceBasicInfo 

【定义】

定义 V2X 设备基本信息属性消息。

```ASN.1
【ASN.1 代码】 
DeviceBasicInfo ::= SEQUENCE { 
    id IA5String, --设备编号，平台唯一 
    esn IA5String, --设备电子序列号 
    name IA5String, --设备名称 
    type DeviceType, --设备类型 
    supplier IA5String, --设备供应商 
    swVersion IA5String, --软件版本 
    hwVersion IA5String, --硬件版本 
    protocolVersion IA5String, --协议版本 
    organization IA5String, --设备归属 
    installationTime INTEGER, --设备安装时间戳（13位） 
    currentLocation Position3D, --设备当前位置 
    supportedCommModes IA5String, --设备支持的通信方式 
    runningCommModes IA5String, --设备当前使用的通信方式 
    centerAddress IA5String --中心子系统地址 
}
```

#### 6.2.3.17 DF_DeviceHealthInfo 

【定义】

定义 V2X 设备运行状况属性消息。

```ASN.1
【ASN.1 代码】 
DeviceHealthInfo ::= SEQUENCE { 
    storageCapacity INTEGER, --存储容量 
    appSoftware AppSoftware, --应用和软件状态 
    timeService TimeServiceStatus, --时间服务状态 
    cellular CellStatus, --蜂窝网工作状态，此处特指4G/5G 
    ethernet EthStatus, --以太网工作状态 
    v2x V2XStatus, --V2X工作状态 
    gnss GNSSstatus, --GNSS工作状态
    wifi WifiStatus, --WIFI工作状态 
    hsm HSMStatus --安全模块工作状态 
}
```

#### 6.2.3.18 DF_DevicePerformanceInfo 

【定义】

定义 V2X 设备性能属性消息。

```ASN.1
【ASN.1 代码】 
DevicePerformanceInfo ::= SEQUENCE { 
	cpu CpuInfo, 
	mem MemInfo, 
	net NetInfo, 
	disk DiskInfo, 
	temp INTEGER, 
	uptime UTF8String 
	-- Unix 命令，显示系统已经运行了多长时间 
	--它依次显示下列信息：当前时间、系统已经运行了多长时间、有多少登陆用户 
	--系统在过去的1分钟、5分钟和15分钟内的平均负载。 
}
```

#### 6.2.3.19 DF_Cv2xMessageList 

【定义】

定义 V2X 设备的部署的 CV2X 消息内容。

```ASN.1
【ASN.1 代码】 
Cv2xMessageList ::= SEQUENCE OF MessageFrame 
-- MessageFrame 见 T/CSAE 53-2017、T/CSAE 157-2020
```

#### 6.2.3.20 DF_UpgradeProgressReport 

【定义】

定义 V2X 设备 CPU 信息。

```ASN.1
【ASN.1 代码】 
CpuInfo ::= SEQUENCE { 
	us REAL, --表示用户空间程序的cpu使用率（没有通过nice调度） 
	sy REAL, --表示系统空间的cpu使用率，主要是内核程序 
	ni REAL, --表示用户空间且通过nice调度过的程序的cpu使用率 
	id REAL, --CPU 空闲时间比 
	wa REAL, --cpu运行时在等待io的时间（IO等待高时，可能是磁盘性能问题） 
	hi REAL, --cpu处理硬中断的数量 
	si REAL, --cpu处理软中断的数量
	st REAL --steal time 
}
```

#### 6.2.3.21 DF_MemInfo 

【定义】

定义 V2X 设备内存信息。

```ASN.1
【ASN.1 代码】 
MemInfo ::= SEQUENCE { 
	total REAL, --总物理内存，单位：M 
	free REAL, --可用内存，单位：M 
	used REAL --已用内存，单位：M 
}
```

#### 6.2.3.22 DF_NetInfo 

【定义】

定义 V2X 设备网络信息。

```ASN.1
【ASN.1 代码】 
NetInfo ::= SEQUENCE { 
	rxpckps REAL, --每秒钟接收的数据包 
	txpckps REAL, --每秒钟发送的数据包 
	rxbytps REAL, --每秒钟接收的字节数 
	txbytps REAL --每秒钟发送的字节数 
}
```

#### 6.2.3.23 DF_DiskInfo 

【定义】

定义 V2X 设备磁盘信息。

```ASN.1
【ASN.1 代码】 
DiskInfo ::= SEQUENCE { 
	total REAL, --磁盘总量(M) 
	used REAL, --已用磁盘（m） 
	free REAL, --可用磁盘（m） 
	tps REAL, --每秒 io 请求数 
	rkBps REAL, --每秒写入磁盘数据量（k） 
	wkBps REAL --每秒读取磁盘数据量（k） 
}
```

#### 6.2.3.24 DF_RemoteLoginInputs

【定义】

定义 V2X 设备远程登陆功能的输入参数。

```ASN.1
【ASN.1 代码】 
RemoteLoginInputs ::= SEQUENCE { 
	username IA5String, 
	password IA5String, 
	access RemoteAccessMethod 
}
```

#### 6.2.3.25 DF_RemoteLogOutputs 

【定义】

定义 V2X 设备远程登陆功能的输出参数。

```ASN.1
【ASN.1 代码】 
RemoteLogOutputs ::= SEQUENCE { 
	success BOOLEAN, 
	error UTF8String OPTIONAL, --失败原因 
	url IA5String --远程访问链接 
}
```

#### 6.2.3.26 DF_RemoteRestartInputs 

【定义】

定义 V2X 设备远程重启功能的输入参数。

```ASN.1
【ASN.1 代码】 
RemoteRestartInputs ::= SEQUENCE { 
	username IA5String, 
	password IA5String, 
	time INTEGER OPTIONAL --设定在几秒钟之后进行重启，单位：秒。 
}
```

#### 6.2.3.27 DF_RemoteRestartOutputs 

【定义】

定义 V2X 设备远程重启功能的输出参数。

```ASN.1
【ASN.1 代码】 
RemoteRestartOutputs ::= SEQUENCE { 
	success BOOLEAN, 
	error UTF8String OPTIONAL --失败原因 
}
```

#### 6.2.3.28 DF_RemoteConfigInputs

【定义】

定义 V2X 设备远程配置功能的输入参数。

```ASN.1
【ASN.1 代码】 
RemoteConfigInputs ::= SEQUENCE { 
	version IA5String, --协议版本号 
	scope ConfigScope, --配置范围 
	type ConfigType, --配置类型,目前支持文件类型，取值：file 
	size IA5String, --配置大小，按字节计算。 
	url IA5String, --存储配置文件的对象存储（OSS）地址 
	sign IA5String, --签名 
	signMethod SignMethod, --签名方法 
	md5 IA5String OPTIONAL, --当签名方法为MD5时，除了会给sign赋值外还会给md5赋值 
	...
}
```

#### 6.2.3.29 DF_RemoteConfigOutputs 

【定义】

定义 V2X 设备远程配置功能的输出参数。

```ASN.1
【ASN.1 代码】 
RemoteConfigOutputs ::= SEQUENCE { 
	success BOOLEAN, 
	error UTF8String OPTIONAL --失败原因 
}
```

#### 6.2.3.30 DF_PC5CommStatisticsInputs 

【定义】

定义 V2X 设备 PC5 接口数据统计功能的输入参数。

```ASN.1
【ASN.1 代码】 
PC5CommStatisticsInputs ::= SEQUENCE { 
	type PC5CommType, --统计类型：接收、发送、接收和发送 
	switch Switch, --统计功能开关 
	duration INTEGER --数据统计持续时长，过期自动停止，0表示持续统计，单位：分钟 
}
```

#### 6.2.3.31 DF_PC5CommStatisticsOutputs 

【定义】

定义 V2X 设备 PC5 接口数据统计功能的输出参数。

```ASN.1
【ASN.1 代码】 
PC5CommStatisticsOutputs ::= SEQUENCE { 
	success BOOLEAN, 
	error UTF8String OPTIONAL --失败原因 
}
```

#### 6.2.3.32 DF_LogReportInputs 

【定义】

定义 V2X 设备日志上报功能的输入参数。

```ASN.1
【ASN.1 代码】
LogReportInputs ::= SEQUENCE { 
	url IA5String, --日志上传地址 
	username IA5String, --日志服务器的登录用户名 
	password IA5String, --日志服务器的的登录密码 
	commProtocol CommProtocol, --数据传输协议类型 
	version IA5String, --协议版本 
	... 
}
```

#### 6.2.3.33 DF_LogReportOutputs 

【定义】

定义 V2X 设备日志上报功能的输出参数。

```ASN.1
【ASN.1 代码】 LogReportOutputs ::= SEQUENCE { 
	success BOOLEAN, 
	error UTF8String OPTIONAL --失败原因 
}
```

#### 6.2.3.34 DF_FotaInputs 

【定义】

定义 V2X 设备远程升级功能的输入参数。

```ASN.1
【ASN.1 代码】 
FotaInputs ::= SEQUENCE { 
	version IA5String, --设备升级包的版本信息 
	size INTEGER, --升级包大小，单位：字节 
	url IA5String, --升级包在对象存储（OSS）上的存储地址 
	sign IA5String, --升级包签名 
	signMethod SignMethod, --签名方法 
	md5 IA5String OPTIONAL,
	--当签名方法为MD5时，除了会给sign赋值外还会给md5赋值 
	module IA5String --升级包所属的模块名 
}
```

#### 6.2.3.35 DF_FotaOutputs 

【定义】

定义 V2X 设备远程升级功能的输出参数。

```ASN.1
【ASN.1 代码】 FotaOutputs ::= SEQUENCE { 
	success BOOLEAN, 
	error UTF8String OPTIONAL --失败原因 
}
```

#### 6.2.3.36 DF_Position3D 

【定义】

定义三维的坐标位置，经纬度和高程。

```ASN.1
【ASN.1 代码】 Position3D ::= SEQUENCE { 
	lat INTEGER (-900000000..900000001), 
	-- Units of 1/10 micro degree 
	-- Providing a range of plus-minus 90 degrees 
	long INTEGER (-1799999999..1800000001), 
	-- Units of 1/10 micro degree 
	-- Providing a range of plus-minus 180 degrees 
	elevation INTEGER (-4096..61439) OPTIONAL 
	-- Units of 10 cm steps above or below the reference ellipsoid 
	-- Providing a range of -409.5 to + 6143.9 meters 
	-- The value -4096 shall be used when Unknown is to be sent 
}
```

### 6.2.4 数据元素（Data Element） 

数据元素是消息体或数据单元的组成部分。它由基本数据类型定义产生，具有实际物理意义。

#### 6.2.4.1 DE_DeviceType 

【定义】

定义 V2X 设备类型。

```ASN.1
【ASN.1 代码】 
DeviceType ::= ENUMERATED {obu, rsu, psu}
```

#### 6.2.4.2 DE_StorageCapacity 

【定义】

定义 V2X 设备存储容量状态。

```ASN.1
【ASN.1 代码】 
StorageCapacity ::= BIT STRING {isHealthy (0)} (SIZE (8))
```

#### 6.2.4.3 DE_AppSoftware 

【定义】

定义 V2X 设备应用软件状态。

```ASN.1
【ASN.1 代码】 
AppSoftware ::= BIT STRING { 
	isSecurity (0), 
	-- 该位置 1 时表示：安全通信 
	isHealthy (1), 
	-- 该位置 0 时表示：某些应用已停止运行 
	fcw (2), 
	icw (3), 
	lta (4), 
	bsw (5), 
	lcw (6), 
	dnpw (7), 
	ebw (8), 
	avw (9), 
	clw (10), 
	hlw (11), 
	slw (12), 
	rlvw (13), 
	vrucw (14), 
	glosa (15), 
	ivs (16), 
	tjw (17), 
	evw (18), 
	vnfp (19), 
	sds (20), 
	clc (21), 
	cvm (22), 
	cip (23),
	dds (24), 
	dlm (25), 
	chpvp (26),
    gspa (27), 
    pdc (28), 
    vrusp (29), 
    cpm (30), 
    rts (31) 
} (SIZE (32))
```

#### 6.2.4.4 DE_TimeServiceStatus 

【定义】

定义 V2X 设备时间服务状态。

```ASN.1
【ASN.1 代码】 
TimeServiceStatus ::= BIT STRING { 
	unavailable (0), -- Not Equipped or unavailable 
	isHealthy (1) 
} (SIZE (8))
```

#### 6.2.4.5 DE_CellStatus 

【定义】

定义 V2X 设备蜂窝网模块状态。 

```ASN.1
【ASN.1 代码】 
CellStatus ::= BIT STRING { 
	unavailable (0), -- Not Equipped or unavailable 
	isHealthy (1) 
} (SIZE (8))
```

#### 6.2.4.6 DE_EthStatus 

【定义】

定义 V2X 设备以太网模块状态。

```ASN.1
【ASN.1 代码】 
EthStatus ::= BIT STRING { 
	unavailable (0), -- Not Equipped or unavailable 
	isHealthy (1) 
} (SIZE (8))
```

#### 6.2.4.7 DE_V2XStatus 

【定义】

定义 V2X 设备 V2X 模块（PC5 接口）状态。

```ASN.1
【ASN.1 代码】 
V2XStatus ::= BIT STRING { 
	unavailable (0), -- Not Equipped or unavailable 
	isHealthy (1) 
} (SIZE (8))
```

#### 6.2.4.8 DE_GNSSstatus 

【定义】

定义 V2X 设备 GNSS 模块状态。

```ASN.1
【ASN.1 代码】 GNSSstatus ::= BIT STRING { 
	unavailable (0), 
	-- Not Equipped or unavailable 
	isHealthy (1), 
	isMonitored (2), 
	baseStationType (3), 
	-- Set to zero if a moving base station, 
	-- or if a rover device (an OBU), 
	-- set to one if it is a fixed base station 
	aPDOPofUnder5 (4), 
	-- A dilution of precision greater than 5 
	inViewOfUnder5 (5), 
	-- Less than 5 satellites in view 
	localCorrectionsPresent (6), 
	-- pseudo range corrections used 
	networkCorrectionsPresent (7) 
	-- RTK type corrections used 
} (SIZE (8))
```

#### 6.2.4.9 DE_WifiStatus 

【定义】

定义 V2X 设备 Wifi 模块状态。

```ASN.1
【ASN.1 代码】 
WifiStatus ::= BIT STRING { 
	unavailable (0), -- Not Equipped or unavailable 
	isHealthy (1) 
} (SIZE (8))
```

#### 6.2.4.10 DE_HSMStatus 

【定义】

定义 V2X 设备硬件安全模块状态。

```ASN.1
【ASN.1 代码】 
HSMStatus ::= BIT STRING { 
	unavailable (0), -- Not Equipped or unavailable 
	isHealthy (1) 
} (SIZE (8))
```

#### 6.2.4.11 DE_CommProtocol 

【定义】

定义通信协议类型。

```ASN.1
【ASN.1 代码】 
CommProtocol ::= ENUMERATED {http, https, ftp, sftp, mqtt, mqtts, other}
```

#### 6.2.4.12 DE_SignMethod 

【定义】

定义签名方式类型。

```ASN.1
【ASN.1 代码】 
SignMethod ::= ENUMERATED {sha256, md5, ...}
```

#### 6.2.4.13 DE_ConfigScope 

【定义】

定义配置生效范围。

```ASN.1
【ASN.1 代码】 
ConfigScope ::= ENUMERATED {product, device, ...}
```

#### 6.2.4.14 DE_ConfigType 

【定义】

定义配置生效对象类型。

```ASN.1
【ASN.1 代码】 
ConfigType ::= ENUMERATED {file, ...}
```

#### 6.2.4.15 DE_Switch 

【定义】

定义开关指令。 

```ASN.1
【ASN.1 代码】 
Switch ::= ENUMERATED {open, off}
```

#### 6.2.4.16 DE_RemoteAccessMethod 

【定义】

定义远程登陆的接入方式类型。

```ASN.1
【ASN.1 代码】 
RemoteAccessMethod ::= ENUMERATED { 
	web-session, ssh-session, web-session-read-only, ssh-session-read-only 
}
```

#### 6.2.4.17 DE_PC5CommType 

【定义】

定义 V2X 设备 PC5 接口通信方向。

```ASN.1
【ASN.1 代码】 PC5CommType ::= ENUMERATED {rx, tx, all}
```

