[TOC]

# 一、RSI—交通事件消息以及交通标志牌信息

```json
{
    "_id" : "5f9fcc925b757b70ecc2cb7d", //希迪自定义消息编号 ，无具体实际意义
    "msgCnt" : 0,   // 计数器，判断数据连续性， 0~127  
    "timeStamp" : null,  //本条消息时间搓 毫秒级
    "id" : "Q0RSMDAwNjg", //RSU  编号  指谁发送的
    "rsiId" : 0,  //RSI消息ID
    "alertType" : 90, //交通标志
    "description" : "d<",  //交通标志描述  ，等于0  文本描述 
    "priority" : null, //表示消息优先级。数值长度占 8 位，其中低五位为 0，为无效位，高三位为有效数据位。数值有效范围是 B00000000 到 B11100000，分别表示 8 档由低到高的优先级
    "refPos" : { //--交通警报位置（交通标志或事件)      三维坐标位置
        "lat" : 281120410,
        "long_" : 1128662238,
        "elevation" : null    //高度
    },
    "alertPath" : [  //圆形范围的半径大小
        {
            "offsetLL" : {
                "choiceID" : 2,  选择LL几， 是一个联合体，只会有一个。
                "position_LL1" : null,
                "position_LL2" : null,
                "position_LL3" : {
                    "lon" : 14839,
                    "lat" : 24381
                },
                "position_LL4" : null,
                "position_LL5" : null,
                "position_LL6" : null,
                "position_LatLon" : null  //绝对定位
            },
            "offsetV" : null    海拔。
        }, 
        {
            "offsetLL" : {
                "choiceID" : 2,
                "position_LL1" : null,
                "position_LL2" : null,
                "position_LL3" : {
                    "lon" : 6280,
                    "lat" : 10332
                },
                "position_LL4" : null,
                "position_LL5" : null,
                "position_LL6" : null,
                "position_LatLon" : null
            },
            "offsetV" : null
        }, 
        {
            "offsetLL" : {
                "choiceID" : 0,
                "position_LL1" : {
                    "lon" : -30,
                    "lat" : -50
                },
                "position_LL2" : null,
                "position_LL3" : null,
                "position_LL4" : null,
                "position_LL5" : null,
                "position_LL6" : null,
                "position_LatLon" : null
            },
            "offsetV" : null
        }
    ],
    "alertRadius" : 101   告警路径的宽度 半径（路的一半宽度）
}
```

# 二、字段说明

## 2.1 alertRadius Radius半径

```json
【定义】
表示一个特定圆形范围的半径大小，如一个交通事件基于圆心参考位置点的作用范围。数值主要用于 RSA 消息。分辨率为 10 cm。
【ASN.1代码】
Radius ::= INTEGER (0..1024)
-- Radius of roadside alert 
-- Unit is 0.1m
```

## 2.2 msgCnt	MsgCount 消息计数

```json
【定义】 
发送方为自己发送的同类消息，依次进行编号。编号数值为 0 ～ 127。 当发送方开始发起某一类数据时，它可以随机选择起始编号，随后依次递增。发送方也可以在 
连续发送相同的数据帧时，选择使用相同的 MsgCount 消息编号。编号到达 127 后，则下一个回到 0。 
【ASN.1 代码】 
MsgCount ::= INTEGER (0..127)
```

## 2.3 timeStamp	MinuteOfTheYear OPTIONAL时间标志

```json
【定义】
数值用来表示当前年份，已经过去的总分钟数（UTC 时间）。分辨率为1 分钟。该数值配合
DSecond 数值，则可表示全年已过去的总毫秒数。
【ASN.1 代码】
MinuteOfTheYear ::= INTEGER (0..527040)
-- the value 527040 shall be used for invalid
```

## 2.4 id 编号

```json
rsu id
OCTET STRING (SIZE(8))
```

## 2.5 rsiId 路侧id

```json
INTEGER (0..255)
```

## 2.6 refPos（3D）

 reference position（Position3D）参考位置

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

## 2.7 priority Priority OPTIONAL优先级

```json
【定义】
表示消息优先级。数值长度占8位，其中低五位为0，为无效位，高三位为有效数据位。数值有效范围是B000到 B11000，分别表示8档由低到高的优先级。
【ASN.1代码】
Priority ::= OCTET STRING (SIZE(1))
--The lower five bits are reserved and shall be set to zero
--Value from B00000 to B110000 represents the lowest to the highest level
```

## 2.8 alertType AlertType警示类型

```json
【定义】
定义路侧警示信息RSA的类型。数值0表示文本描述信息。大于0的数值表示交通标志标牌信息，内容参照 GB 5768。 
【ASN.1 代码】
AlertType ::= INTEGER (0..6535)
-- Text message warning =0
--Traffic signs according to China GB5768 
--Danger = 37 
-- Rockfall = 15 
-- SharpTurn =2 
--UnderConstruction=38 
--Slippy = 17 
--Tunnel=21
```

## 2.9 alertPath PathPointList路径位置点列表

```json
【定义】
定义RSA消息中，消息作用范围的车辆行进轨迹区段。该区段由有序位置点列组成，排列顺序与车辆行进方向一致。
【ASN.1 代码】
PathPointList ::= SEQUENCE (SIZE2.32)) OF PositionOffsetLLV 
-- Path point lis for RSA message
```

###  SEQUENCE OF PositionOffsetLLV三维的相对位置

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

## 2.10 description IA5String(SIZE(1..256))OPTIONAL描述

```json
 IA5String(SIZE(1..256))OPTIONAL
```