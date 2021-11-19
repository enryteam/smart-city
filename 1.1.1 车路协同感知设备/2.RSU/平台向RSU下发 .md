

## 一、Message Frame消息帧

- 一个消息帧中可接受的消息类型包括了：BSM，MAP，RSM，SPAT，RSI。

```json
【定义】
消息帧是应用层数据包收发的基本单位。由不同类别的消息体组成。 
【ASN.1 代码】 
-- Main message frame 
MessageFrame ::= CHOICE { 
bsmFrame BasicSafetyMessage, 	//基本安全消息
mapFrame MapData				//地理地图数据
rsmFrame RoadsideSafetyMessage, //路侧安全消息
spatFrame SPAT,					//信号灯消息
rsiFrame RoadSidelnformation,	//路侧信息
}
```

### 1.1 BSM-bsmFrame Basic Safety Message基本安全消息

```json
【定义】
车辆基本安全消息。是使用最广泛的一个应用层消息，用来在车辆之间交换安全状态数据。车辆通过该消息的广播，将自身的实时状态告知周围车辆，以此支持一系列协同安全等应用。
【ASN.1 代码】
BasicSafetyMessage ::= SEQUENCE {
msgCnt MsgCount,	//计数器，用来判断数据的连续性
id OCTET STRING (SIZE(8))		//原意：应该存储车辆唯一编码号，如车架号等，目前存储车牌号
-- vehicle ID
plateNo OCTET STRING (SIZE(4..16)) OPTIONAL, 	//车牌号
-- Reserved for Electronic Vehicle Identification //用于电子车辆识别
secMark DSecond, 		//TODO：定义毫米级时刻（具体含义仍需确认）
pos Position3D,			//三维坐标点：经度、纬度、海拔高度
accuracy PositionConfidenceSet, 	//应该用来确认车辆的精确位置
transmission TransmissionState, 	//车辆档位：Neutral：空档；Park：停止档；ForwardGears：前进档；   ReverseGears：倒档
speed Speed, 		//车速，单位厘米每小时
heading Heading,	//航向角：即为车头方向与正北方向的顺时针夹角。分辨率为 0.0125°，通过GPS得到。
angle SteeringWheelAngle OPTIONAL, 	//角度
motionCfd MotionConfidenceSet OPTIONAL,	//移动方向
accelSet AccelerationSet4Way, 	//车辆四轴加速度
brakes BrakeSystemStatus, 		//刹车状况，刹车踏板踩下情况
size VehicleSize,		//车辆尺寸大小（自己手动配置，希迪说我们有权限改这个的配置文件）
vehicleClass VehicleClassification,		//车辆分类
--VehicleClassification includes Basic VehicleClass and other extendible type	//车辆分类和其他可拓展分类类型 
safetyExt VehicleSafetyExtensions OPTIONAL,	//车辆安全辅助信息集合，如ABS，紧急制动，转向灯等
...
}
```

### 1.2 MAP-mapFrame MapData地图数据

```json
【定义】
地图消息。由路侧单元广播，向车辆传递局部区域的地图信息。包括局部区域的路口信息、路段信息、车道信息，道路之间的连接关系等。单个地图消息可以包含多个路口或区域的地图数据。路口处的信号灯信息则在SPAT消息中详细定义。
【ASN.1 代码】
MapData::= SEQUENCE { 
msgCnt MsgCount,	//计数器，用来判断数据的连续性
timeStamp MinuteOfTheYear OPTIONAL,		//时间戳
 nodes NodeList,		//地图节点
--intersections or road endpoints	//十字路口或道路终点
...
}
```

### 1.3 RSM-rsmFrame RoadsideSafetyMessage路侧安全消息

```json
【定义】 
路侧安全消息。路侧单元通过路侧本身拥有的相应检测手段，得到其周边交通参与者的实时状态信息（这里交通参与者包括路侧单元本身、周围车辆、非机动车、行人等），并将这些信息整理成本消息体所定义的格式，作为这些交通参与者的基本安全状态信息（类似于 Msg_BSM），广播给周边车辆，支持这些车辆的相关应用。 
Msg_RSM 消息的存在，使得车辆对于周围环境的感知不仅仅依赖于 Msg_BSM 消息。路侧单元基于路侧传感器，帮助车辆对其周围的环境进行了探测，并将实时信息通过 Msg_RSM 消息传递给车辆。 
【ASN.1 代码】 
RoadsideSafetyMessage ::= SEQUENCE { 
msgCnt MsgCount, 	//计数器，判断数据连续性
id OCTET STRING (SIZE(8)), 		//RSU 设备编号
-- RSU ID 
refPos Position3D, 			//三维坐标信息，经度、纬度、海拔高度
-- Reference position of this RSM message 	//RSM消息的参考位置
participants ParticipantList, 	//交通参与者列表，应用于RSM 消息中 ，表示所有或部分RSU当前探测到的交通参与者信息
-- All or part of the participants 
-- detected by RSU 
... 
}
```

### 1.4 RSI-rsiFrame RoadSidelnformation路侧信息

```json
【定义】
由路侧单元向周围车载单元发布的交通事件消息以及交通标志标牌信息。其中，交通标志标牌信息参考GB5768，包含其中所有标志标牌内容。针对一些动态的、临时的交通事件，例如"前方事故"、"前方路面结冰"等，还可以用文本消息的方式向车载单元进行发布。车载单元在判定消息的生效区域时，根据自身的定位与运行方向，以及消息本身提供的区域范围，来进行判定，而后向驾驶员推送。消息体中，参考点位置表示本信息产生的位置点（标志标牌的放置位置或交通事件的发生位置），消息中其余的位置偏移量均基于该参考点测算。用有序的位置点列，来表示该消息生效的车辆行进轨迹区段;用半径来表示区段的宽度以覆盖路段的宽度。RSI消息所传递的是与道路相关的一些预警或提示信息，不用作车辆的求救或其他安全应用。
【ASN.1 代码】
RoadSidelnformation :: = SEQUENCE {
msgCnt MsgCount,		// 计数器，判断数据连续性， 0~127
timeStamp MinuteOfTheYear OPTIONAL, 		//时间戳
id OCTET STRING (SIZE(8)), 	//8位字节
-- RSU ID
rsild INTEGER (0.255),		//RSI消息ID
-- local ID of this rsi information set by RSU
alertType AlertType,		//交通标志
--Text message warning or Traffic sign type according to China GB5768 description IA5String (SIZE(1.256))OPTIONAL, 	//短信警告或交通标志类型根据中国GB5768描述IA5String
-- Text message if alertType = 0
-- Additional description to the traffic sign if alertType>0
-- e.g. describe the subtype of the traffic sign 
priority Priority OPTIONAL,	////表示消息优先级。数值长度占 8 位，其中低五位为 0，为无效位，高三位为有效数据位。数值有效范围是 B00000000 到 B11100000，分别表示 8 档由低到高的优先级
-- the urgency of this message, a relative 
-- degree of merit compared with other 
-- similar messages for this type (not other 
-- messages being sent by the device), nor a 
-- priority of display urgency 
refPos Position3D,	//--交通警报位置（交通标志或事件)      三维坐标位置
--Position of traffic alert (traffic sign or incident)
alertPath PathPointList,	//圆形范围的半径大小
-- Warning is active if vehicle is within this path 
-- Points are listed from upstream to downstream 
-- along the vehicle drive direction. 
-- One path includes at least two points. 
alertRadius Radius,	//告警路径的宽度 半径（路的一半宽度）
--The biggest distance away from the alert path 
-- within which the warning is active.
...
}
```

### 1.5 SPAT-spatFrame信号灯消息

```json
【定义】
信号灯消息。包含一个或多个路口信号灯的当前状态信息。结合MAP消息，为车辆提供实时的前方信号灯相位信息。
【ASN.1 代码】 
SPAT ::= SEQUENCE { 
msgCnt MsgCount,	// 计数器，判断数据连续性
timeStamp MinuteOfTheYear OPTIONAL,	//本条消息时间戳
name DescriptiveName OPTIONAL, 		//   --用于优先策略，存了当前车辆的优先通行策略，例如策略编号，策略时间，车辆编号。
-- human readable name for this collection 
-- to be used only in debug mode	//仅在调试模式下使用
intersections IntersectionStateList, 	//交叉路口
--sets of SPAT data(one per intersection)	//吐口数据集(每个交集一个)
...
}
```