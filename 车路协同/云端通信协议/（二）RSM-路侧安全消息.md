[TOC]

# 一、RSM路侧安全消息10毫秒周期传感器人工智能相关的通过这个发出来

```json
RoadsideSafetyMessage ::= {
    msgCnt: 111    // 计数器   判断数据连续性
    id: 72 73 75 30 30 30 30 33      //RSU 设备编号
    refPos: Position3D ::= {     //--交通警报位置（交通标志或事件)      三维坐标位置
        lat: 281132739
        long: 1128669787
        elevation: 553
    }
    participants: ParticipantList ::= {  //交通参与者列表，应用于RSM 消息中 ，表示所有或部分RSU当前探测到的交通参与者信息
        ParticipantData ::= {  //定义交通参与者的基本安全信息。对应 BSM 消息，该参与者信息由 RSU 探测得到
            ptcType: 3 (pedestrian)     // 参与者事务类型  车 ，行人，根据国标来判断的。
            ptcId: 1     //   场景类型     见微信王泽涛   行人闯入 
            source: 3 (video)  //定义路侧交通参与者数据的检测器来源
            id: 参与者ID	
            secMark: 9732    // //定义毫米级时刻   
            pos: PositionOffsetLLV ::= {   //定义三维的相对位置
                offsetLL: Position-LL-24B ::= {  //24 比特相对经纬度位置，表示当前位置点关于参考位置点的经纬度偏差。由两个 12 比特的经度、纬度偏差值组成。
                    lon: -1124
                    lat: -1615
                }
                offsetV: -64    //垂直方向位置偏差 
            }
            accuracy: PositionConfidenceSet ::= {  //定义位置（经纬度和高程）的综合经度   定义设备的可行度，精准度。
                pos: 11 (a20cm)      经纬度的精准度，
                elevation: 10 (elev-000-50)       // 高度经纬度。
            }
            speed: 0  // 速度
            heading: 16559  //为车辆航向角，即为车头方向与正北方向的顺时针夹角。分辨率为 0.0125°。
            size: VehicleSize ::= {  //  车辆大小
                width: 100
                length: 100
                height: 40
            }
            vehicleClass: VehicleClassification ::= {  // 车辆类型   
                classification: 0
            }
        }
    }
}



typedef enum{
 MSG_VEHICLE    = 0,  //普通车辆
 MSG_PEDESTRIAN   = 1,  // 行人与动物闯入检测
 MSG_ILLEGAL_V1   = 2,  // 违章车辆1(违停)
 MSG_VISIBILITY   = 3,  // 白天能见度检测
 MSG_AVAILABLE_AREA  = 4,  // 可行驶区域检测
 MSG_ABNORMAL_CAR  = 5,  // 异常车辆检测(静止)
 MSG_ILLEGAL_V2   = 6,  // 违章车辆2(应急车道)
 MSG_TRAFFIC    = 7,  // 交通态势感知
 MSG_BACKWARD_DRIVING = 8,  // 逆向行驶告警
 MSG_ROAD_DANGER   = 9,  // 道路危险状况提醒(抛洒物)
 MSG_OBSTRUCTION   = 9,  // 道路危险状况提醒(障碍物)
 MSG_FIRE_SMOKE   = 10, // 隧道内火焰与烟雾预警
 MSG_PEDESTRIAN_CROSS = 11,  // 行人穿越预警
 MSG_ABNORMAL_CAR2  =12,
}MSG_ID;
```





# 二、字段说明

## 2.1 msgCnt	MsgCount	消息计数

【定义】 

发送方为自己发送的同类消息，依次进行编号。编号数值为 0 ～ 127。 当发送方开始发起某一类数据时，它可以随机选择起始编号，随后依次递增。发送方也可以在 

连续发送相同的数据帧时，选择使用相同的 MsgCount 消息编号。编号到达 127 后，则下一个回到 0。 

【ASN.1 代码】 

MsgCount ::= INTEGER (0..127)



## 2.2 id 编号

rsu id
OCTET STRING (SIZE(8))



## 2.3 participants：ParticipantList交通参与者列表

【定义】 
定义交通参与者列表。应用于RSM消息中，表示所有或部分RSU当前探测到的交通参与者信息。
【ASN.1 代码】
 ParticipantList ::= SEQUENCE (SIZE(1..16) OF ParticipantData



### SEQUENCE OF ParticipantData交通参与者的基本安全信息序列

【定义】
 定义交通参与者的基本安全信息。对应BSM消息，该参与者信息由RSU探测得到。

【ASN.1 代码】 

```json
ParticipantData ::= SEQUENCE{
ptcType ParticipantType, 

ptcld INTEGER(0..65535),
-- temporary ID set by RSU
-- 0 is RSU itself
-- 1..65535 represent participants detected by RSU 
source SourceType,
id OCTET STRING (SIZE8)OPTIONAL,
plateNo OCTET STRING(SIZE(16)OPTIONAL,
secMark DSecond, 
pos PositionOffsetLLV, 
accuracy PositionConfidenceSet, 
transmission TransmissionState OPTIONAL, 
speed Speed, 
heading Heading,
angle SteeringWheelAngle OPTIONAL,
motionCfd MotionConfidenceSet OPTiONAL,
accelSet AccelerationSet4Way OPTIONAL, 
size VehicleSize,
vehicdeClass VehicleClassification OPTIONAL,
...
}
```



#### 1. ptcType ParticipantType路侧单元检测到的交通参与者类型

【定义】 
路侧单元检测到的交通参与者类型。
【 ASN.1 代码】 

```json
ParticipantType ::= ENUMERATED{
unknown(0),--B0000 Unknown 
motor(1),-- B'0001 motor 
non-motor(2),--B'0010 non-motor
pedestrian(3),-- B'0011 pedestrian 
rsu(4),-- B'0100 rsu
...
}
```



#### 2. ptcld ptc编号

```json
ptcId INTEGER (0.65535),
-- temporary ID set by RSU
--0 is RSU itself 
--1.65535 represent participants detected by RSU
```



#### 3. source SourceType路侧交通参与者数据的检测器来源

```json
【定义】
定义路侧交通参与者数据的检测器来源。
【ASN.1 代码】
SourceType ::= ENUMERATED{ 
unknown(0),-- 0 Unknown 
selfinfo(1), --1 infomation from iself 
v2x(2),--2 v2x 
video(3), -- 3 video
microwaveRadar(4),--4 microwave radar 
loop(5),-- 5 lop
...
}
```



#### 4. id OCTET  

```json
STRING(SIZE8)OPTIONAL
```



#### 5. plateNoOCTET 

```json
STRING(SIZE(16)OPTIONAL
```



#### 6. secMark DSecond1分钟内的毫秒级时刻

```json
【定义】
定义1分钟内的毫秒级时刻。分辨率为1毫秒，有效范围是0～599。6000及以上表示未知或无效数值 
【ASN.1 代码】
DSecond ::= INTEGER (0..65535)
-- units of milliseconds
```



#### 7.  posOffset PositionOffsetLLV三维的相对位置

- offsetLL PositionOffsetLL经纬度偏差

```json
【定义】
经纬度偏差，用来描述一个坐标点的相对位置。提供了7种尺度的描述方式。
【ASN.1代码】
PositionOffsetLL ::= CHOICE {
--Locations with LL content Span at the equator when using a zoom of one: 

position-LL1 Position-LL-24B,
-- within +-22.634554 meters of the reference position 

position-LL2 Position-LL-28B,
-- within +-90.571389 meters of the reference position 

position-LL3 Position-LL-32B,
-- within+-362.31873 meters of the reference position 

position-LL4 Position-LL-36B,
--within+-01.449308 Kmeters of the reference position 

position-LL5 Position-LL-44B,
-- within+-23.189096 Kmeters of the referenceposition

position-LL6 Position-LL-48B,
--within+-92.756481 Kmeters of the reference position 

position-LatLon Position-LLmD-64b
--node is afull 32b Lat/Lon range
}
```

- - position-LL1 Position-LL-24B24比特相对经纬度位置

  - ```json
    【定义】
    24比特相对经纬度位置，表示当前位置点关于参考位置点的经纬度偏差。由两个12比特的经度、纬度偏差值组成。 
    【ASN.1 代码】
    Position-LL-24B ::= SEQUENCE {
    -- ranges of +- 0.0002047 degrees
    -- ranges of +-22.634554 meters at the equator 
    lon OffsetLL-B12, 
    lat OffsetLL-B12
    }
    ```

  - on OffsetLL-B12 12比特数值经纬度偏差

  - ```json
    【定义】
    12比特数值，表示当前位置点关于参考位置点的经纬度偏差。值得注意的是，根据纬度的不同，相同的经纬度偏差值对应的实际球面距离可能不同。关于参考点，向东或向北偏移，数值为正，反之为负。分辨率为1e-7°。
    【ASN.1 代码】
    OffsetLL-B12::=INTEGER(-2048..2047)
    -- A range of +-0.0002047 degrees
    --In LSB units of 0.1 microdegrees
    ```

  - lat OffsetLL-B12比特数值经纬度偏差

  - ```json
    【定义】
    12比特数值，表示当前位置点关于参考位置点的经纬度偏差。值得注意的是，根据纬度的不同，相同的经纬度偏差值对应的实际球面距离可能不同。关于参考点，向东或向北偏移，数值为正，反之为负。分辨率为1e-7°。
    【ASN.1 代码】
    OffsetLL-B12::=INTEGER(-2048..2047)
    -- A range of +-0.0002047 degrees
    --In LSB units of 0.1 microdegrees
    ```



- - position-LL2 Position-LL-28B28比特相对经纬度位置

  - ```json
    【定义】
    28比特相对经纬度位置，表示当前位置点关于参考位置点的经纬度偏差。由两个14比特的经度纬度偏差值组成。 
    【ASN.1 代码】
    Position-L-28B ::= SEQUENCE{
    -- ranges of +-0.0008191 degrees
    -- ranges of +-90.571389 meters at the equator 
    lon OffsetLL-B14, 
    lat OffsetLL-B14,
    }
    ```

  - lon OffsetLL-B14  14比特数值经纬度偏差

- ```json
  【定义】
  14比特数值，表示当前位置点关于参考位置点的经纬度偏差。值得注意的是，根据纬度的不同，相同的经纬度偏差值对应的实际球面距离可能不同。关于参考点，向东或向北偏移，数值为正，反之为负。分辨率为1e-7°。
    【ASN.1 代码】
    OffsetLL-B14 ::= INTEGER (-8192.8191)
    -- A range of +- 0.0008191 degrees
    -- In LSB units of 0.1 microdegrees
  ```

  - lat OffsetLL-B14 14比特数值经纬度偏差

  - ```json
    【定义】
    14比特数值，表示当前位置点关于参考位置点的经纬度偏差。值得注意的是，根据纬度的不同，相同的经纬度偏差值对应的实际球面距离可能不同。关于参考点，向东或向北偏移，数值为正，反之为负。分辨率为1e-7°。
    【ASN.1 代码】
    OffsetLL-B14 ::= INTEGER (-8192.8191)
    -- A range of +- 0.0008191 degrees
    -- In LSB units of 0.1 microdegrees
    ```

- - position-LL3 Position-LL-32B32比特相对经纬度位置

  - ```json
    【定义】
    32比特相对经纬度位置，表示当前位置点关于参考位置点的经纬度偏差。由两个16比特的经度、纬度偏差值组成。 
    【ASN.1代码】
    Position-LL-32B ::= SEQUENCE {
    -- ranges of +-0.0032767 degrees
    -- ranges of +-362.31873 meters at the equator 
    lon OffsetLL-B16, 
    lat OffsetLL-B16,
    }
    ```

  - lon OffsetLL-B16 16比特数值经纬度偏差

  - ```json
    【定义】
    16比特数值，表示当前位置点关于参考位置点的经纬度偏差。值得注意的是，根据纬度的不同，相同的经纬度偏差值对应的实际球面距离可能不同。关于参考点，向东或向北偏移，数值为正，反之为负。分辨率为1e-7°。
    【ASN.1代码】
    OffseLL-B16 ::= INTEGER (-32768..32767)
    -- A range of +- 0.0032767 degrees
    --In LSB units of 0.1 microdegrees
    ```

  - lat OffsetLL-B16 16比特数值经纬度偏差

  - ```json
    【定义】
    16比特数值，表示当前位置点关于参考位置点的经纬度偏差。值得注意的是，根据纬度的不同，相同的经纬度偏差值对应的实际球面距离可能不同。关于参考点，向东或向北偏移，数值为正，反之为负。分辨率为1e-7°。
    【ASN.1代码】
    OffseLL-B16 ::= INTEGER (-32768..32767)
    -- A range of +- 0.0032767 degrees
    --In LSB units of 0.1 microdegrees
    ```

- - position-LL4 Position-LL-36B36比特相对经纬度位置

  - ```json
    【定义】
    36比特相对经纬度位置，表示当前位置点关于参考位置点的经纬度偏差。由两个18比特的经度、纬度偏差值组成。 
    【ASN.1代码】
    Position-LL-36B ::= SEQUENCE {
    -- ranges of +- 0.0131071 degrees
    -- ranges of +-001.449308 Kmeters at the equator 
    lon OffsetLL-B18,
    lat OffsetLL-B18
    }
    ```

  - lon OffsetLL-B18  18比特数值经纬度偏差

  - ```json
    【定义】
    18比特数值，表示当前位置点关于参考位置点的经纬度偏差。值得注意的是，根据纬度的不同，相同的经纬度偏差值对应的实际球面距离可能不同。关于参考点，向东或向北偏移，数值为正，反之为负。分辨率为1e-7°。
    【ASN.1代码】
    OffsetLL-B18 ::= INTEGER (-131072..131071)
    -- A range of +-0.0131071 degrees
    -- In LSB units of 0.1 microdegrees
    ```

  - lat OffsetLL-B18  18比特数值经纬度偏差

  - ```json
    【定义】
    18比特数值，表示当前位置点关于参考位置点的经纬度偏差。值得注意的是，根据纬度的不同，相同的经纬度偏差值对应的实际球面距离可能不同。关于参考点，向东或向北偏移，数值为正，反之为负。分辨率为1e-7°。
    【ASN.1代码】
    OffsetLL-B18 ::= INTEGER (-131072..131071)
    -- A range of +-0.0131071 degrees
    -- In LSB units of 0.1 microdegrees
    ```

- - position-LL5 Position-LL-44B44比特相对经纬度位置

  - ```json
    【定义】
    44比特相对经纬度位置，表示当前位置点关于参考位置点的经纬度偏差。由两个22比特的经度、纬度偏差值组成。
    【ASN.1代码】
    Position-LL-44B ::= SEQUENCE {
    -- ranges of +- 0.2097151 degrees
    -- ranges of +- 23.189096 Kmeters at the equator 
    lon OffsetLL-B22, 
    lat OffsetLL-B22
    }
    ```

  - lon OffsetLL-B22  22比特数值经纬度偏差

  - ```json
    【定义】
    22比特数值，表示当前位置点关于参考位置点的经纬度偏差。值得注意的是，根据纬度的不同，相同的经纬度偏差值对应的实际球面距离可能不同。关于参考点，向东或向北偏移，数值为正，反之为负。分辨率为1e-7°。
    【ASN.1 代码】
    OffsetLL-B22:= INTEGER (-2097152..2097151)
    --A range of +- 0.2097151 degrees 
    --In LSB units of 0.1 microdegrees
    ```

  - lat OffsetLL-B22  22比特数值经纬度偏差

  - ```json
    【定义】
    22比特数值，表示当前位置点关于参考位置点的经纬度偏差。值得注意的是，根据纬度的不同，相同的经纬度偏差值对应的实际球面距离可能不同。关于参考点，向东或向北偏移，数值为正，反之为负。分辨率为1e-7°。
    【ASN.1 代码】
    OffsetLL-B22:= INTEGER (-2097152..2097151)
    --A range of +- 0.2097151 degrees 
    --In LSB units of 0.1 microdegrees
    ```

- - position-LL6 Position-LL-48B48比特相对经纬度位置

  - ```json
    【定义】
    48比特相对经纬度位置，表示当前位置点关于参考位置点的经纬度偏差。由两个24比特的经度、纬度偏差值组成。
    【ASN.1 代码】
    Position-LL-48B ::= SEQUENCE {
    -- ranges of +- 0.8388607 degrees
    -- ranges of +-92.756481 Kmeters at the equator 
    lon OffsetLL-B24, 
    lat OffsetLL-B24
    }
    ```

  - lon OffsetLL-B24  24比特数值经纬度偏差

- ```json
  【定义】
  24比特数值，表示当前位置点关于参考位置点的经纬度偏差。值得注意的是，根据纬度的不同，相同的经纬度偏差值对应的实际球面距离可能不同。关于参考点，向东或向北偏移，数值为正，反之为负。分辨率为 1e-7°。
    【ASN.1 代码】
    OffsetLL-B24 ::= INTEGER (-838608..8388607)
    -- A range of +-0.8388607 degrees
    -- In LSB units of 0.1 microdegrees
  ```

  - lat OffsetLL-B24 24比特数值经纬度偏差

  - ```json
    【定义】
    24比特数值，表示当前位置点关于参考位置点的经纬度偏差。值得注意的是，根据纬度的不同，相同的经纬度偏差值对应的实际球面距离可能不同。关于参考点，向东或向北偏移，数值为正，反之为负。分辨率为 1e-7°。
    【ASN.1 代码】
    OffsetLL-B24 ::= INTEGER (-838608..8388607)
    -- A range of +-0.8388607 degrees
    -- In LSB units of 0.1 microdegrees
    ```

- - position-LatLon Position-LLmD-64b 64比特经纬度位置

  - ```json
    【定义】
    64比特经纬度位置。该尺度采用了真实经纬度数据进行描述，非相对位置。
    【ASN.1代码】
    Position-LLmD-64b ::= SEQUENCE {
    --a full 32b Lat/Lon range 
    lon Longitude, 
    lat Latitude
    }
    ```

  - lon Longitude经度数值

- ```json
  【定义】
  定义经度数值。东经为正，西经为负。分辨率为1e-7°。
    【ASN.1 代码】
    Longitude ::= INTEGER(-17999999..18000001)
    --ISB = 1/10 micro degree
    --Providing a range of plus-minus 180 degrees
  ```

  - lat Latitude纬度数值

  - ```json
    【定义】
    定义纬度数值，北纬为正，南纬为负。分辨率1e-7°。
    【ASN.1 代码】
    Latitude ::= INTEGER(-900000.9000001)
    --LSB= 1/10 micro degree
    --Providing a range of plus-minus 90 degrees
    ```



-  offsetV VerticalOffset OPTIONAL垂直方向位置偏差

```json
【定义】
定义垂直方向位置偏差。提供了7种尺度范围的偏差表示方式。【ASN.1 代码】 
VerticalOffset ::= CHOICE {
--Vertical Offset
--All below in steps of 10cm above or below the reference ellipsoid 
offsetl VertOffset-B07,-- with arange of +-6.3 meters vertical
offset2 VertOffset-B08,-- with arange of +-12.7meters vertical
offset3 VertOffset-B09,-- with arange of+-25.5 meters vertical 
offset4 VertOffset-B10,--with a range of +-51.1 meters vertical
offset5 VertOffset-B11,-- with a range of +-102.3meters vertical 
offset6 VertOffset-B12,-- with a range of+-204.7meters vertical
 elevation Elevation-- with a range of-409.5 to+6143.9 meters
}
```



#### 8. accuracy PositionConfidenceSet位置（经纬度和高程）的综合精度

【定义】
 定义位置（经纬度和高程）的综合精度。
【ASN.1 代码】 

```json
PositionConfidenceSet ::= SEQUENCE {
pos PositionConfidence,	
--for both horizontal directions 
elevation ElevationConfidence OPTIONAL
}
```

- pos PositionConfidence95%置信水平的车辆位置精度

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

- elevation ElevationConfidence95%置信水平的车辆高程精度

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

#### 9. transmission TransmissionState OPTIONAL定义车辆档位状态

```json
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



#### 10. speed Speed车速大小

```json
【定义】
车速大小。分辨率为0.02m/s。数值8191表示无效数值。
【ASN.1 代码】
Speed ::=INTEGER(0..8191)
-- Units of 0.02 m/s
--The value 8191 indicates that
-- speed is unavailable
```

#### 11. heading Heading车辆航向角

```json
【定义】
为车辆航向角，即为车头方向与正北方向的顺时针夹角。分辨率为0.0125°。
【ASN.1 代码】
Heading := INTEGER (0.28800)
-- ILSB of 0.0125 degrees
-- A range of O to 359.9875 degrees
```

#### 12. angle SteeringWheelAngle OPTIONAL 方向盘转角

```json
【定义】
方向盘转角。向右为正，向左为负。分辨率为1.5°。数值127为无效数值。
【ASN.1 代码】
SteeringWheelAngle ::=INTEGER (-126..127)
--LSB units of 1.5 degrees,a range of-189 to+189 degrees
-- +001 = +1.5 deg
-- -126=-189 deg and beyond
--+126 =+189 deg and beyond
-- +127 to be used for unavailable
```

#### 13. motionCfd MotionConfidenceSet OPTIONAL车辆运行状态的精度

```json
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

```json
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

```json
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

```json
【定义】
数值描述了95%置信水平的方向盘转角精度。该精度理论上只考虑了当前方向盘转角传感器的误差。但当系统能够自动检测错误并修正时，相应的精度数值也应该提高。
【ASN.1代码】
SteeringWheelAngleConfidence ::= ENUMERATED { 
unavailable (0),-- B'00 Not Equipped with Wheel angle 
-- or Wheel angle status is unavailable 
prec2deg (1),-- B'01 2 degrees 
prec1deg (2), -- B'10 1 degre e
prec0-02deg(3), --B'11 0.02 degrees
}-- Encoded as a 2bit value
```



#### 14.  size VehicleSize车辆尺寸大小

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

- width VehicleWidth车辆车身宽度

```json
【定义】
定义车辆车身宽度。分辨率为1cm。数值0表示无效数据。【ASN.1 代码】 
VehicleWidth ::= INTEGER (0..1023)-
--LSB units are 1cm with a range of>10meters
```

-  length VehicleLength车辆车身长度

```json
【定义】
定义车辆车身长度。分辨率为1cm。数值0表示无效数据。【ASN.1 代码】 
VehicleLength ::= INTEGER(0..4095)
--LSB units of 1cm with a range of >40meters
```

-  height VehicleHeight OPTIONAL车辆车身高度

```json
【定义】
定义车辆车身高度。分辨率为5cm。数值0表示无效数据。【ASN.1代码】 
VehicleHeight ::= INTEGER 0.127)
--LSB units of 5 cm,range to 6.35 meters	
```

#### 15. accelSet AccelerationSet4Way车辆四轴加速度

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

- long Acceleration加速度

```json
【定义】
定义车辆加速度。分辨率为0.01m/s²，数值2001为无效数值。【ASN.1 代码】 
Acceleration ::= INTEGER (-2000..2001)
--LSB units are 0.01 m/s^2
--the value 2000 shall be used for values greater than 2000
-- the value -2000 shall be used for values less than-2000
--a value of 2001 shall be used for Unavailable
```

- lat Acceleration加速度

```json
【定义】
定义车辆加速度。分辨率为0.01m/s²，数值2001为无效数值。【ASN.1 代码】 
Acceleration ::= INTEGER (-2000..2001)
--LSB units are 0.01 m/s^2
--the value 2000 shall be used for values greater than 2000
-- the value -2000 shall be used for values less than-2000
--a value of 2001 shall be used for Unavailable
```

-  vert VerticalAccelerationZ轴方向的加速度

```json
【定义】
定义Z轴方向的加速度大小，Z轴方向竖直向下，沿着Z轴方向为正。分辨率为0.02g，g为重力加速度典型值 9.80665 m/s32。【ASN.1 代码】
VerticalAcceleration ::= INTEGER(-127..127)
-- LSB units of 0.02 G steps over-2.52 to +2.54 G
--The value +127 shall be used for ranges >= 2.54 G
--The value -126 shall be used for ranges <= 2.52 G
--The value -127 shall be used for unavailable
```

- yaw YawRate 车辆横摆角速度

```json
【定义】
车辆横摆角速度。指汽车绕垂直轴的偏转，该偏转的大小代表汽车的稳定程度。如果偏转角速度达到一个阈值，说明汽车处于发生测滑或者甩尾等的危险工况。顺时针旋转为正，逆时针为负。数据分辨率为 0.01° /s。
【ASN.1 代码】
YawRate ::= INTEGER (-32767..32767)
-- LSB units of 0.01 degrees per second (signed)
```

#### 16. vehicleClass VehicleClassification车辆的分类

```json
【定义】
定义车辆的分类，可从各个维度对车辆类型进行定义。目前仅有车辆基本类型一项。
【ASN.1 代码】
VehicleClassification ::= SEQUENCE {
classification BasicVehicleClass,
...
}
```

- classification BasicVehicleClass车辆基本类型

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



## 2.4 refPos（3D） reference position（Position3D）参考位置

【定义】 
三维的坐标位置，包括经纬度和高程。
【ASN.1 代码】 

```json
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

【定义】 
定义纬度数值，北纬为正，南纬为负。分辨率1e-7°。
【ASN.1 代码】

```json
Latitude:= INTEGER(-900000.9000001)
--LSB= 1/10 micro degree
--Providing a range of plus-minus 90 degrees
```



### long Longitude经度

【定义】
 定义经度数值。东经为正，西经为负。分辨率为1e-7°。
【ASN.1 代码】

```json
Longitude ::= INTEGER(-17999999..180000001)
-- ISB= 1/10 micro degree 
-- Providing a range of plus-minus 180 degrees
```



### elevation Elevation OPTIONAL 海拔

【定义】
 定义车辆海拔高程。分辨率为0.1米。数值-4096 表示无效数值。

【ASN.1 代码】

```json
Elevation ::= INTEGER (-4096..61439)
-- In units of 10cm steps above or below the reference ellipsoid
-- Providing a range of-409.5 to＋6143.9 meters
-- The value-4096 shall be used when Unknown is to be sent
```



```json
RoadsideSafetyMessage ::= {
    msgCnt: 111    // 计数器   判断数据连续性
    id: 72 73 75 30 30 30 30 33      //RSU 设备编号
    refPos: Position3D ::= {     //--交通警报位置（交通标志或事件)      三维坐标位置
        lat: 281132739
        long: 1128669787
        elevation: 553
    }
    participants: ParticipantList ::= {  //交通参与者列表，应用于RSM 消息中 ，表示所有或部分RSU当前探测到的交通参与者信息
        ParticipantData ::= {  //定义交通参与者的基本安全信息。对应 BSM 消息，该参与者信息由 RSU 探测得到
            ptcType: 3 (pedestrian)     // 参与者事务类型  车 ，行人，根据国标来判断的。
            ptcId: 1     //   场景类型     见微信王泽涛   行人闯入 
            source: 3 (video)  //定义路侧交通参与者数据的检测器来源
            id: 参与者ID	
            secMark: 9732    // //定义毫米级时刻   
            pos: PositionOffsetLLV ::= {   //定义三维的相对位置
                offsetLL: Position-LL-24B ::= {  //24 比特相对经纬度位置，表示当前位置点关于参考位置点的经纬度偏差。由两个 12 比特的经度、纬度偏差值组成。
                    lon: -1124
                    lat: -1615
                }
                offsetV: -64    //垂直方向位置偏差 
            }
            accuracy: PositionConfidenceSet ::= {  //定义位置（经纬度和高程）的综合经度   定义设备的可行度，精准度。
                pos: 11 (a20cm)      经纬度的精准度，
                elevation: 10 (elev-000-50)       // 高度经纬度。
            }
            speed: 0  // 速度
            heading: 16559  //为车辆航向角，即为车头方向与正北方向的顺时针夹角。分辨率为 0.0125°。
            size: VehicleSize ::= {  //  车辆大小
                width: 100
                length: 100
                height: 40
            }
            vehicleClass: VehicleClassification ::= {  // 车辆类型   
                classification: 0
            }
        }
    }
}
```

```java
typedef enum{
 MSG_VEHICLE    = 0,  //普通车辆
 MSG_PEDESTRIAN   = 1,  // 行人与动物闯入检测
 MSG_ILLEGAL_V1   = 2,  // 违章车辆1(违停)
 MSG_VISIBILITY   = 3,  // 白天能见度检测
 MSG_AVAILABLE_AREA  = 4,  // 可行驶区域检测
 MSG_ABNORMAL_CAR  = 5,  // 异常车辆检测(静止)
 MSG_ILLEGAL_V2   = 6,  // 违章车辆2(应急车道)
 MSG_TRAFFIC    = 7,  // 交通态势感知
 MSG_BACKWARD_DRIVING = 8,  // 逆向行驶告警
 MSG_ROAD_DANGER   = 9,  // 道路危险状况提醒(抛洒物)
 MSG_OBSTRUCTION   = 9,  // 道路危险状况提醒(障碍物)
 MSG_FIRE_SMOKE   = 10, // 隧道内火焰与烟雾预警
 MSG_PEDESTRIAN_CROSS = 11,  // 行人穿越预警
 MSG_ABNORMAL_CAR2  =12,
}MSG_ID;
```