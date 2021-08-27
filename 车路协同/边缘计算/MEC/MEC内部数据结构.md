# MEC内部数据结构

## TrafficEvent

类型名：TrafficEvent

| 属性名      | 类型         | 属性         | 备注       |
| :---------- | :----------- | :----------- | :--------- |
| eventId     | string       | 事件ID       | -          |
| eventType   | int          | 事件类型     | -          |
| source      | string       | 来源         | -          |
| eventPos    | Position3D   | 事件位置     | -          |
| eventRadius | int          | 事件范围     | 单位：0.1m |
| timeStart   | long         | 事件开始时间 | -          |
| timeEnd     | long         | 事件结束时间 | -          |
| priority    | int          | 优先级       | -          |
| alertPath   | [Position3D] | 预警路径     | 列表       |
| referLink   | [int]        | 相关车道     | 列表       |

类型名：Position3D

| 属性名 | 类型 | 属性 | 备注                                                         |
| ------ | ---- | ---- | ------------------------------------------------------------ |
| lat    | int  | 纬度 | 纬度，LSB=0.1微度，提供一个加减范围                          |
| lon    | int  | 经度 | 纬度，LSB=0.1微度，提供一个加减范围                          |
| ele    | int  | 高度 | 海拔高度，单位时参考椭圆上下方10cm， 范围-409.5~+6143.9m 当未知数据出现时，赋值-4096 |

## TrafficSign

类型名：TrafficSign

| 属性名      | 类型         | 属性         | 备注     |
| ----------- | ------------ | ------------ | -------- |
| signId      | string       | 标志标线id   | -        |
| signType    | int          | 标志标线类型 | -        |
| signPos     | Pos3         | 标志标线位置 | -        |
| description | string       | 描述         | -        |
| timeStart   | long         | 开始时间     | -        |
| timeEnd     | long         | 结束时间     | -        |
| priority    | int          | 优先级       | -        |
| referPath   | [Position3D] | 相关路径     | -        |
| pathRadius  | int          | 路径半径     | 单位0.1m |
| referLink   | [int]        | 相关车道     | -        |

## RoadSideInformation

类型名：RoadSideInformation

| 属性名      | 类型                | 属性       | 备注                                                         |
| ----------- | ------------------- | ---------- | ------------------------------------------------------------ |
| timeStamp   | int                 | 时间戳     | 一年中的分钟，无效时输入527040                               |
| id          | string              | id         | RSU ID（大小（8））                                          |
| rsiId       | int                 | rsi 编号   | 通过RSU建立rsi 信息的本地id（0..255）                        |
| alertType   | int                 | 警告类型   | 参考GB 5768.2或 GBT 29100-2012，事故预警或者交通标志类型     |
| description | string              | 描述       | IA5字符串（大小（1..256）），alterType=0时消息警告，alterType>0时交通标志等警告 |
| priority    | string              | 优先级     | 优先级。与此类型的相似信息比较后的相对程度（不是这个装置发送的其他信息），也不是紧急程度的优先级。低五位保留置0，B00000000到B11100000代表最低到最高级别。 |
| refPos      | Position3D          | 参考点位置 | 交通警告消息的位置（交通标志或者事件）                       |
| alertPath   | [PositionOffsetLLV] | 预警路径   | Msg_RSI信息路径点列表，如果车辆行驶在该路径，警告激活，沿车辆行驶方向由近到远列出点，一条路径至少包含两个点。 |
| alertRaduis | int                 | 预警半径   | 路侧预警消息的半径，(0..1024),单位时0.1m                     |

类型名： PositionOffsetLLV

| 属性名         | 类型                   | 属性           | 备注                                                         |
| -------------- | ---------------------- | -------------- | ------------------------------------------------------------ |
| offsetLLChoice | PositionOffsetLLChoice | 相对经纬度类型 | positionLL1=0, positionLL2=1, postitionLL3=2, psotitionLL4=3, positionLL5=4, positionLL6=5, positionLatLon=6, |
| offsetLL       | PositionOffsetLL       | 相对经纬度     | 相对lon/lat                                                  |
| offsetVChoice  | VerticalOffsetChoice   | 相对高度类型   | offset1=0, offset2=1, offset3=2,  offset4=3, offset5=4, elevation=6 |
| offsetV        | VerticalOffset         | 相对高度       | 相对高度                                                     |

类型名：VerticalOffset

以下变量均低于或高于参考椭圆球10cm

| 属性名    | 类型 | 属性      | 备注                                           |
| --------- | ---- | --------- | ---------------------------------------------- |
| offset1   | int  | 相对高度1 | VertOffsetB07，范围是+-6.3m                    |
| offset2   | int  | 相对高度2 | VertOffsetB08，LSB，单位10cm，范围+-12.7m      |
| offset3   | int  | 相对高度3 | VertOffsetB09，LSB,   单位10cm，范围+-25.5m    |
| offset4   | int  | 相对高度4 | VertOffsetB10,   LSB,  单位10cm，范围+-51.m    |
| offset5   | int  | 相对高度5 | VertOffsetB11,   LSB,  单位10cm，范围+-102.3.m |
| offset6   | int  | 相对高度6 | VertOffsetB12,   LSB,  单位10cm，范围+-204.7.m |
| elevation | int  | 高度      | Elevation，LSB, 单位10cm，范围-409.5~+6143.9m  |

类型名：PositionOffsetLL

当使用相对位置时，相对经纬度包含了跨越赤道的情况

| 属性名         | 类型            | 属性        | 备注 |
| -------------- | --------------- | ----------- | ---- |
| positionLL1    | PositionLL24B   | 相对经纬度1 | -    |
| positionLL2    | PositionLL28B   | 相对经纬度2 | -    |
| positionLL3    | PositionLL32B   | 相对经纬度3 | -    |
| positionLL4    | PositionLL36B   | 相对经纬度4 | -    |
| positionLL5    | PositionLL44B   | 相对经纬度5 | -    |
| positionLL6    | PositionLL48B   | 相对经纬度6 | -    |
| positionLatLon | PositionLLmD46b | 经纬度      | -    |

类型名：PositionLLmD64b
一个Lat/Lon完整32b的范围，LSB单位为0.1微度

| 属性名 | 类型 | 属性 | 备注 |
| ------ | ---- | ---- | ---- |
| lon    | int  | 经度 | -    |
| lat    | int  | 纬度 | -    |

类型名：PositionLL48B
范围+-0.8388607度，赤道范围+-92.754681千米，LSB单位为0.1微度

| 属性名 | 类型 | 属性     | 备注 |
| ------ | ---- | -------- | ---- |
| lon    | int  | 相对经度 | -    |
| lat    | int  | 相对纬度 | -    |

类型名：PositionLL44B
范围+-0.2097151度，赤道范围+-23.189096千米，LSB单位为0.1微度

| 属性名 | 类型 | 属性     | 备注 |
| ------ | ---- | -------- | ---- |
| lon    | int  | 相对经度 | -    |
| lat    | int  | 相对纬度 | -    |

类型名：PositionLL36B
范围+-0.0131071度，赤道范围+-01.449308千米，LSB单位为0.1微度

| 属性名 | 类型 | 属性     | 备注 |
| ------ | ---- | -------- | ---- |
| lon    | int  | 相对经度 | -    |
| lat    | int  | 相对纬度 | -    |

类型名：PositionLL32B
范围+-0.0032767度，赤道范围+-362.31873米，LSB单位为0.1微度

| 属性名 | 类型 | 属性     | 备注 |
| ------ | ---- | -------- | ---- |
| lon    | int  | 相对经度 | -    |
| lat    | int  | 相对纬度 | -    |

类型名：PositionLL 28B
范围+-0.008191度，赤道范围+-90.571389米，LSB单位为0.1微度

| 属性名 | 类型 | 属性     | 备注 |
| ------ | ---- | -------- | ---- |
| lon    | int  | 相对经度 | -    |
| lat    | int  | 相对纬度 | -    |

类型名：PositionLL 24B
范围+-0.0002347度，赤道范围+-22.634566b米，LSB单位为0.1微度

| 属性名 | 类型 | 属性     | 备注 |
| ------ | ---- | -------- | ---- |
| lon    | int  | 相对经度 | -    |
| lat    | int  | 相对纬度 | -    |

## RoadsideSafetyMessage

类型名：VehicleSize

| 属性名 | 类型 | 属性 | 备注                                    |
| ------ | ---- | ---- | --------------------------------------- |
| width  | int  | 宽度 | 整数（0..1023）,LSB单位1cm，范围>10m    |
| length | int  | 长度 | (0..4095), LSB单位1cm，范围>40m         |
| height | int  | 高度 | 整数(0..127)，LSB单位为5cm，范围到6.35m |

类型名：AccelerationSet4Way

| 属性名 | 类型 | 属性 | 备注                                                         |
| ------ | ---- | ---- | ------------------------------------------------------------ |
| long   | int  | 纵向 | 沿车辆纵向坐标，整数（-2000，2001）,LSB单位时0.01m/s^2^,大于2000的值应使用2000 的值，小于-2000的值应使用值-2000，不可用的值应使用值2001。 |
| lat    | int  | 横向 | 沿车辆横向轴，整数（-2000..2001）,LSB单位为0.01m/s^2^，大于2000的值应使用2000 的值，-2000也会用到。 |
| vert   | int  | 垂直 | 沿车辆垂直坐标，,LSB单位时0.01m/s^2^,大于2000的值应使用2000 的值，-2000也能使用。 |
| yaw    | int  | 偏移 | 偏移率，整数（-32767…32767）,LSB单位每秒0.01度（标记）       |

类型名： PositionConfidenceSet

| 属性名    | 类型 | 属性       | 备注                     |
| --------- | ---- | ---------- | ------------------------ |
| pos       | int  | 水平置信度 | 水平两个方向的位置置信度 |
| elevation | int  | 高度置信度 | 高度置信度               |

类型名：MotionConfidenceSet

| 属性名     | 类型 | 属性       | 备注 |
| ---------- | ---- | ---------- | ---- |
| speedCfd   | int  | 速度置信度 | enum |
| headingCfd | int  | 航向置信度 | enum |
| steerCfd   | int  | 转向置信度 | enum |

类型名： ParticipantData

| 属性名       | 类型                  | 属性     | 备注                                                         |
| ------------ | --------------------- | -------- | ------------------------------------------------------------ |
| ptcType      | int                   | ptc类型  | -                                                            |
| ptcID        | int                   | ptcID    | RSU设置的临时ID，0为RSU本身，1…255代表RSU检测到参与者        |
| source       | int                   | 来源     | 未知（0），自己信息（1），v2x（2），v2x，视频（3），微波雷达（4），线圈（5） |
| id           | string                | id       | 八字节字符串（大小（8））可选                                |
| plateNo      | string                | 车牌     | 八字节字符串（大小（4..16））可选                            |
| secMark      | int                   | 秒       | D秒，以毫秒为单位                                            |
| pos          | PositionOffsetLLV     | 位置     | -                                                            |
| accuracy     | PositionConfidenceSet | 准确度   | -                                                            |
| transmission | int                   | 传输     | -                                                            |
| speed        | int                   | 速度     | 整数（0..8191),单位0.02m/s,8191意味着速度无效                |
| heading      | int                   | 航向     | LSB的0.0125度，范围0~359.9875度                              |
| angle        | int                   | 角度     | LSB单位为1.5度，范围为-189至+189度，+001=+1.5度，-126=-189度及以上，+126=+189度及以上，+127用于不可用 |
| motionCfd    | MotionConfidenceSet   | 动力Cfd  |                                                              |
| accelset     | AccelerationSet4Way   | 加速度   |                                                              |
| size         | VehicleSize           | 尺寸     | -                                                            |
| vehicleClass | int                   | 车辆分类 | 基础车辆分类，整数（0..255）                                 |

类型名：RoadsideSafetyMessage

| 属性名       | 类型              | 属性       | 备注                          |
| ------------ | ----------------- | ---------- | ----------------------------- |
| id           | string            | id         | RSU ID                        |
| refPos       | Position3D        | 参考点位置 | Msg_RSM信息参考位置           |
| participants | [ParticipantData] | 参与者     | RSU检测到所有或者部分参与设备 |

## SafetyMessage

类型名：PositionConfienceSet

| 属性名    | 类型                | 属性       | 备注                                                         |
| --------- | ------------------- | ---------- | ------------------------------------------------------------ |
| pos       | PositionConfidence  | 位置置信度 | 水平两个方向的位置置信度 unavailable=0,a500m=1,a200m=2,  a100m=3,a50m=4,a20m=5,a10m=6, a5m=7,a2m=8,a1m=9,a50cm=10, a20cm=11,a10cm=12,a5cm=13, |
| elevation | ElevationConfidence | 高度置信度 | 高度置信度 unavailable=0,elev50000=1, elev20000=2,elev10000=3, elev05000=4,elev02000=5, elev01000=6,elev00500=7, elev00200=8,elev00100=9, elev0050=10,elev0020=11, |

类型名：MotionConfidenceSet

| 属性名     | 类型                         | 属性    | 备注                                                         |
| ---------- | ---------------------------- | ------- | ------------------------------------------------------------ |
| speedCfd   | SpeedConfidence              | 速度Cfd | unavailable=0，prec100ms=1，prec10ms=2，prec5ms=3，prec1ms=4，prec0_1ms=5,prec0_05ms=6,prec0_01ms=7 |
| headingCfd | HeadingConfidence            | 航向Cfd | unavailable=0,prec10deg=1, prec05deg=2,prec01deg=3, prec0_1deg=4,prec0_05deg=5, prec0_01deg=6,prec0_0125deg=7 |
| steerCfd   | SteeringWheelAngleConfidence | 转向Cfd | unavailable=0,prec2deg=1, prec1deg=2,prec0_02deg=3           |

类型名：VehicleSafetyExtensions

| 属性名 | 类型              | 属性 | 备注                                                         |
| ------ | ----------------- | ---- | ------------------------------------------------------------ |
| events | VehicleEventFlags | 事件 | eventHazardLights=0， evenStoplineViolation=1， eventABSactivated=2，eventTractionControlLoss=3, eventStabilityControlactivated=4, eventHazardousMaterials=5， eventReserved1=6, eventHardBraking=7, eventLightsChanged=8, eventWipersChanged=9, eventFlatTire=10, eventDisabledVehicle=11, eventAirbagDeployment =12 |
| lights | ExteriorLights    | 灯光 | lowBeamHeadlightsOn=0, highBeamHeadlightsOn=1, leftTurnSignalOn=2, rightTurnSignalOn=3, hazardSignalOn=4, automaticLightControlOn=5, daytimeRunningLightsOn=6, fogLightOn=7, parkingLightsOn=8 |

类型名：BarkeSystemStatus

| 属性名      | 类型                   | 属性           | 备注                                                         |
| ----------- | ---------------------- | -------------- | ------------------------------------------------------------ |
| brakePadel  | BrakePedalStatus       | 刹车盘         | unavailable=0,   off=1,       on=2                           |
| wheelBrakes | BrakeAppliedStatus     | 车轮制动器     | unavailable=0,leftFront=1, rightRear=4，leftRear=2,rightFront=3, |
| traction    | TractionControlStatus  | 牵引           | unavailable=0,off=1,on=2, engaged=3                          |
| abs         | AntiLockBrakeStatus    | 防抱死制动系统 | unavailable=0,off=1, on=2,engaged=3                          |
| scs         | StabilityControlStatus | 稳定控制状态   | unavailable=0,off=1, on=2,engaged=3                          |
| brakeBoost  | BrakeBoostApplied      | 制动推动器     | unavailable=0,off=1, on=2,engaged=3                          |
| auxBrakes   | AuxiliaryBrakeStatus   | 辅助制动器     | unavailable=0,off=1, on=2,engaged=3                          |

类型名：ReferPosition
以雷达为原点的坐标系中的相对位置

| 属性名    | 类型 | 属性    | 备注                                   |
| --------- | ---- | ------- | -------------------------------------- |
| deviceId  | int  | 设备id  | 检测设备                               |
| positionX | int  | X轴坐标 | 单位0.01m，雷达法线方向为 x 轴         |
| positionY | int  | Y轴坐标 | 单位0.01m，垂直雷达法线的左方向为 y 轴 |

类型名：SafetyMessage

| 属性名          | 类型                    | 属性         | 备注                                                         |
| --------------- | ----------------------- | ------------ | ------------------------------------------------------------ |
| ptcType         | string                  | ptc类型      | 参与者类型                                                   |
| ptcId           | string                  | ptc id       | 参与者id                                                     |
| source          | string                  | 来源         | -                                                            |
| plateNo         | string                  | 凭证         | 车牌                                                         |
| secMark         | int                     | sec标志      | DSecond，单位是毫秒                                          |
| pos             | Position3D              | 位置         | -                                                            |
| referPos        | ReferPosition           | 相对位置     | -                                                            |
| laneId          | int                     | 所在车道     | -                                                            |
| accuracy        | PositionConfidenceSet   | 精确度       | -                                                            |
| transmission    | TransmissionState       | 传输         | -                                                            |
| speed           | int                     | 速度         | 整数（0，8191），单位0.02m/s，8191指代速度值无效             |
| heading         | int                     | 航向         | LSB0.0125度，范围0~359.9875度                                |
| angle           | int                     | 角度         | LSB单位1.5度，范围为-189至+189度，+001=+1.5度，-126=-189度及以上，+126=+189度及以上，+127用于不可用 |
| motionCfd       | MotionConfidenceSet     | Cfd运动      | -                                                            |
| acclset         | AccelerationSet4Way     | 加速度计     | -                                                            |
| brakes          | BrakeSystemStatus       | 制动状态     | -                                                            |
| size            | VehicleSize             | 尺寸         | -                                                            |
| vehicleClass    | int                     | 车辆分类     | 车辆分类包括基本类型和其他类型                               |
| safetyExt       | VehicleSafetyExtensions | 车辆安全拓展 | -                                                            |
| driverBehavior  | string                  | 驾驶行为     | 分心，违法…                                                  |
| laneChangingAim | int                     | 变道瞄准     | -                                                            |

## DensityLane

类型名：DensityLane

| 属性名         | 类型       | 属性           | 备注                                               |
| -------------- | ---------- | -------------- | -------------------------------------------------- |
| deviceId       | string     | 装置ID         | -                                                  |
| detectStartPos | Position3D | 检测开始时位置 | -                                                  |
| detectEndPos   | Position3D | 检测结束时位置 | -                                                  |
| timeStamp      | int        | 时间戳         | 一年中每一分钟，整数（0..527040）,无效时输入527040 |
| laneNo         | int        | 车道号         | -                                                  |
| density        | int        | 密度           | -                                                  |

## SpeedLaneArea

类型名：SpeedLaneArea

| 属性名         | 类型       | 属性           | 备注                                             |
| -------------- | ---------- | -------------- | ------------------------------------------------ |
| deviceID       | string     | 检测器id       | -                                                |
| detectStartPos | Position3D | 检测开始的位置 | -                                                |
| detectEndPos   | Position3D | 检测结束的位置 | -                                                |
| timeStamp      | int        | 时间戳         | 年每一分钟，整数（0.527040），527040被用作无效值 |
| laneNo         | int        | 车道号         | -                                                |
| speed          | int        | 速度           | 整数（0..8191），单位0.02m/s，8191意味着无效值   |

## SpeedLanePoint

类型名：SpeedLanePoint

| 属性名    | 类型       | 属性     | 备注                                            |
| --------- | ---------- | -------- | ----------------------------------------------- |
| deviceID  | string     | 装置ID   | -                                               |
| detectPos | Position3D | 检测位置 | -                                               |
| timeStamp | int        | 时间戳   | 年每一分钟，整数（0.527040） 527040被用作无效值 |
| cycle     | int        | 周期     | -                                               |
| laneNo    | int        | 车道数   | -                                               |
| speed     | int        | 速度     | 整数（0..8191），单位0.02m/s 8191意味着无效值   |

## VolumeLane

类型名：VolumeLane

| 属性名    | 类型       | 属性     | 备注 |
| --------- | ---------- | -------- | ---- |
| deviceID  | string     | 装置ID   | -    |
| detectPos | Position3D | 检测位置 | -    |
| timeStamp | long       | 采样时间 | -    |
| cycle     | int        | 周期     | -    |
| laneNo    | int        | 车道号   | -    |
| volume    | int        | 流量     | -    |

## Map

类型名：RegulatorySpeedLimit

| 属性名 | 类型           | 属性 | 备注                                                         |
| ------ | -------------- | ---- | ------------------------------------------------------------ |
| type   | SpeedLimitType | 类型 | unknown=0，maxSpeedInSchoolZone=1，maxSpeedInSchoolZoneWhenChildrenArePresent=2,maxSpeedInConstructionZone=3,  vehicleMinSpeed=4,vehicleMaxSpeed=5,vehicleNightMaxSpeed=6，truckMinSpeed=7, truckMaxSpeed=8,truckNightMaxSpeed=9,vehiclesWithTrailersMinSpeed=10, vehiclesWithTrailersMaxSpeed=11,vehiclesWithTrailersNightMaxSpeed=12 |
| speed  | int            | 速度 | 速度的单位是0.02米/秒。参见第11节的换算和转换，速度以m/s为单位 |

类型名：RoadPoint

| 属性名    | 类型              | 属性     | 备注               |
| --------- | ----------------- | -------- | ------------------ |
| posOffset | PositionOffsetLLV | 相对位置 | 参考位置的相对位置 |

类型名： NodeReferenceID

| 属性名 | 类型 | 属性 | 备注                                                         |
| ------ | ---- | ---- | ------------------------------------------------------------ |
| region | int  | 区域 | 0~65535随机整数，0仅作为测试需要，全球每一区域只赋值一个，优先派给区域DOT |
| id     | int  | id   | 0~65535之间随机整数，在上述区域中，讨论与区域节点的映射关系  |

类型名：Movement

| 属性名             | 类型            | 属性         | 备注                                                         |
| ------------------ | --------------- | ------------ | ------------------------------------------------------------ |
| remoteIntersection | NodeReferenceID | 远方十字路口 | 表示沿行驶方向，与该车道连接的十字路口                       |
| phaseId            | int             | 相位ID       | 该车道/机动的SPAT信息发送的匹配信号组。 除非连接车道没有信号组（无信号） |

类型名：ConnectingLane

| 属性名   | 类型 | 属性 | 备注                 |
| -------- | ---- | ---- | -------------------- |
| lane     | int  | 车道 | 列表里已连接的车道   |
| maneuver | int  | 方向 | 在车道和该车道停止线 |

类型名：Connection

| 属性名             | 类型            | 属性         | 备注                                                         |
| ------------------ | --------------- | ------------ | ------------------------------------------------------------ |
| remoteIntersection | NodeReferenceID | 远方十字路口 | 指示与车道相连的十字路口，这提供了建立车道网格的方法         |
| connectingLane     | ConnectingLane  | 连接车道     | 连接道路的索引，又或者时从当前车道移动到下一个t0列表上允许连接的车道上，我们使用 |
| phaseid            | int             | 相位id       | 该车道/机动的SPAT信息发送的匹配信号组。 除非连接车道没有信号组（无信号） |

类型名： LaneTypeAttributes

| 属性名    | 类型 | 属性     | 备注           |
| --------- | ---- | -------- | -------------- |
| vehicle   | int  | 车辆     | 包括摩托车     |
| crosswalk | int  | 斑马线   | 人行横道       |
| bikeLane  | int  | 自行车道 | 自行车车道     |
| sidewalk  | int  | 人行道   | 人行道         |
| median    | int  | 中间带   | 中间带或绿化带 |
| striping  | int  | 条带     | 道路标线       |
| tracked   | int  | 铁轨     | 火车和手推车   |
| parking   | int  | 停车     | 停车或者停车线 |

类型名： LaneAttributes

| 属性名    | 类型               | 属性     | 备注                                                         |
| --------- | ------------------ | -------- | ------------------------------------------------------------ |
| shareWith | LaneSharing        | 共享     | overlappingLaneDescriptionProvided=0，multipleLanesTreatedAsOneLane=1,otherNonMotorizedTrafficTypes=2, individualMotorizedVehicleTraffic=3,busVehicleTraffic=4,taxiVehicleTraffic=5, pedestriansTraffic=6,cyclistVehicleTraffic=7,trackedVehicleTraffic=8, pedestrianTraffic=9 |
| laneType  | LaneTypeAttributes | 车道类型 | -                                                            |

类型名：Lane

| 属性名         | 类型                   | 属性     | 备注                                                         |
| -------------- | ---------------------- | -------- | ------------------------------------------------------------ |
| laneID         | int                    | 车道iD   | 整数（0。。255），当车道ID不可用或未知时，应使用0。255保留供将来使用 |
| laneAttributes | LaneAttributes         | 车道属性 |                                                              |
| maneuvers      | int                    | 方向     |                                                              |
| connectsTo     | [Connection]           | 连接     | 列表                                                         |
| speedLimits    | [RegulatorySpeedLimit] | 限速     |                                                              |
| points         | [RoadPoint]            | 点       |                                                              |

类型名：Link

| 属性名         | 类型                   | 属性     | 备注                 |
| -------------- | ---------------------- | -------- | -------------------- |
| name           | string                 | 名称     | 路段名               |
| upstreamNodeId | NodeReferenceID        | 上游节点 | -                    |
| speedLimits    | [RegulatorySpeedLimit] | 限速     | 列表                 |
| laneWidth      | int                    | 路段宽度 | 0~32767整数，单位1cm |
| points         | [RoadPoint]            | 点       | 列表                 |
| movements      | [Movement]             | 方向     | 列表                 |
| lanes          | [Lane]                 | 车道     | 列表                 |

类型名：Node

 节点可以是交叉点，也可以是道路终点 

| 属性名  | 类型            | 属性     | 备注                                               |
| ------- | --------------- | -------- | -------------------------------------------------- |
| name    | string          | 名称     | 节点名称                                           |
| id      | NodeReferenceID | id       | 全球唯一值集合，由区域和节点id组成                 |
| refPos  | Position3D      | 参考位置 | 中心的三维位置节点。这个位置也是内部元素的参考位置 |
| inLinks | [Link]          | 路段     | 所有的路段都进入这个节点                           |

类型名：Map

| 属性名   | 类型   | 属性   | 备注                                             |
| -------- | ------ | ------ | ------------------------------------------------ |
| timeSamp | long   | 时间戳 | 年中每一分钟，0~527040中的整数，无效时填写527040 |
| nodes    | [Node] | 节点   | 列表                                             |

## SignalPhaseAndTiming

类型名：TimeChangeDetails

| 属性名         | 类型 | 属性           | 备注                                                         |
| -------------- | ---- | -------------- | ------------------------------------------------------------ |
| startTime      | int  | 开始时间       | 以UTC时间的1/10s为单位，当此阶段开始时，如果开始，此值为0    |
| minEndTime     | int  | 最小结束时间   | 预期最短结束时间，以UTC时间的1/10s为单位，如果已经启动，则该值是从现在开始最小剩余时间，如果未启动，则值表示该阶段最小长度 |
| maxEndTime     | int  | 最大结束时间   | 预期最短结束时间，以UTC时间的1/10s为单位，如果已经启动，则该值是从现在开始最大剩余时间，如果未启动，则值表示该阶段最大长度 |
| likelyEndTime  | int  | 可能结束时间   | 以UTC时间的1/10s为单位，基于其他数据的最佳预测值，如果已经开始，则值是从现在开始可能剩余的时间，如果未开始，则该值表示该阶段的可能长度 |
| timeConfidence | int  | 时间置信度     | 以UTC时间的1/10s为单位，表示可能结束时间的置信度             |
| nextStartTime  | int  | 下一次开始时间 | 以UTC时间的1/10s为单位，此状态下次可能发生时间的粗略估计，在上述结束时间之后，用于支持各种环保驱动电源管理需求。如果已经启动，建议传递此值。 |
| nextDuration   | int  | 下一个持续时间 | 以UTC时间的1/10s为单位，此状态下次可能结束时间的粗略估计，在上述结束时间之后，用于支持各种环保驱动电源管理需求。如果已经启动，建议传递此值。 |

类型名：PhaseState

| 属性名 | 类型              | 属性 | 备注                                                         |
| ------ | ----------------- | ---- | ------------------------------------------------------------ |
| light  | LightState        | 灯光 | 包括定向、保护、许可等11种基本状态 unavailable = 0,dark = 1，stopThenProceed = 2,stopAndRemain = 3, preMovement = 4,permissiveMovementAllowed = 5,protectedMovementAllowed = 6,  intersectionClearance = 7,cautionConflictingTraffic = 8 |
| timing | TimeChangeDetails | 时间 | 事件的UTC时间戳计时数据，包括阶段的开始时间和最小/最大结束时间，置信度和估计下次发生 |

类型名：Phase

| 属性名      | 类型         | 属性     | 备注                                                         |
| ----------- | ------------ | -------- | ------------------------------------------------------------ |
| id          | int          | id       | 组id用于映射到车道列表（及其描述），移动状态数据的使用 查看备注中有关用法详细信息的注释 |
| phaseStates | [PhaseState] | 阶段状态 | 列表，由一组变化数据组成，具有：a） 信号灯状态信息b）时间变化详细信息，以及c）建议速度（可选），未来的时间，允许传送多个信息。使用当前信号组来预测下一阶段和行驶时间。 |

类型名：IntersectionState

| 属性名         | 类型                     | 属性       | 备注                                                         |
| -------------- | ------------------------ | ---------- | ------------------------------------------------------------ |
| intersectionId | NodeReferenceID          | 十字路口id | 全球唯一值集（由区域ID和分配的交叉口id）提供唯一地图节点映射 |
| status         | IntersectionStatusObject | 状态       | 枚举，控制器的一般状态                                       |
| moy            | int                      | 分钟数     | 当前UTC年的分钟数，仅用于消息存档，使用值527040表示无效      |
| timeStamp      | int                      | 时间戳     | 以毫秒为单位，表示当前UTC分钟的毫秒点                        |
| phases         | [Phase]                  | 阶段       | 给出每个移动状态，并包含信号状态，映射到它所在车道以及它将结束的时间点，它可能包含移动状态和未来状态 |

类型名：SignalPhaseAndTiming

| 属性名        | 类型                | 属性   | 备注                                 |
| ------------- | ------------------- | ------ | ------------------------------------ |
| timeStamp     | long                | 时间戳 | 年中每一分钟，值527040将用于无效     |
| name          | string              | 名称   | 此集合的可读名称，仅在调试模式下使用 |
| intersections | [IntersectionState] | 交叉口 | SPAT数据集（每个交叉点一个）         |

## DedicatedLaneControl

类型名：ControlScheme

| 属性名     | 类型 | 属性         | 备注     |
| ---------- | ---- | ------------ | -------- |
| id         | int  | id           | 方案id   |
| vmsId      | int  | 可变信息版id | -        |
| laneId     | int  | 车道id       | -        |
| laneType   | int  | 车道类型     | 专用道   |
| laneStatus | bool | 车道状态     | 是否开启 |

类型名： DedicatedLaneControl

| 属性名    | 类型            | 属性     | 备注                                             |
| --------- | --------------- | -------- | ------------------------------------------------ |
| timeStamp | long            | 时间戳   | 年中每一分钟，0~527040中的整数，无效时填写527040 |
| schemes   | [ControlScheme] | 方案列表 | 列表                                             |

## RampMetering

类型名：RMScheme

| 属性名       | 类型 | 属性     | 备注   |
| ------------ | ---- | -------- | ------ |
| id           | int  | id       | 列表id |
| rampId       | int  | 斜坡id   | -      |
| signalHeadId | int  | 信号灯id | -      |
| cycle        | int  | 周期     | 单位s  |
| green        | int  | 红灯     | 单位s  |
| red          | int  | 绿灯     | 单位s  |

类型名：SignalPhase

| 属性名        | 类型 | 属性           | 备注     |
| ------------- | ---- | -------------- | -------- |
| id            | int  | id             | 信号灯id |
| phaseStatus   | int  | 阶段状态       | -        |
| nextGreenTime | int  | 下一个绿灯时间 | 单位s    |

类型名：RampMetering

| 属性名    | 类型          | 属性     | 备注                                             |
| --------- | ------------- | -------- | ------------------------------------------------ |
| timeStamp | int           | 时间戳   | 年中每一分钟，0~527040中的整数，无效时填写527040 |
| schemes   | [RMScheme]    | 方案列表 | -                                                |
| phases    | [SignalPhase] | 相位     | 列表                                             |

## VariableSpeedLimit

类型名：SpeedLimitScheme

| 属性名             | 类型 | 属性       | 备注       |
| ------------------ | ---- | ---------- | ---------- |
| speedLimitSchemeId | int  | 限速列表id | km/h       |
| laneId             | int  | 道路id     | -          |
| vmsId              | int  | vms id     | -          |
| speedLimit         | int  | 限速       | -          |
| speedLimitTime     | int  | 限速时间   | 速度、分钟 |

类型名：VariableSpeedLimit 

| 属性名    | 类型               | 属性   | 备注                             |
| --------- | ------------------ | ------ | -------------------------------- |
| timeStamp | int                | 时间戳 | 年中每一分钟，值527040将用于无效 |
| schemes   | [SpeedLimitScheme] | 方案   | 列表                             |