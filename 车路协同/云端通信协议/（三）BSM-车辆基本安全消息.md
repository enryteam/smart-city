[TOC]

# 一、BSM-车辆基本安全消息  

时间是固定的 100毫秒一次

```json
BasicSafetyMessage ::= {
    msgCnt: 120      //计数器 ，判断数据连续性
    id: 30 30 31 34 39 30 36 33    //车辆编号
    plateNo: 56 36 36 36 30 33 31 30 35 38 30      // 车牌号 
    secMark: 33184    //定义毫米级时刻
    pos: Position3D ::= {  //三维坐标点
        lat: 374713976
        long: 1214557130
        elevation: 80
    }
    accuracy: PositionConfidenceSet ::= {    //定义位置的综合经度
        pos: 9 (a1m)
    }
    transmission: 0 (neutral)   //车辆档位  ●●     Neutral：空档；●●     Park：停止档；●●     ForwardGears：前进档；●●     ReverseGears：倒档。

    speed: 0    //速度   厘米每小时
    heading: 13940   //为车辆航向角，即为车头方向与正北方向的顺时针夹角。分辨率为 0.0125°。  通过GPS得到的
    accelSet: AccelerationSet4Way ::= {  // 车辆四轴加速度  
        long: 0 //  纵向   前为正
        lat: 0   //横向   左右  右为正
        vert: 0 //  垂直   下为正
        yaw: 0   //横摆角度速度   瞬时为正
    }
    brakes: BrakeSystemStatus ::= {  // 刹车状态
        brakePadel: 1 (off)  // 刹车踏板踩下情况
    }
    size: VehicleSize ::= {   //车辆尺寸大小    自己手动配置，希迪说我们有权限改这个的配置文件。
        width: 180
        length: 500
    }
    vehicleClass: VehicleClassification ::= {   //车辆类型    自己配置
        classification: 54
    }
    safetyExt: VehicleSafetyExtensions ::= {  //车辆安全辅助信息集合。
        events: 00 00 (3 bits unused)   // 什么意思   
        lights: 0C 00 (7 bits unused)     //  转向灯   

}
```

```java
事件  标准
typedef enum VehicleEventFlags {
 VehicleEventFlags_eventHazardLights = 0,
 VehicleEventFlags_eventStopLineViolation = 1,
 VehicleEventFlags_eventABSactivated = 2,
 VehicleEventFlags_eventTractionControlLoss = 3,
 VehicleEventFlags_eventStabilityControlactivated = 4,
 VehicleEventFlags_eventHazardousMaterials = 5,
 VehicleEventFlags_eventReserved1 = 6,
 VehicleEventFlags_eventHardBraking = 7,
 VehicleEventFlags_eventLightsChanged = 8,
 VehicleEventFlags_eventWipersChanged = 9,
 VehicleEventFlags_eventFlatTire = 10,
 VehicleEventFlags_eventDisabledVehicle = 11,
 VehicleEventFlags_eventAirBagDeployment = 12
} e_VehicleEventFlags;

车辆灯标准
typedef enum ExteriorLights {
 ExteriorLights_lowBeamHeadlightsOn = 0,
 ExteriorLights_highBeamHeadlightsOn = 1,
 ExteriorLights_leftTurnSignalOn = 2,
 ExteriorLights_rightTurnSignalOn = 3,
 ExteriorLights_hazardSignalOn = 4,
 ExteriorLights_automaticLightControlOn = 5,
 ExteriorLights_daytimeRunningLightsOn = 6,
 ExteriorLights_fogLightOn = 7,
 ExteriorLights_parkingLightsOn = 8
} e_ExteriorLights;
```

# 二、字段说明

## 2.1 id 编号

```json
rsu id
OCTET STRING (SIZE(8))
```

## 2.2 safetyExt VehicleSafetyExtensions OPTIONAL车辆安全扩展

```json
【定义】 
定义车辆安全辅助信息集合。用于BSM消息中，作为基础安全数据的补充。包括车辆特殊事件状态、车辆历史轨迹、路线预测、车身灯光状态等。各项辅助信息均为可选项。 
【ASN.1代码】
 VehicleSafetyExtensions:: SEQUENCE {
events VehicleEventFlags OPTIONAL, 

pathHistory PathHistory OPTIONAL,

pathPrediction PathPrediction OPTIONAL,

lights ExteriorLights OPTIONAL,
}
```

### 2.2.1 events VehicleEventFlags OPTIONAL车辆特殊标志/状态

```json
【定义】
 定义了一系列车辆的特殊状态。如果数据某一位被置 1，表示车辆处于该位对应的状态。当至少有一种对应状态被激活或者从激活状态恢复，该标志数值才应该被设置和交互。当车辆收到一个包含车辆特殊状态的数据后，需要根据数据的内容，来选择特定的操作。 车辆特殊状态定义如下∶
● Hazard Lights∶ 车辆警示灯亮起; 
● Stop Line Violation∶车辆在到达路口前预测自己可能会来不及刹车而越过停止线;
● ABS∶ ABS 系统被触发并超过 100 毫秒;
 ● Traction Control∶牵引力控制系统被触发并超过100 毫秒;
● Stability Control∶ 车身稳定控制系统被触发并超过 100毫秒;
● Hazardous Materials∶ 危险品运输车; 
●Hard Braking∶车辆急刹车，并且减速度大于0.4g，g为重力加速度典型值9.80665m/s³²;
● Lights Changed∶过去2 秒内，车灯状态改变; 
● Wipers Changed∶ 过去2秒内，车辆雨刷（前窗或后窗）状态改变;
● Flat tire∶车辆发现至少1 个轮胎爆胎了;
● Disabled Vehicle∶车辆故障，无法行驶;
● Air Bag Deployment∶ 至少1个安全气囊弹出。
【ASN.1代码】 
VehicleEventFlags ::=BIT STRING { 
eventHazardLights (0), 
eventStopLineViolation(1),--Intersection Violation 
eventABSactivated (2), 
eventTractionControlLoss (3),
eventStabilityControlactivated (4), 
eventHazardousMaterials (5), 
eventReserved1 (6), 
eventHardBraking (7),
eventLightsChanged (8), 
eventWipersChanged (9), 
eventFlatTire (10), 
eventDisabledVehicle(11),--The Disabled Vehicle DF may also be sent 
eventAirBagDeployment (12)
} (SIZE (13..)
```

### 2.2.2 pathHistory PathHistory OPTIONAL车辆历史轨迹

```json
【定义】
定义车辆历史轨迹。 利用一个参考轨迹点信息，以及一系列基于该参考信息的历史轨迹点，给出车辆一段完整的历史轨迹。车辆历史轨迹能够真实地反映其在当时的行驶状态，且从侧面反映当时其所在的道路和交通环境。 数据单元中的参考轨迹点信息在时间上比所有轨迹点都要靠后（时间较晚）。
【ASN.1代码】 PathHistory := SEQUENCE {
 initial Position FullPositionVector OPTIONAL, 
currGNSSstatus GNSSstatus OPTIONAL, 
crumbData PathHistoryPointList,
}
```

#### 1.  initialPosition FullPositionVector OPTIONAL完整的参考轨迹点信息

```json
【定义】
定义完整的参考轨迹点信息。用于车辆历史轨迹数据单元，作为一串轨迹点的参考点数据。
【ASN.1 代码】
FulPositionVector ::= SEQUENCE{
utcTime DDateTime OPTIONAL,-- time with mSec precision
pos Position3D,
heading Heading OPTIONAL,
transmission TransmissionState OPTIONAL,
speed Speed OPTIONAL,
posAccuracy PositionConfidenceSet OPTIONAL, 
timeConfidence TimeConfidence OPTIONAL,
posConfidence PositionConfidenceSet OPTIONAL, 
motionCfd MotionConfidenceSet OPTIONAL,
}
```

- utcTime DDateTime OPTIONAL日期和时间数据单元

```json
【定义】
定义完整的日期和时间数据单元。
【ASN.1 代码】
DDateTime::= SEQUENCE{
year DYear OPTIONAL, 
month DMonth OPTIONAL，
day DDay OPTIONAL,
hour D Hour OPTIONAL,
minute DMinute OPTIONAL, 
second DSecond OPTIONAL,
offset DTimeOffset OPTIONAL-- time zone
}
```

- - year DYear OPTIONAL公历年份

  - ```json
    【定义】
    定义公历年份。0表示未知年份。
    【ASN.1 代码】
    DYear:= INTEGER(0.4095)
    -- units of years
    ```

  - month DMonth OPTIONAL月份

  - ```json
    【定义】
    定义1年中的月份。有效范围是1～12。数值0表示未知月份。
    【ASN.1 代码】
    DMonth = INTEGER (0..12)
    -- units of months
    ```

  ```
    
  - day DDay OPTONAL日期
  
  - ```json
    【定义】
    定义1个月中的日期。有效范围是1～31。0表示未知日期。
    【ASN.1 代码】 
    DDay := INTEGER(0.31)
    -- units of days
  ```

  - hour DHour OPTIONAL小时时刻

  - ```json
    【定义】
    定义1天中的小时时刻。有效范围是0～23。24及以上表示未知或无效。
    【ASN.1 代码】
    DHour =INTEGER(0.31)
    -- units of hours
    ```

  - minute DMinute OPTIONAL分钟时刻

  - ```json
    【定义】
    定义1小时中的分钟时刻。有效范围是0～59。数值60表示未知分钟时刻。
    【ASN.1 代码】
    DMinute = INTEGER (0.60)
    -- units of minutes
    ```

  - secondDSecond OPTIONAL毫秒级时刻

  - ```json
    【定义】
    定义1分钟内的毫秒级时刻。分辨率为1毫秒，有效范围是0～599。60000及以上表示未知或无效数值。
    【ASN.1代码】
    DSecond := INTEGER (0.65535)
    -- units of milliseconds
    ```

  - offset DTimeOffet OPTIONAL和UTC时间的分钟差

  - ```json
    【定义】
    定义和UTC时间的分钟差，用来表示时区。比UTC快为正，否则为负。
    【ASN.1 代码】
    DTimeOfset ::= INTECER(-840.840)
    -- units of minutes from UTC time
    ```

- - heading Heading OPTIONAL车辆航向角

  - ```json
    【定义】
    为车辆航向角，即为车头方向与正北方向的顺时针夹角。分辨率为0.0125°。
    【ASN.1 代码】
    Heading := INTEGER (0.28800)
    -- ILSB of 0.0125 degrees
    -- A range of O to 359.9875 degrees
    ```



- - transmission TransmissionState OPTIONAL车辆档位状态

  - ```json
    【定义】
    定义车辆档位状态。具体定义如下∶
    ● Neutral∶ 空档;
    ● Park∶ 停止档;
    ● ForwardGears∶ 前进档;
    ● ReverseGears∶ 倒档。
    【ASN.1 代码】
    TransmissionSate ::= ENUMERATED{
    neutral (0),-- Neutral
    park(1), -- Park
    forwardGears (2),-- Forward gears 
    reverseGears (3), -- Reverse gears 
    reserved1 (4), 
    reserved2 (5),
    reserved3 (6),
    unavailable (7)-- not-equipped or unavailable value,
    -- Any related speed is relative to the vehicle reference frame used
    }
    ```

- - speed Speed OPTIONAL车速大小

  - ```json
    【定义】
    车速大小。分辨率为002mk。数值8191表示无效数值。
    【ASN.1 代码】
    Speed:= INTEGER(0.8191)
    -- Units of 0.02 m/s
    -- The value 8191 indicates that
    -- speed is unavailable
    ```

- - posAccuracy PositionConfidenceSet OPTIONAL位置（经纬度和高程）的综合精度

  - ```json
    【定义】
    定义位置（经纬度和高程）的综合精度。
    【ASN.1 代码】
    PositionConfidenceSet :;= SEQUENCE {
    pos PositionConfidence,--for both horizontal directions
    elevation ElevationConfidence OPTIONAL
    }
    ```

  - pos PositionConfidence95%置信水平的车辆位置精度

  - ```json
    【定义】
    数值描述了95%置信水平的车辆位置精度。该精度理论上只考虑了当前位置传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
    【ASN.1 代码】
    PositionConfidence ::= ENUMERATED {
    unavailable (0),-- B'0000 Not Equipped or unavailable 
    a500m(1),--B'0001 500m or about 5*10^-3 decimal degrees
    a200m(2),--B'0010 200m or about 2*10^-3 decimal degrees 
    a100m (3),-- B'0011 100m or about 1*10^-3 decimal degrees 
    a50m (4),--B'0100 50m or about 5*10^-4 decimal degrees
    a20m(5),-- B'0101 20m or about 2*10^-4 decimal degrees 
    a10m (6),-- B'0110 10m or about 1*10^-4 decimal degrees
    a5m(7),--B'0111 5m or about 5*10^-5 decimal degrees 
    a2m(8),--B'1000 2m or about 2*10^-5 decimal degrees 
    a1m((9),--B'1001 1m or about 1*10^-5 decimal degrees 
    a50cm(10),--B'1010 0.50m or about5*10^-6 decimal degrees
    a20cm(11),--B'1011 0.20m or about 2*10^-6 decimal degrees 
    a10cm(12),--B'1100 0.10m or about 1*10^-6 decimal degrees
    a5cm(13),--B'1101 0.05m or about 5*10^-7 decimal degrees 
    a2cm(14),--B'1110 0.02m or about 2*10^-7decimal degrees 
    a1cm(15),--B'1111 0.01m or about 1*10^-7decimal degrees
    }-- Encoded as a 4 bit value
    ```

  - elevation ElevationConfidence95%置信水平的车辆高程精度

  - ```json
    【定义】
    数值描述了95%置信水平的车辆高程精度。该精度理论上只考虑了当前高程传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
    【ASN.1 代码】
    ElevationConfidence := ENUMERATED{
    unavailable (0), -- B'0000 Not Equipped or unavailable
    elev-500-00 (1), -- B'0001(500 m) 
    elev-200-00 (2),--B'0010 (200 m) 
    elev-100-00(3), -- B'0011 (100 m) 
    elev-050-00(4), -- B'0100 (50 m) 
    elev-020-00(5),-- B'0101 (20m) 
    elev-010-00(6),--B'0110(10m) 
    elev-005-00(7),--B'0111(5m)
    elev-002-00(8),--B'1000(2m) 
    elev-001-00(9)-- B'1001(1m) 
    elev-000-50(10),--B'1010(50cm) 
    elev-000-20(11)--B'1011 (20cm) 
    elev-000-10(12),--B'1100(10cm) 
    elev-000-05 (13),--B'1101(5cm) 
    elev-000-02 (14).--B'1110(2cm) 
    elev-000-01 (15)--B'1111(1cm)
    }--Encoded as a 4 bit value
    ```

- - timeConfidence TimeConfidence OPTIONAL95%置信水平的时间精度

  - ```json
    【定义】
    数值描述了95%置信水平的时间精度。该精度理论上只考虑了当前计时系统本身传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
    【ASN.1代码】
    TimeConfidence ::= ENUMERATED {
    unavailable (0),-- Not Equipped or unavailable 
    time-100-000 (1),-- Better than 100 Seconds 
    time-050-000 (2), -- Better than 50 Seconds 
    time-020-000 (3), -- Beter than 20 Seconds 
    time-010-000(4), -- Better than 10 Seconds
    time-002-000(5),-- Better than 2 Seconds 
    time-001-000(6),-- Better than 1 Second 
    time-000-500(7),--Better than 0.5 Seconds 
    time-000-200(8),-- Better than 0.2 Seconds 
    time-000-100(9),--Better than 0.1 Seconds 
    time-00-050(10),-- Better than 0.05 Seconds 
    time-000-020(11),-- Better than 0.02 Seconds 
    time-000-010(12),--Better than 0.01 Seconds
    time-000-005 (13),--Better than 0.005 Seconds 
    time-000-002 (14),-- Better than 0.002 Seconds 
    time-000-001(15),-- Better than 0.001 Seconds
    -- Better than one millisecond 
    time-000-000-5(16),--Better than0.000,5 Seconds 
    time-000-000-2(17),--Better than 0.000,2 Seconds 
    time-000-000-1(18),--Better than 0.000,1 Seconds 
    time-000-000-05(19),--Better than 0.00,05 Seconds 
    time-000-000-02 (20),-- Better than 0.000,02 Seconds 
    time-000-000-01(21),-- Better than 0.000,01 Seconds 
    time-000-000-005 (22),-- Better than 0.000,005 Seconds 
    time-000-000-002 (23),-- Better than 0.000,002 Seconds 
    time-000-000-001(24),--Better than 0.000,001 Seconds
    -- Better than one micro second 
    time-000-000-000-5 (25),-- Better than 0.000,000,5 Seconds 
    time-000-000-000-2 (26),--Better than 0.000,000,2 Seconds 
    time-000-000-000-1 (27),--Better than 0.000,000,1 Seconds 
    time-000-000-000-05 (28),--Better than 0.000,000,05 Seconds
    time-000-000-000-02(29),--Better than 0.000,000,02 Seconds 
    time-000-000-000-01(30),-- Better than 0.000,000,01 Seconds 
    time-000-000-000-005(31),--Better than 0.000,000,005Seconds 
    time-000-000-000-002 (32),--Better than 0.000,000,002 Seconds 
    time-000-000-000-001 (33),--Better than 0.000,000,001 Seconds-- Better than one nano second 
    time-000-000-000-000-5(34),--Better than 0.000000,000,5 Seconds 
    time-000-000-000-000-2 (35),--Better than 0.000,000,000,2 Seconds 
    time-000-000-000-000-1 (36),--Better than 0.000,000,000,1 Seconds 
    time-000-000-000-000-05 (37),--Better than 0.00000,05 Seconds 
    time-000-000-000-000-02 (38),--Better than 0.000,000,000,02 Seconds 
    time-000-000-000-000-01 (39),-- Better than 0.000,000,000.01 Seconds
    }
    ```

- - posConfidence PositionConfidenceSet OPTIONAL位置（经纬度和高程）的综合精度

  - ```json
    【定义】
    定义位置（经纬度和高程）的综合精度。
    【ASN.1 代码】
    PositionConfidenceSet := SEQUENCE{
    pos PositionConfidence,--for both horizontal directions
    elevation ElevationConfidence OPTIONAL
    }
    ```

  - pos PositionConfidence95%置信水平的车辆位置精度

  - ```json
    【定义】
    数值描述了95%置信水平的车辆位置精度。该精度理论上只考虑了当前位置传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
    【ASN.1 代码】
    PositionConfidence ::= ENUMERATED {
    unavailable (0),-- B'0000 Not Equipped or unavailable 
    a500m(1),--B'0001 500m or about 5*10^-3 decimal degrees
    a200m(2),--B'0010 200m or about 2*10^-3 decimal degrees 
    a100m (3),-- B'0011 100m or about 1*10^-3 decimal degrees 
    a50m (4),--B'0100 50m or about 5*10^-4 decimal degrees
    a20m(5),-- B'0101 20m or about 2*10^-4 decimal degrees 
    a10m (6),-- B'0110 10m or about 1*10^-4 decimal degrees
    a5m(7),--B'0111 5m or about 5*10^-5 decimal degrees 
    a2m(8),--B'1000 2m or about 2*10^-5 decimal degrees 
    a1m((9),--B'1001 1m or about 1*10^-5 decimal degrees 
    a50cm(10),--B'1010 0.50m or about5*10^-6 decimal degrees
    a20cm(11),--B'1011 0.20m or about 2*10^-6 decimal degrees 
    a10cm(12),--B'1100 0.10m or about 1*10^-6 decimal degrees
    a5cm(13),--B'1101 0.05m or about 5*10^-7 decimal degrees 
    a2cm(14),--B'1110 0.02m or about 2*10^-7decimal degrees 
    a1cm(15),--B'1111 0.01m or about 1*10^-7decimal degrees
    }-- Encoded as a 4 bit value
    ```

  - elevation ElevationConfidence95%置信水平的车辆高程精度

  - ```json
    【定义】
    数值描述了95%置信水平的车辆高程精度。该精度理论上只考虑了当前高程传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
    【ASN.1 代码】
    ElevationConfidence := ENUMERATED{
    unavailable (0), -- B'0000 Not Equipped or unavailable
    elev-500-00 (1), -- B'0001(500 m) 
    elev-200-00 (2),--B'0010 (200 m) 
    elev-100-00(3), -- B'0011 (100 m) 
    elev-050-00(4), -- B'0100 (50 m) 
    elev-020-00(5),-- B'0101 (20m) 
    elev-010-00(6),--B'0110(10m) 
    elev-005-00(7),--B'0111(5m)
    elev-002-00(8),--B'1000(2m) 
    elev-001-00(9)-- B'1001(1m) 
    elev-000-50(10),--B'1010(50cm) 
    elev-000-20(11)--B'1011 (20cm) 
    elev-000-10(12),--B'1100(10cm) 
    elev-000-05 (13),--B'1101(5cm) 
    elev-000-02 (14).--B'1110(2cm) 
    elev-000-01 (15)--B'1111(1cm)
    }--Encoded as a 4 bit value
    ```

- - motionCfd MotionConfidenceSet OPTIONAL车辆运行状态的精度

  - ```json
    【定义】
    描述车辆运行状态的精度。包括车速精度、航向精度和方向盘转角精度。
    【ASN.1 代码】
    MotionConfidenceSet ::= SEQUENCE { 
    speedCfd SpeedConfidence OPTIONAL,
    headingCfd HeadingConfidence OPTIONAL,
    steerCfd SteeringWheelAngleConfidence OPTIONAL
    }
    ```

  - speedCfd SpeedConfidence OPTIONAL95%置信水平的车速精度

- ```json
  【定义】
  数值描述了95%置信水平的车速精度。该精度理论上只考虑了当前车速传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
    【ASN.1 代码】
    SpeedConfidence ::= ENUMERATED {
    unavailable (0),-- Not Equipped or unavailable 
    prec100ms (1), -- 100 meters / sec 
    prec10ms (2), -- 10 meters / sec 
    prec5ms (3), --5 meters / sec 
    prec1ms (4), --1 meters / sec
    prec0-1ms(5),--0.1 meters/sec 
    prec0-05ms(6),--0.05 meters/sec 
    prec0-01ms(7)--0.01 meters/sec
    }-- Encoded as a 3 bit value
  ```

  - headingCfd HeadingConfidence OPTIONAL95%置信水平的车辆航向精度

  - ```json
    【定义】
    数值描述了95%置信水平的车辆航向精度。该精度理论上只考虑了当前航向传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
    【ASN.1代码】
    HeadingConfidence ::=ENUMERATED{
    unavailable (0),--B'000 Not Equipped or unavailable 
    prec10deg (1),-- B'010 10 degrees 
    prec05deg(2), -- B'011 5 degrees 
    prec01deg (3),-- B'100 1 degrees 
    prec0-1deg (4),--B'101 0.1 degrees 
    prec0-05deg (5),-- B'110 0.05 degrees 
    prec0-01deg (6),-- B'110 0.01 degrees
    prec0-0125deg((7),--B'111 0.0125 degrees,aligned with heading LSB
    } -- Encoded as a 3 bit value
    ```

  - steerCfd SteeringWheelAngleConfidence OPTIONAL95%置信水平的方向盘转角精度

  - ```json
    【定义】
    数值描述了95%置信水平的方向盘转角精度。该精度理论上只考虑了当前方向盘转角传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
    【ASN.1代码】
    SteeringWheelAngleConfidence ::= ENUMERATED {
    unavailable (0),-- B'00 Not Equipped with Wheel angle
    -- or Wheel angle status is unavailable 
    prec2deg (1),-- B'01 2 degrees 
    prec1deg (2), -- B'10 1 degree
    prec0-02deg(3), --B'11 0.02 degrees
    }-- Encoded as a 2bit value
    ```



#### 2. currGNSSstatus GNSSstatus OPTIONALGNSS系统工作状态

```json
【定义】
定义 GNSS系统工作状态。包括设备工作状态、锁星情况和修正信息等。GNSS系统可以是GPS、北斗等相关系统和设备。【ASN.1 代码】
GNSSstatus ::= BIT STRING {
unavailable (0),--Not Equipped or unavailable
isHealthy (1), 
isMonitored (2),
baseStationType(3),--Set to zero if a moving base station,
--or if a rover device (an OBU),
--set to one if it is a fixed base station
aPDOPofUnder5(4),--A dilution of precision greater than5 
inViewOfUnder5 (5),--Less than5 satellites in view 
localCorrectionsPresent (6),-- DGPS type corrections used 
networkCorrectionsPresent(7)--RTK type corrections used
}(SIZE(8))
```



#### 3. crumbData PathHistoryPointList车辆的历史轨迹点列表

```json
【定义】
定义车辆的历史轨迹点列表。该轨迹由一系列轨迹点组成。能够精准地给出车辆完整的历史行驶轨迹，可以以当前时刻运动状态为基准，也可以是一段时间之前的轨迹。
【ASN.1 代码】
PathHistoryPoinList ::=SEQUENCE(SIZE(1..23))OF PathHistoryPoint
```

##### PathHistoryPoint车辆的历史轨迹点

```json
【定义】
定义车辆的历史轨迹点。包括位置、时间戳，以及轨迹点处的车速、位置精度和航向等。
【ASN.1 代码】
PathHistoryPoint ::= SEQUENCE {
llvOffset PositionOffsetLLV, 
timeOffset TimeOffset,
-- Offset backwards in time 
speed Speed OPTIONAL,
-- Speed over the reported period
posAccuracy PositionConfidenceSet OPTIONAL,
--The accuracy of this value 
heading CoarseHeading OPTIONAL
-- overall heading
..
}
```

-  llvOffset PositionOffsetLLV三维的相对位置

```json
【定义】
定义三维的相对位置（相对经纬度和相对高程）。
【ASN.1 代码】
PositionOffsetLLV ::= SEQUENCE{ 
offsetLL PositionOffsetLL,
-- offset in lon/lat
offsetV VerticalOffset OPTIONAL
-- offset in elevation
}
```

![image-20210302110211747](D:\self\smart-city\img\image-20210302110211747.png)



- timeOffet TimeOffset和UTC时间的分钟差

```json
【定义】
定义和UTC时间的分钟差，用来表示时区。比 UTC快为正，否则为负
【ASN.1代码】
DTimeOffset = INTEGER (-840.840)
-- units of minutes from UTC time
```



- speed Speed OPTIONAL车速大小

```json
【定义】
车速大小。分辨率为0.02 m/s。数值8191表示无效数值。【ASN.1 代码】
Speed := INTEGER (0.8191)
-- Units of 0.02 m/s
-- The value 8191 indicates that
-- speed is unavailable
```



- posAccuracy PositionConfidenceSet OPTIONAL位置（经纬度和高程）的综合精度

```json
【定义】
定义位置（经纬度和高程）的综合精度。
【ASN.1 代码】
PositionConfidenceSet ::= SEQUENCE {
pos PositionConfidence,-- for both horizontal directions 
elevation ElevationConfidence OPTIONAL
}
```

- - pos PositionConfidence95%置信水平的车辆位置精度

  - ```json
    【定义】
    数值描述了95%置信水平的车辆位置精度。该精度理论上只考虑了当前位置传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
    【ASN.1 代码】
    PositionConfidence := ENUMERATED { 
    unavailable (0,-- B‘0000 Not Equipped or unavailable 
    a500m (1),-- B'0001 500m or about 5*10^-3 decimal degrees
    a200m (2),--B'0010 200m or about 2*10^-3 decimal degrees 
    a100m (3),--B'0011 100m or about 1*10^-3 decimal degrees 
    a50m (4),--B'0100 50m or about 5*10^-4 decimal degrees
    a20m((5),—-B'0101 20mor about 2*10^-4 decimal degrees
    a10m(6),-- B'0110 10m or about 1*10^-4 decimal degrees 
    a5m (7),--B'0111 5m or about 5*10^-5 decimal degrees 
    a2m(8),--B'1000 2m or about 2*10^-5 decimal degrees
    a1m(9),--B'1001 1m or about 1*10^-5 decimal degrees
    a50cm(10),--B'1010 0.50m or about 5*10^-6 deimal degrees 
    a20cm(11),--B'1011 0.20m or about 2*10~-6 decimal degees 
    a10cm(12),--B1100 0.10m or about 1*10~-6 decimal degees 
    a5cm(13),--B'1101 0.05m or about 5*10^-7 decimal degrees
    a2cm(14),--B'1110 0.02m or about 2*10^-7 decimal degrees 
    a1cm(15)--B'1111 0.01m or about 1*10^-7 decimal degrees
    }-- Encoded as a 4 bit value
    ```

  - elevation ElevationConfidence95%置信水平的车辆高程精度

  - ```json
    【定义】
    数值描述了95%置信水平的车辆高程精度。该精度理论上只考虑了当前高程传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
    【ASN.1 代码】
    ElevationConfidence ::= ENUMERATED{
    unavailable (0),-- B'0000 Not Equipped or unavailable 
    elev-500-00 (1),--B'0001 (500 m) 
    elev-200-00 (2), -- B'0010 (200 m) 
    elev-100-00 (3), -- B'0011 (100 m) 
    elev-050-00 (4), -- B'0100 (50 m) 
    elev-020-00 (5),--B'0101 (20m) 
    elev-010-00(6),-- B'0110 (10m) 
    elev-005-00(7),-- B'0111 (5 m) 
    elev-002-00(8),--B'1000 (2 m) 
    elev-001-00 (9),--B'1001(1m) 
    elev-000-50(10),--B'1010(50cm) 
    elev-000-20(11),--B'1011((20cm) 
    elev-000-10(12),--B'1100(10cm) 
    elev-000-05(13),--B'1101(5cm) 
    elev-000-02 (14),--B'1110(2cm) 
    elev-000-01(15),-- B1111(1 cm)
    }--Encoded as a 4 bit value
    ```

    

- heading CoarseHeading OPTIONAL车辆航向角

```json
【定义】
定义粗粒度的车辆航向角。分辨率为1.5°。
【ASN.1代码】
CoarseHeading ::=INTEGER (0.240)
--Where the LSB is in units of 1.5 degrees
--over a range of 0～ 358.5 degrees
-- the value 240 shall be used for unavailable
```



### 2.2.3 pathPrediction PathPrediction OPTIONAL车辆的预测线路

```json
【定义】
定义车辆的预测线路，主要是预测线路的曲率半径。
【 ASN.1 代码】
PathPrediction ::= SEQUENCE { 
radiusOfCurve RadiusOfCurvature,
-- LSB units of 10cm
-- straight path to use value of32767 
confidence Confidence,
-- LSB units of 0.5 percent
}
```

- radiusOfCurve RadiusOfCurvature车辆预测自身前方行驶轨迹的曲率半径

```json
【定义】
表示车辆预测自身前方行驶轨迹的曲率半径。数值可能来源于地图数据、曲率传感器、视觉传感器、定位系统等。 分辨率为10cm。轨迹曲线向右偏转（圆心在车辆行驶方向右侧）数值为正，向左则为负。数值32767 表示直线行驶。
【ASN.1代码】
RadiusOFCurvature ::= INTEGER ((-32767..32767)
-- LSB units of 10cm
-- A straight path to use value of 32767
```

- confidence Confidence置信度

```json
【定义】
定义置信度。分辨率为 0.005。
【ASN.1 代码】Confidence:= INTEGER (0.200)
--ISB units of 0.5 percent
```



### 2.2.4 lights ExteriorLights OPTIONAL车身周围的车灯状态

```json
【定义】
定义车身周围的车灯状态。
【ASN.1 代码】
ExteriorLights ::= BIT STRING{ 
-- All lights off is indicated by no bit set 
lowBeamHeadlightsOn (0), 
highBeamHeadlightsOn(1)), 
leftTurnSignalOn (2), 
rightTurnSignalOn (3), 
hazardSignalOn (4), 
automaticLightControlOn (5), 
daytimeRunningLightsOn(6), 
fogLightOn (7), 
parkingLightsOn(8)
}(SIZE (9,…))
```



## 2.3 accelSet AccelerationSet4Way车辆四轴加速度

```json
【定义】
定义车辆四轴加速度。其中∶
●Long∶ 纵向加速度。向前加速为正，反向为负;
● Lat∶横向加速度。向右加速为正，反向为负;
●Ven∶垂直加速度。沿重力方向向下为正，反向为负;
●Yaw∶ 横摆角速度。顺时针旋转为正，反向为负。
【ASN. 代码】
AccelerationSet4Way ::= SEQUENCE{
long Acceleration,
--Along the Vehicle Longitudinal axis 
lat Acceleration,
--Along the Vehicle Lateral axis
vert VerticalAcceleration,
-- Along the Vehicle Vertical axis
yaw YawRate
}
```

### long Acceleration加速度

```json
【定义】
定义车辆加速度。分辨率为0.01m/s²，数值2001为无效数值。【ASN.1 代码】 
Acceleration ::= INTEGER (-2000..2001)
--LSB units are 0.01 m/s^2
--the value 2000 shall be used for values greater than 2000
-- the value -2000 shall be used for values less than-2000
--a value of 2001 shall be used for Unavailable
```

### lat Acceleration加速度

```json
【定义】
定义车辆加速度。分辨率为0.01m/s²，数值2001为无效数值。【ASN.1 代码】 
Acceleration ::= INTEGER (-2000..2001)
--LSB units are 0.01 m/s^2
--the value 2000 shall be used for values greater than 2000
-- the value -2000 shall be used for values less than-2000
--a value of 2001 shall be used for Unavailable
```

###  vert VerticalAccelerationZ轴方向的加速度

```json
【定义】
定义Z轴方向的加速度大小，Z轴方向竖直向下，沿着Z轴方向为正。分辨率为0.02g，g为重力加速度典型值 9.80665 m/s32。【ASN.1 代码】
VerticalAcceleration ::= INTEGER(-127..127)
-- LSB units of 0.02 G steps over-2.52 to +2.54 G
--The value +127 shall be used for ranges >= 2.54 G
--The value -126 shall be used for ranges <= 2.52 G
--The value -127 shall be used for unavailable
```

### yaw YawRate 车辆横摆角速度

```json
【定义】
车辆横摆角速度。指汽车绕垂直轴的偏转，该偏转的大小代表汽车的稳定程度。如果偏转角速度达到一个阈值，说明汽车处于发生测滑或者甩尾等的危险工况。顺时针旋转为正，逆时针为负。数据分辨率为 0.01° /s。 
【ASN.1 代码】
YawRate ::= INTEGER (-32767..32767)
-- LSB units of 0.01 degrees per second (signed)
```



## 2.4 motionCfd MotionConfidenceSet OPTIONAL运行状态精度

```json
【定义】
描述车辆运行状态的精度。包括车速精度、航向精度和方向盘转角精度。
【ASN.1代码】
MotionConfidenceSet ::= SEQUENCE {
speedCfd SpeedConfidence OPTIONAL,
headingCfd HeadingConfidence OPTIONAL,
steerCfd SteeringWheelAngleConfidence OPTIONAL
}
```

###  speedCfd SpeedConfidence OPTIONAL95%置信水平的车速精度

```json
【定义】
数值描述了95%置信水平的车速精度。该精度理论上只考虑了当前车速传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
【ASN.1 代码】
SpeedConfidence ::= ENUMERATED {
unavailable (0) -- Not Equipped or unavailable 
prec100ms (1), -- 100 meters / sec 
prec10ms (2),-- 10 meters / sec 
prec5ms (3),--5 meters / sec 
prec1ms (4), --1 meters / sec
prec0-1ms(5),--0.1 meters/sec 
prec0-05ms(6),--0.05 meters/sec 
prec0-01ms(7)--0.01 meters/sec
}--Encoded as a 3 bit value
```

### headingCfd HeadingConfidence OPTIONAL95%置信水平的车辆航向精度

```json
【定义】
数值描述了95%置信水平的车辆航向精度。该精度理论上只考虑了当前航向传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
【ASN.1 代码】
HeadingConfidence ::= ENUMERATED {
unavailable (0),--B'000 Not Equipped or unavailable 
prec10deg (1),-- B'010 10 degrees 
prec05deg (2), -- B'011 5 degrees 
prec01deg (3), -- B'100 1 degrees 
prec0-1deg (4),--B'101 0.1 degrees
prec0-05deg(5),-- B'110 0.05 degrees 
prec0-01deg (6),-- B'110 0.01 degrees
prec0-0125deg((7)--B'111 0.0125 degrees,aligned with heading LSB
}-- Encoded as a 3 bit value
```

### steerCfd SteeringWheelAngleConfidence OPTIONAL95%置信水平的方向盘转角精度

```json
【定义】
数值描述了95%置信水平的方向盘转角精度。该精度理论上只考虑了当前方向盘转角传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
【ASN.1代码】
SteeringWheelAngleConfidence ::=ENUMERATED{
unavailable (0), -- B'00 Not Equipped with Wheel angle
-- or Wheel angle status is unavailable 
prec2deg (1),-- B'01 2 degrees
prec1deg (2),-- B'10 1 degree 
prec0-02deg (3)-- B'11 0.02 degrees
}--Encoded as a 2 bit value
```



## 2.5 vehicleClass VehicleClassification车辆的分类

```json
【定义】
定义车辆的分类，可从各个维度对车辆类型进行定义。目前仅有车辆基本类型一项。
【ASN.1 代码】
VehicleClassification ::= SEQUENCE {
classification BasicVehicleClass,
...
}
```

### classification BasicVehicleClass车辆基本类型

```json
【定义】
定义车辆基本类型。
【ASN.1代码】
BasicVehicleClass ::= INTEGER 0.255) 
unknown VehicleClass Basic VehicleClass ::= 0
--Not Equipped, Not known or unavailable 

specialVehicleClass BasicVehicleClass ::= 1
-- Special use
-- Basic Passenger Motor Vehicle Types

passenger-Vehicle-TypeUnknown BasicVehicleClass ::= 10--default type 

passenger-Vehicle-TypeOther BasicVehicleClass::= 11
-- various fuel types are handled in another element
-- Light Trucks, Pickup,Van, Panel

lightTruck-Vehicle-TypeUnknown BasicVehicleClass ::=20--default type 
lighrTruck-Vehicle-TypeOther BasicVehicleClass::= 21
--Trucks, Various axle types, includes HPMS items
truck-Vehicle-TypeUnknown BasicVehicleClass = 25--default type 
truck-Vehicle-TypeOther BasicVehicleClass ::= 26
truck-axleCnt2 BasicVehicleClass ::=27--Two axle,six tire single units 
truck-axleCn3 BasicVehicleClass ::=28--Three axle,single units 
truck-axleCnt4 BasicVehicleClass ::=29-- Four or more axle,single unit 
truck-axleCnt4Trailer BasicVehicleClass ::=30--Four or less axle,single trailer 
truck-axleCnt5Trailer BasicVehicleClass  ::= 31--Five or less axle,single trailer 
truck-axleCnt6Trailer BasicVehicleClass ::=32--Six or more axle,single trailer 
truck-axleCnt5 MultiTrailer BasicVehicleClass::=33--Five or less axle,multi-trailer 
truck-axleCnt6MultiTrailer BasicVehicleClass::= 34--Six axle,multi-trailer 
truck-axleCnt7MultiTrailer BasicVehicleClass::=35--Seven or more axle,multi-trailer
-- Motorcycle Types
motorcycle-TypeUnknown BasicVehicleClass ::= 40--default type 
motorcycle-TypeOther BasicVehicleClass ::= 41 
motorcycle-Cruiser-Standard BasicVehicleClass ::= 42 
motorcycle-SportUnclad BasicVehicleClass ::= 43 
motorcycle-SportTouring BasicVehicleClass ::= 44
motorcycle-SuperSport BasicVehicleClass ::= 45 
motoreycle-Touring BasicVehicleClass::= 46 
motorcycle-Trike BasicVehicleClass ::= 47
motorcycle-wPassengers BasicVehicleClass::= 48--type not stated 
-- Transit Types
transit-TypeUnknown BasicVehicleClass ::= 50--default type
transit-TypeOther BasicVehicleClass ::= 51 
transit-BRT BasicVehicleClass ::= 52 
transit-ExpressBus BasicVehicleClass ::= 53 
transit-LocalBus BasicVehicleClass ::= 54 
transit-SchoolBus BasicVehicleClass ::=55 
transit-FixedGuideway BasicVehicleClass ::= 56 
transit-Paratransit BasicVehicleClass ::= 57
transit-Paratransit-Ambulance BasicVehicleClass ::=58
--Emergency Vehicle Types 
emergency-TypeUnknown BasicVehicleClass ::=60--default type 
emergency-TypeOther BasicVehicleClass ::=61--includes federal users 
emergency-Fire-Light-Vehicle BasicVehicleClass ::=62 
emergency-Fire-Heavy-Vehicle BasicVehicleClass ::= 63 
emergency-Fire-Paramedic-Vehicle BasicVehicleClass::=64 
emergency-Fire-Ambulance-Vehicle BasicVehicleClass ::= 65 
emergency-Police-Ligh-Vehicle BasicVehicleClass::= 66 
emergency-Police-Heavy-Vehicle BasicVehicleClass ::=67 
emergency-Other-Responder BasicVehicleClass ::= 68 
emergency-Other-Ambulance BasicVehicleClass ::= 69
-- Other V2X Equipped Travelers
otherTraveler-TypeUnknown BasicVehicleClass ::= 80-- default type 
otherTraveler-TypeOther BasicVehicleClass ::= 81 
otherTraveler-Pedestrian BasicVehicleClass ::= 82 
otherTraveler-Visually-Disabled BasicVehicleClass::= 83
otherTraveler-Physically-Disabled BasicVehicleClass::= 84 
otherTraveler-Bicycle BasicVehicleClass ::= 85
otherTraveler-Vulnerable-Roadworker BasicVehicleClass::= 86
-- Other V2X Equipped Device Types
infrastructure-TypeUnknown BasicVehicleClass ::=90-- default type 
infrastructure-Fixed BasicVehicleClass ::= 91 
infrastructure-Movable BasicVehicleClass::= 92 
equipped-CargoTrailer BasicVehicleClass = 93
```



## 2.6 angle SteeringWheelAngle OPTIONAL 方向盘转角

```json
【定义】
方向盘转角。向右为正，向左为负。分辨率为1.5°。数值127为无效数值。
【ASN.1 代码】
SteeringWheelAngle ::= INTEGER (-126..127)
--ISB units of 1.5 degrees,a range of-189 to+189 degrees 
-- +001 = +1.5 deg
-- -126 =-189 deg and beyond 
-- +126 = +189 deg and beyond 
--+127 to be used for unavailable
```

## 2.7 msgCnt MsgCount消息计数

```json
【定义】 
发送方为自己发送的同类消息，依次进行编号。编号数值为 0 ～ 127。 当发送方开始发起某一类数据时，它可以随机选择起始编号，随后依次递增。发送方也可以在 连续发送相同的数据帧时，选择使用相同的 MsgCount 消息编号。编号到达 127 后，则下一个回到 0。 
【ASN.1 代码】 
MsgCount ::= INTEGER (0..127)
```

## 2.8 plate板块

```json
NoOCTETSTRING SIZE(4.16)OPTIONAL
```

## 2.9 secMark DSecond秒

```json
DSecond
【定义】
定义1分钟内的毫秒级时刻。分辨率为1毫秒，有效范围是0～5999。600及以上表示未知或无效数值。
【ASN.1 代码】
DSecond ::= INTEGER (0.65535)
-- units of milliseconds	
```

## 2.10 pos Position3D三维的坐标位置

```json
【定义】
三维的坐标位置，包括经纬度和高程。
【ASN.1 代码】
Position3D := SEQUENCE{
lat Latitude,
--in I/10th micro degrees
long Longitude, 
--in I/10th micro degrees
elevation Elevation OPTIONAL 
-- in 10 cm units
}
```

### lat Latitude纬度

```json
【定义】
定义纬度数值，北纬为正，南纬为负。分辨率1e-7°。
【ASN.1 代码】
Latitude:= INTEGER(-900000.9000001)
--LSB= 1/10 micro degree
--Providing a range of plus-minus 90 degrees
```

### long Longitude经度

```json
【定义】
定义经度数值。东经为正，西经为负。分辨率为1e-7°。
【ASN.1 代码】
Longitude ::= INTEGER(-17999999..180000001)
-- ISB= 1/10 micro degree 
-- Providing a range of plus-minus 180 degrees
```

### elevation Elevation OPTIONAL 海拔

```json
【定义】
定义车辆海拔高程。分辨率为0.1米。数值-4096 表示无效数值。【ASN.1 代码】
Elevation ::= INTEGER (-4096..61439)
-- In units of 10cm steps above or below the reference ellipsoid
-- Providing a range of-409.5 to＋6143.9 meters
-- The value-4096 shall be used when Unknown is to be sent
```

## 2.11 accuracy PositionConfidenceSet位置（经纬度和高程）的综合精度

```json
【定义】
定义位置（经纬度和高程）的综合精度。
【ASN.1 代码】
PositionConfidenceSet ::= SEQUENCE {
pos PositionConfidence,	
--for both horizontal directions 
elevation ElevationConfidence OPTIONAL
}
```

### pos PositionConfidence95%置信水平的车辆位置精度

```json
【定义】
数值描述了95%置信水平的车辆位置精度。该精度理论上只考虑了当前位置传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
【ASN.1 代码】
PositionConfidence ::= ENUMERATED {
unavailable (O),-- B'0000 Not Equipped or unavailable 
a500m (1),-- B'0001 500m or about 5*10^-3 decimal degrees
a200m (2),-- B'0010 200m or about 2*10^-3 decimal degrees 
a100m(3),--B'0011 100m or about 1*10^-3 decimal degrees 
a50m(4),-- B'0100 50m or about 5*10^-4 decimal degrees
a20m(5),--B'0101 20m or about 2*10^-4 decimal degrees
a10m(6),--B'0110 10m or about 1*10^~-4 decimal degrees 
a5m(7),--B'0111 5m or about 5*10^-5 decimal degrees 
a2m(8),--B'1000 2m or about 2*10^-5 decimal degrees
a1m(9),--B'1001 1m or about 1*10^-5 decimal degrees 
a50cm (10),--B'1010 0.50m or about5*10^-6 decimal degrees    
a20cm(11),--B'1011 0.20m or about 2*10^-6 decimal degrees  
a10cm(12),--B'1100 0.10m or about1*10^-6 decimal degrees 
a5cm(13),--B'1101 0.05m or about 5*10^-7 decimal degrees
a2cm(14),--B'1110 0.02m or about 2*10^-7 decimal degrees
a1cm(15)--B'1111 0.01m or about 1*10^-7 decimal degrees
}-- Encoded as a 4 bit value
```

### elevation ElevationConfidence95%置信水平的车辆高程精度

```json
【定义】
数值描述了95%置信水平的车辆高程精度。该精度理论上只考虑了当前高程传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
【ASN.1 代码】
ElevationConfidence ::= ENUMERATED {
unavailable (0),-- B'0000 Not Equipped or unavailable
 elev-500-00 (1),-- B'0001 (500 m)
 elev-200-00 (2), -- B'0010 (200 m)
 elev-100-00 (3), -- B'0011(100 m) 
elev-050-00(4), --B'0100(50 m)
elev-020-00(5),--B'0101 (20m) 
elev-010-00(6),--B‘0110(10m) 
elev-005-00(7),-- B'0111(5m) 
elev-002-00(8),--B'1000(2m) 
elev-001-00(9),--B'1001(1m) 
elev-000-50(10),--B'1010(50cm)
elev-000-20(11),--B'1011(20cm) 
elev-000-10(12),--B'1100(10cm) 
elev-000-05(13),--B'1101(5cm) 
elev-000-02(14).--B'1110(2cm) 
elev-000-01(15)-B'1111(1cm)
}--Encoded as a 4 bit value
```

## 2.12 transmission TransmissionState车辆档位状态

```json
【定义】
定义车辆档位状态。具体定义如下∶
● Neutral∶空档;
● Park∶停止档;
● ForwardGears∶ 前进档;
● ReverseGears∶ 倒档。
【ASN.1 代码】
TransmissionState ::= ENUMERATED{
neutral(0),-- Neutral 
park (1),--Park
forwardGears (2), -- Forward gears
reverseGears (3) -- Reverse gears 
reserved1 (4), 
reserved2 (5),
reserved3 (6),
unavailable (7)-- not-equipped or unavailable value,
--Any related speed is relative to the vehicle reference frame used 
}
```

## 2.13  speed Speed车速

```json
【定义】
车速大小。分辨率为0.02 m/。数值8191表示无效数值。
【ASN.1 代码】
Speed ::= INTEGER (0..8191)
-- Units of 0.02 m/s
-- The value 8191 indicates that 
-- speed is unavailable
```

## 2.14 heading Heading车辆航向角

```json
【定义】
为车辆航向角，即为车头方向与正北方向的顺时针夹角。分辨率为0.0125°。
【ASN.1 代码】
Heading ::= INTEGER (0..28800)
-- LSB of 0.0125 degrees
-- A range of 0 to 359.9875 degrees
```

## 2.15  size VehicleSize车辆尺寸大小

```json
【定义】
定义车辆尺寸大小。由车辆长、宽、高三个维度来定义，其中高度数值为可选项。
【ASN.1 代码】
VehicleSize ::= SEQUENCE {
width VehicleWidth,
 length VehicleLength, 
 height VehicleHeight OPTIONAL
}
```

### width VehicleWidth车辆车身宽度

```json
【定义】
定义车辆车身宽度。分辨率为1cm。数值0表示无效数据。【ASN.1 代码】
VehicleWidth ::= INTEGER (0..1023)-
--LSB units are 1cm with a range of>10meters
```

###  length VehicleLength车辆车身长度

```json
【定义】
定义车辆车身长度。分辨率为1cm。数值0表示无效数据。【ASN.1 代码】
VehicleLength ::= INTEGER(0..4095)
--LSB units of 1cm with a range of >40meters
```

###  height VehicleHeight OPTIONAL车辆车身高度

```json
【定义】
定义车辆车身高度。分辨率为5cm。数值0表示无效数据。【ASN.1代码】
VehicleHeight ::= INTEGER 0.127)
--LSB units of 5 cm,range to 6.35 meters
```

## 2.16  brakes BrakeSystemStatus车辆的刹车系统状态

```json
【定义】
定义车辆的刹车系统状态。包括如下7种不同类型的状态∶
● brakePadel∶刹车踏板踩下情况;
● wheelBrakes∶ 车辆车轮制动情况;
● traction∶牵引力控制系统作用情况;
● abs∶ 制动防抱死系统作用情况;
● scs∶ 车身稳定控制系统作用情况;
● brakeBoost∶ 刹车助力系统作用情况;
● auxBrakes∶ 辅助制动系统（一般指手刹）情况。
【ASN.1 代码】
BrakeSystemStatus ::= SEQUENCE{
brakePadel BrakePedalStatus OPTIONAL,
wheelBrakes BrakeAppliedStatus OPTIONAL,
traction TractionControlStatus OPTIONAL, 
abs AntiLockBrakeStatus OPTIONAL, 
scs StabilityControlStatus OPTIONAL,
 brakeBoost BrakeBoostApplied OPTIONAL,
 auxBrakes AuxiliaryBrakeStatus OPTIONAL,
}
```

### brakePadel BrakePedalStatus OPTIONAL刹车踏板状态

```json
【定义】
指示刹车踏板状态，即是否处在被踩下状态。
【ASN.1代码】
BrakePedalStatus ::= ENUMERATED{
unavailable (0),--Vehicle brake pedal detector is unavailable 
off(1),--Vehicle's brake padel is not pressed 
on (2)-- Vehicle's brake padel is pressed
}
```

### wheelBrakes BrakeAppliedStatus OPTIONAL四轮分别的刹车状态

```json
【定义】
定义四轮分别的刹车状态。这里将车辆的轮胎分为左前、右前、左后、右后四组。当车辆进行刹车时，该数值分别指示了四组轮胎的刹车情况。当车辆为单排轮胎（摩托车等）时，分别以左前和左后表示其前、后轮，后侧轮胎对应数值置为0。当车辆某一组轮胎由多个组成时，其状态将等效为一个数值来表示。【ASN.1 代码】
BrakeAppliedStatus ::= BIT STRING {
unavailable (0),--When set,the brake applied status is
unavailable 
lefFront (1), -- Left Front Active 
leftRear (2), --Left Rear Active 
rightFront (3),-- Right Front Active 
rightRear(4),--Right Rear Active
} (SIZE (5))
```

### traction TractionControlStatus OPTIONAL牵引力控制系统实时状态

```json
【定义】
定义牵引力控制系统实时状态。具体定义如下∶● Unavailable∶ 系统未装备或不可用;● Off∶ 系统处于关闭状态;● On∶ 系统处于开启状态，但未触发;● Engaged∶ 系统被触发，处于作用状态。
【ASN.1 代码】
TractionControlStatus ::= ENUMERATED {
unavailable (0),--B'00 Not Equipped wih traction control
--or traction control status is unavailable
off (1),-- B'01 traction control is Off
on(2),--B'10 traction control is On(but not Engaged) 
engaged(3)-- B'11 traction control is Engaged
}
```

### abs AntiLockBrakeStatus OPTIONAL刹车防抱死系统（ABS）状态

```json
【定义】
定义刹车防抱死系统（ABS）状态。
【ASN.1代码】
AntiLockBrakeStatus ::= ENUMERATED{
unavailable (0),--B'00 Vehicle Not Equipped with ABS Brakes
-- orABS Brakes status is unavailable 
off(1),--B'01 Vehicle's ABS are Off
on(2),--B'10 Vehicle's ABS are On( but not Engaged) 
engaged(3)--B'11 Vehicle's ABS control is Engaged on any wheel
}
```

### scs StabilityControlStatus OPTIONAL车辆动态稳定控制系统状态

```json
【定义】
定义车辆动态稳定控制系统状态。具体定义如下∶● Unavailable∶系统未装备或不可用;● Of∶ 系统处于关闭状态;● On∶ 系统处于开启状态，但未触发;● Engaged∶系统被触发，处于作用状态。
【ASN.1 代码】
StabilityControlStatus ::= ENUMERATED{
unavailable (0),--B'00 Not Equipped withSC
--or SC status is unavailable 
off(1),-- B'01 Off
on(2).--B'10 On or active(but not engaged) 
engaged(3)--B'll stability control is Engaged
}
```

###  brakeBoost BrakeBoostApplied OPTIONAL刹车辅助系统的状态

```json
【定义】
通过刹车辅助系统的状态，指示车辆紧急刹车状态。刹车辅助系统通过对情况的判断，确定是否需要急刹车，进而确定是否需要接管刹车系统，在驾驶员未来得及做出反应时进行刹车。辅助系统可能通过监测油门踏板的突然松开或前置检测器，来判断紧急刹车的需求。
【ASN.1 代码】
BrakeBoostApplied ::= ENUMERATED ({
unavailable (0), -- Vehicle not equipped with brake boost
-- or brake boost data is unavailable 
off (1), -- Vehicle's brake boost is off 
on (2)--Vehicle's brake boost is on(applied)
}
```

###  auxBrakes AuxiliaryBrakeStatus OPTIONAL指示刹车辅助系统状态

```json
【定义】
指示刹车辅助系统状态（通常为手刹）。
【ASN.1代码】
AuxiliaryBrakeStatus ::= ENUMERATED {
unavailable(0),--B'00 Vehicle Not Equipped with Aux Brakes
-- or Aux Brakes status is unavailable 
off (1),-- B'01 Vehicle's Aux Brakes are Off 
on(2),--B'10 Vehicle's Aux Brakes are On (Engaged) 
reserved (3) -- B'11
}
```