本文档旨在说明SO库应用与MEC硬件设备交互的逻辑。

# 交互逻辑

## MEC -> SO

MEC主体软件向so库传递`MECData`数据结构，包含以下信息：

- MEC设备本身的ID、所在位置和运行状态；
- MEC所连接的所有外设的类型、ID、位置、检测范围/广播范围（如适用）、实时运行状态。

`MECData`数据结构包含的信息和具体定义见[附录对应内容](http://108.61.183.243/project/3/post/26#MECData数据结构)。

MECData数据结构传递到so库的时机包括：

- so库初始化；
- MEC设备或连接外设的信息发生变化，需要通知so库。

其他时候，so库不会收到`MECData`数据结构输入。如需要与外设交互，为了实现上述逻辑，so库对应json配置文件中，应当在初始化和业务循环两个阶段均声明`MECData`数据结构输入。

## SO -> MEC

SO输出数据，需要通过`Get()`函数中的`string_value`参数指明该结构体应当被传输到的设备ID，可以传递给MEC设备本身，也可以传递到MEC连接的硬件外设。
设备ID由MEC自动分配，SO库内部直接读取并利用即可。设备ID编号规则见[附录对应内容](http://108.61.183.243/project/3/post/26#设备ID规则)。
【例】若需要向车辆广播RSI消息，则应当把so库生成的RSI结构体发送到ID为`"RSU_0"`的外设。

# 附录

## 设备ID规则

设备ID为字符串类型，格式：`[设备类别前缀]+"_"+[十进制数字]`。

| 设备类别         | 前缀        |
| :--------------- | :---------- |
| 本地MEC          | `"LOCAL"`   |
| 其他MEC          | `"MEC"`     |
| RSU              | `"RSU"`     |
| 雷达             | `"RADAR"`   |
| 视频             | `"VIDEO"`   |
| 可变情报板       | `"VMS"`     |
| 信号控制机       | `"SIGNAL"`  |
| 云平台           | `"CLOUD"`   |
| 本地设备管理后台 | `"CONSOLE"` |
| 其他             | `"OTHERS"`  |

数字部分，由MEC主体程序根据外设注册先后顺序自动分配。

## MECData数据结构

- `MECData.fbs`：`MECData`数据结构根节点。

```
include "Position3D.fbs";
include "DeviceAbnormal.fbs";
include "DeviceInfo.fbs";
namespace MECData;
table MSG_MECInfo {
id:string;                                         //MEC id
pos:DF_Position3D;
status:DF_DeviceAbnormal;
deviceManage:[DF_DeviceInfo];
}
root_type MSG_MECInfo;
```

- `DeviceInfo.fbs`：MEC外设基本信息。

```
include "Position3D.fbs";
include "DeviceAbnormal.fbs";
namespace MECData;
table DF_DeviceInfo {
	id:string;                //other device id, eg: radar, video, rsu...
    deviceType:ubyte; 
    pos:DF_Position3D;
    direction:ubyte;          //normal direction, units of degree
    deviceRange:ubyte;        //units of m
    status:DF_DeviceAbnormal;
}
```

- `DeviceAbnormal.fbs`: MEC或者外设的实时运行状态和故障信息。

```
namespace MECData;
table DF_DeviceAbnormal {
	state:ubyte;
	abnormalType:ubyte;
	descrption:string;
}
```

- `Position3D.fbs`: 设备所在经纬度和海拔。

```
namespace MECData;
struct DF_Position3D {
	lat:int;        //Latitude,LSB = 1/10 micro degree,Providing a range of plus-minus 90 degrees
    lon:int;        //Longitude,LSB = 1/10 micro degree,Providing a range of plus-minus 180 degrees
    ele:short;      //Elevation,units of 10 cm steps above or below the reference elli psoid,Provid ing a range of - 409.5 to + 6143.9 meters,The value -4 096 shall be used when Unknown is to be sent
}
```

数据结构中类型与状态等可能取值见[相关定义](http://108.61.183.243/project/3/post/26#外设类别、运行状态和异常类型等定义)。

## 外设类别、运行状态和异常类型等定义

摘自`mec_lib.h`：

```
// 设备管理
#define MAX_DEV_ID_SIZE 0x20u  // 设备ID字符串最大长度
// 设备ID类别
#define DEV_LOCAL 0x0u  // MEC自身
#define DEV_MEC 0x1u    // 其它MEC
#define DEV_RSU 0x2u
#define DEV_RADAR 0x3u
#define DEV_VIDEO 0x4u
#define DEV_VMS 0x5u
#define DEV_SIGNAL 0x6u
#define DEV_CLOUD 0x7u
#define DEV_CONSOLE 0xfeu   // 预留本机管理后台
#define DEV_OTHERS 0xffu
// 设备运行状态
#define DEV_STATE_OK 0x0u
#define DEV_STATE_OFF 0x1u  // 电源断开
#define DEV_STATE_ABNORMAL 0x2u // 设备运行状态异常
// 设备异常类型
#define DEV_AB_OK 0x0u
#define DEV_AB_POWER 0x1u   // 电源异常或断开
#define DEV_AB_NETWORK 0x2u // 网络连接问题
#define DEV_AB_ENV 0x3u     // 运行环境异常
#define DEV_AB_FUNC 0x4u    // 设备功能异常
#define DEV_AB_INTERR 0X5u  // 设备内部错误
#define DEV_AB_UNKNOWN 0xffu    // 未知类型
```