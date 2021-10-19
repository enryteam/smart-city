[TOC]

信号灯消息。包含了一个或多个路口信号灯的当前状态信息。结合MAP消息，为车辆提供实时的前方信号灯相位信息。
图43给出了SPAT消息的主体结构。其中实线框为必有项，虚线框为可选项。

![image-20210609095414996](https://gitee.com/AiShiYuShiJiePingXing/img/raw/master/img/image-20210609095414996.png)

# 一、SPAT信号灯消息   机器发送的值：ABCDEDF

```json
{
    "_id" : "5f9f94b9f31c6413d5ae3cf6",  //希迪自定义消息编号 ，无具体实际意义
    "msgCnt" : 42,  // 计数器，判断数据连续性， 0~127 
    "timeStamp" : 441444,  //本条消息时间戳
    "name" : "1234567890", //   --用于优先策略，存了当前车辆的优先通行策略，例如策略编号，策略时间，车辆编号。
    "intersections" : [  //交叉路口
        {
            "intersectionId" : {   //路口所在区域， 依据当前路口地图intersectionID  设置
                "region" : 0,   //区域编号
                "id" : 123    // 交叉路口编号
            },
            "status" : {  //路口信号机的工作状态指示。用于 SPAT 消息中
                "bytes" : "AAA", // status全部的值   ABCDEDF
                "unusedBits : 0,//没有使用的位数    ABC
                "recentChangeInMAPassignedLanesIDsUsed" : false,   //第十位10 最新地图消息更新状态
                "noValidMAPisAvailableAtThisTime" : false,  //地图不可用
                "noValidSPATisAvailableAtThisTime" : false, // -SPAT系统此时不工作
                "off" : false,// -控制器关闭   
                "failureMode" : false, //故障模式
                "failureFlash" : false,//故障动画显示
                "stopTimeIsActivated" : false, //所有的计数/计时都停止
                "recentMAPmessageUpdate" : false,  //地图内容改变
                "preemptIsActive" : false,
                "trafficDependentOperation" : false,
                "standbyOperation" : false,
                "signalPriorityIsActive" : false,
                "manualControlIsEnabled" : false,
                "fixedTimeOperation" : false,
                "bitSize" : 16
            },
            "moy" : 441444,  //当前UTC年的分钟数
            "timeStamp" : 14988,//
            "phases" : [ // 相位    南北 ，东西 ，左转，右转。
                { 
                    "id" : 3,  // 和道路编号一一对应
                    "phaseStates" : [ 
                        {
                            "light" : "permissive_Movement_Allowed",  //信号机相位状态   前行， 左转，右转
                            "timing" : {
                                "startTime" : 0,  //灯组灯色开始时间
                                "minEndTime" : null,
                                "maxEndTime" : null,
                                "likelyEndTime" : 240, //灯组灯色结束时间
                                "timeConfidence" : null,
                                "nextStartTime" : null,
                                "nextDuration" : null
                            }
                        }
                    ]
                }, 
                {
                    "id" : 1,
                    "phaseStates" : [ 
                        {
                            "light" : "stop_And_Remain",
                            "timing" : {
                                "startTime" : 0,
                                "minEndTime" : null,
                                "maxEndTime" : null,
                                "likelyEndTime" : 270,
                                "timeConfidence" : null,
                                "nextStartTime" : null,
                                "nextDuration" : null
                            }
                        }
                    ]
                }, 
                {
                    "id" : 5,
                    "phaseStates" : [ 
                        {
                            "light" : "stop_And_Remain",
                            "timing" : {
                                "startTime" : 0,
                                "minEndTime" : null,
                                "maxEndTime" : null,
                                "likelyEndTime" : 570,
                                "timeConfidence" : null,
                                "nextStartTime" : null,
                                "nextDuration" : null
                            }
                        }
                    ]
                }, 
                {
                    "id" : 8,
                    "phaseStates" : [ 
                        {
                            "light" : "stop_And_Remain",
                            "timing" : {
                                "startTime" : 0,
                                "minEndTime" : null,
                                "maxEndTime" : null,
                                "likelyEndTime" : 870,
                                "timeConfidence" : null,
                                "nextStartTime" : null,
                                "nextDuration" : null
                            }
                        }
                    ]
                }
            ]
        }
    ]
}
```



# 二、字段说明

## 2.1 intersections IntersectionStateList路口信号灯集合

```json
IntersectionState

【定义】
定义一个路口信号灯的属性和当前状态。包括路口ID、信号灯工作状态、时间戳以及信号灯的相位列表。
【ASN.1代码】
IntersectionState ::= SEQUENCE{
intersectionId NodeReferenceID,
-- A globally unique value set,consisting of a 
-- regionID and intersection ID assignment 
-- provides a unique mapping to the MAP Node 

status IntersectionStatusObject,
-- general status of the controller(s)

moy MinuteOfTheYear OPTIONAL, 
-- Minute of current UTC year 
-- used only with messages to be archived 

timeStamp DSecond OPTIONAL,
-- the mSec point in the current UTC minute that 
-- this message was constructed 

phases PhaseList 
-- Each Movement is given in turn 
-- and contains its signal phase state, 
-- mapping to the lanes it applies to, and 
-- point in time it will end, and it 
-- may contain both active and future states

}
IntersectionStateList

【定义】
定义一个路口信号灯集合。
【ASN.1 代码】
IntersectionStateList ::= SEQUENCE (SIZE(1..32)OF IntersectionState
```

###  Seq. of IntersectionState sequence of intersection state路口信号灯集合序列

#### intersectionID NodeReferenceID参考ID

```json
【定义】
定义参考ID。参考 ID由一个全局唯一的地区ID和一个地区内部唯一的节点D组成。
【ASN.1 代码】
NodeReferenceID ::= SEQUENCE {
region RoadRegulatorID OPTIONAL,
--a globally unique regional assignment value
-- typical assigned to a regional DOT authority
-- the value zero shall be used for testing needs 

id NodeID,
-- a unique mapping to the node 
-- in question within the above region of use

}
```

- region RoadRegulatorID OPTIONAL地图中各个划分区域的ID号

```json
【定义】
定义地图中各个划分区域的ID号。数值O仅用于测试。
【ASN.1 代码】
RoadRegulatorID ::= INTEGER (0..65535)
--The value zero shall be used for testing only
```

- id NodeID节点D

```json
【定义】
 定义节点D。路网最基本的构成即节点和连接节点的路段。节点可以是路口，也可以是一条路的端点。一个节点的ID在同一个区域内是唯一的。数值0～255 预留为测试使用。
【ASN.1代码】
 NodeID ::= INTEGER (0..65535)
--The values zero through 255 areallcated for testing purposes
-- Note that the value assigned to a node will be
-- unique within a given regional ID only
```

#### status IntersectionStatusObject信号灯工作状态

```json
【定义】
路口信号机的工作状态指示。用于SPAT消息中。
【ASN.1 代码】
IntersectionStatusObject ::= BIT STRING{
manualControllsEnabled (0),
--Timing reported is per programmed values, etc. but 
--person at cabinet can manually request that certain intervals --are terminated early (e.g. green). 

stopTimelsActivated (1),
-- And all counting/timing has stopped. 

failureFlash (2),
-- Above to be used for any detected hardware failures, 
--e.g.conflict monitor as well as for police flash 

preemptIsActive (3), 
signalPriorityIsActive (4), 
-- Additional states 

fixedTimeOperation (5),
--Schedule of signals is based on time only 
-- (i.e. the state can be calculated)

trafficDependentOperation (6),
--Operation is based on different levels of traffic parameters 
--(requests, duration of gaps or more complex
--parameters)

standbyOperation (7),
--Controller: partially switched off or partially amber flashing 

failureMode (8),
--Controller has a problem or failure in operation 

off9,
--Controller is switched off
--Related to MAP and SPAT bindings 

recentMAPmessageUpdate (10), 
-- Map revision with content changes

recentChangeIn MAP assigned LanesIDs Used (11), 
--Change in MAP'sassigned lanes used (lane changes)
--Changes in the active lane list description 

noValidMAPisAvailableAtThisTime (12), 
--MAP(and various lanes indexes) not available

noValidSPATisAvailableAtThisTime(13)
--SPAT system is not working at this time 
--Bits 14,15 reserved at this time and shall bezero 

} (SIZE(16))
```

#### timeStamp DSecond OPTIONAL某年某分

```json
【定义】
数值用来表示当前年份，已经过去的总分钟数（UTC时间）。分辨率为1分钟。该数值配合DSecond 数值，则可表示全年已过去的总毫秒数。
【ASN.1 代码】
MinuteOfTheYear ::= INTEGER (0..527040)
-- the value 527040 shall be used for invalid
```

#### timeStamp DSecond OPTIONAL时间戳

```json
【定义】
数值用来表示当前年份，已经过去的总分钟数（UTC 时间）。分辨率为1 分钟。该数值配合
DSecond 数值，则可表示全年已过去的总毫秒数。
【ASN.1 代码】
MinuteOfTheYear ::= INTEGER (0..527040)
-- the value 527040 shall be used for invalid
```

#### phases PhaseList相位列表

```json
Phase
【定义】
定义信号灯相位。一个相位包括一个相位 ID以及一个相位状态列表。
【ASN.1 代码】
Phase ::= SEQUENCE{
id PhaseID,
-- the group id is used to map to lists 
-- of lanes (and their descriptions)
-- which this MovementState data appies to
--see comments in the Remarks for usage details 

phaseStates PhaseStateList,
-- Consisting of sets of movement data with:
--a) SignalPhaseState 
--b) TimeChangeDetails, and 
--c) AdvisorySpeeds (optional)
--Note one or more of the movement events may be for
--a future time and that this allows conveying muliple 
--predictive phase and movement timing for various uses 
--for the current signal group

}

PhaseList
【定义】
定义一组信号灯包含的所有相位的列表。
【 ASN.1代码】
PhaseList ::= SEQUENCE (SIZE(1.16)OF Phase 
--List of phases in one taffic signal
```

##### Seq. of Phase sequence of phase相位序列

- id PhaseID相位编号

```json
【定义】
定义信号灯相位 ID。数值o 表示无效 ID。
【ASN.1代码】
PhaseID ::= INTEGER (0..255)
--The value 0 shall be used when the ID is not available or not known
```

- phaseStates PhaseStateList 相位状态

```json
PhaseState
【定义】
定义信号灯的一个相位状态。包含该状态对应的灯色，以及实时计时信息。
【ASN.1 代码】
PhaseState ::= SEQUENCE{
light LightState, 
-- Consisting of:
-- Phase state (the basic 11 states)
-- Directional, protected, or permissive state 

timing TimeChangeDetails OPTIONAL, 
--Timing Data in UTC time stamps for event 
-- includes start and min/max end times of phase 
-- confidence and estimated next occurrence 

..

 }

PhaseStateList
【定义】
定义一个信号灯的一个相位中的相位状态列表。列表中每一个相位状态物理上对应一种相位灯色，其属性包括了该状态的实时计时信息。
【ASN.1 代码】
PhaseStateList:= SEQUENCE (SIZE1.16)OF PhaseStae
```

## 2.2 msgCnt	MsgCount 消息计数

```json
【定义】 
发送方为自己发送的同类消息，依次进行编号。编号数值为 0 ～ 127。 
当发送方开始发起某一类数据时，它可以随机选择起始编号，随后依次递增。发送方也可以在 
连续发送相同的数据帧时，选择使用相同的 MsgCount 消息编号。编号到达 127 后，则下一个回到 0。 
【ASN.1 代码】 
MsgCount ::= INTEGER (0..127)
```

## 2.3 name DescriptiveName名称

```json
【定义】 
定义名称字符串类型。 
【ASN.1 代码】 
DescriptiveName ::= IA5String (SIZE(1..63))
```



## 2.4 timeStamp	MinuteOfTheYear OPTIONAL时间戳

```json
【定义】
数值用来表示当前年份，已经过去的总分钟数（UTC 时间）。分辨率为1 分钟。该数值配合
DSecond 数值，则可表示全年已过去的总毫秒数。
【ASN.1 代码】
MinuteOfTheYear ::= INTEGER (0..527040)
-- the value 527040 shall be used for invalid
```