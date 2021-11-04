# 一、业务数据接口要求

业务数据接口用于中心子系统与 RSU 之间下发和上报的 V2X 业务数据，包括：RSU 信息/MAP 数据/RSI数据的上报和确认、RSU 信息上报确认、RSU 业务配置/MAP 数据/RSI 数据的下发和确认、BSM 数据的上报、RSM 数据/SpaT 数据的上报和下发。MAP、RSI、BSM、RSM、SPAT 等消息的定义遵从标准 YDT 3709-2020基于 LTE 的车联网无线通信技术 消息层技术要求。

## 1.1 RSU信息上报

### 1.1.1 基本介绍和要求

RSU 向中心子系统上报自身的经纬度位置和配置参数及运行信息。

消息发送频率： RSU 启动时和参数发生变化时上报。

#### 1. 消息集

RSU 信息上报的消息 V2X.RSU.INFO.UP 中各数据元素如表 1 所示。

| 名称      | 是否必选 | 类型     | 说明                                      |
| --------- | -------- | -------- | ----------------------------------------- |
| rsuId     | 是       | String   | RSU的标识                                 |
| rsuEsn    | 是       | String   | RSU的序列号，用于唯一标识一个RSU          |
| rsuName   | 是       | String   | RSU的名称                                 |
| version   | 是       | String   | 接口协议版本                              |
| rsuStatus | 是       | String   | RSU状态正常或异常                         |
| location  | 是       | Location | 位置信息，包含经纬度数据                  |
| config    | 是       | Config   | RSU的配置数据                             |
| ack       | 否       | Boolean  | 是否需要确认，TRUE需要，不带或FALSE不需要 |
| seqNum    | 否       | Integer  | 当需要确认时填写，用于匹配响应消息        |

#### 2. 数据帧

RSU信息上报的消息V2X.RSU.INFO.UP中各数据元素的数据类型如表2-表10所示。

##### DF_Location

| 名称 | 是否必选 | 类型  | 说明                      |
| ---- | -------- | ----- | ------------------------- |
| lon  | 是       | Float | 经度，无效值：180.0000001 |
| lat  | 是       | Float | 纬度，无效值：90.0000001  |

##### DF_Config

| 名称       | 是否必选 | 类型       | 说明     |
| ---------- | -------- | ---------- | -------- |
| mapConfig  | 是       | MapConfig  | MAP配置  |
| bsmConfig  | 是       | BsmConfig  | BSM配置  |
| rsiConfig  | 是       | RsiConfig  | RSI配置  |
| spatConfig | 是       | SpatConfig | SPAT配置 |
| rsmConfig  | 是       | RsmConfig  | RSM配置  |

DF_MapConfig

| 名称     | 是否必选 | 类型   | 说明                       |
| -------- | -------- | ------ | -------------------------- |
| mapSlice | 是       | String | MAP切片                    |
| eTag     | 是       | String | MAP切片ETag+表示切片的版本 |

DF_BsmConfig

| 名称             | 是否必选 | 类型             | 说明                                                         |
| ---------------- | -------- | ---------------- | ------------------------------------------------------------ |
| sampleMpde       | 是       | String           | "ByAll"：全局采样；"ByID"：RSU解析出车ID，按ID进行采样，保证均匀 |
| sampleRate       | 是       | Integer(0~10000) | 采样率：单位：条/秒，按照该采样率进行转发，0表示不需要转发，当达到转发上限(upLimit)时，则自动降低采样率。 |
| actualSampleRate | 是       | Integer(0~10000) | 实际采样率，当达到upLimit定义的转发上限时，RSU自动降低采样率，此参数表示当前RSU实际的采样率。 |
| upLimit          | 是       | Integer(0~10000) | 上行转发上限，中心子系统通过"RSU配置下发"决定，RSU通过该消息表示每秒最多发送多少条消息，0表示不需要发。 |
| upFilters        | 否       | List<Filter>     | 上报的BSM的过滤条件，多个filter之间是"或"的关系，不带表示不过滤。同一个filter之间是“与”的关系，比如：filters:[{"id":1},{"id":2}]，表示只上报1和2的BSM消息。 |

DF_RsiConfig

| 名称      | 是否必选 | 类型         | 说明                                                         |
| --------- | -------- | ------------ | ------------------------------------------------------------ |
| maxRsiNum | 是       | Integer      | RSU同时支持的最大RSI数量，RSU根据自己的能力决定，通过该参数通知中心子系统要控制不要超过 |
| curRsiNum | 是       | Integer      | 当前RSU上实际广播的RSI消息数量                               |
| downRsis  | 是       | List<Rsi>    | 需要下发的RSI消息列表，中心子系统通过“RSI数据下发”配置，该参数用于中心子系统校验。 |
| upFilters | 否       | List<Filter> | 上报的RSI的过滤条件，多个filter之间是或关系，不带表示不过滤。比如：filters：[{"1":"15"}]，表示只上报id为15的RSI消息。 |

DF_Rsi

| 名称    | 是否必选 | 类型   | 说明                                                         |
| ------- | -------- | ------ | ------------------------------------------------------------ |
| alertID | 是       | String | 中心子系统下发的事件唯一ID                                   |
| eTag    | 是       | String | 事件ID对应的eTag，由中心子系统确定，用于校验、匹配修改确认的最新版本。 |

DF_SpatConfig

| 名称      | 是否必选 | 类型         | 说明                                                         |
| --------- | -------- | ------------ | ------------------------------------------------------------ |
| upLimit   | 是       | Integer      | 上行转发上限，中心子系统提供，每秒最多发送多少条消息，0表示不需要发，-1表示不限制。 |
| downLimit | 是       | Integer      | 下行转发上限，RSU提供，每秒最多发送多少条消息，0表示不需要发吗，-1表示不限制。 |
| upFilters | 否       | List<Filter> | 上报的SPAT的过滤条件，中心子系统提供，多个filter之间是或关系，不带表示不过滤。比如：filter：["intersectionId":"1"]，表示只上报intersectionId为1的SPAT消息。 |

DF_RsmConfig

| 名称      | 是否必选 | 类型         | 说明                                                         |
| --------- | -------- | ------------ | ------------------------------------------------------------ |
| upLimit   | 是       | Integer      | 上行转发上限，中心子系统提供，每秒最多发送多少条消息，0表示不需要发，-1表示不限制。 |
| downLimit | 是       | Integer      | 下行转发上限，RSU提供，每秒最多发送多少条消息，0表示不需要发吗，-1表示不限制。 |
| upFilters | 否       | List<Filter> | 上报的RSM的过滤条件，多个filter之间是或关系，不带表示不过滤，同一个filter之间是“关系”。比如：filters：[{"ptcType":"3"},{“source“：”3“}]，表示只上报ptcType为3且source为3的RSM消息。 |

DF_Filter

| 名称        | 是否必选 | 类型 | 说明                   |
| ----------- | -------- | ---- | ---------------------- |
| {fidldName} |          |      | 过滤字段，可携带多个。 |

## 1.2 RSU信息上报确认

### 1.2.1 基本介绍和要求

中心子系统收到 RSU 上报自身经纬度位置和配置参数的确认响应消息。

消息发送频率：收到上报消息后发送一次确认消息。

### 1.2.2 消息集

V2X.RSU.INFO.UP.ACK。

## 1.3 RSU业务配置下发

### 1.3.1 基本介绍和要求

中心子系统向 RSU 下发消息配置参数，包括对 BSM、RSI、SpaT、RSM 和 MAP 消息的配置。根据该配置，确定 RSU 向中心子系统发送 BSM、RSI、SpaT、RSM 和 MAP 的规则。

消息发送频率：中心子系统对 RSU 配置时下发消息。

### 1.3.2 消息集

RSU 业务配置下发的消息 V2X.RSU.CONFIG.DOWN 中各数据元素如表 11 所示。

| 名称       | 是否必选 | 类型       | 说明                                      |
| ---------- | -------- | ---------- | ----------------------------------------- |
| bsmConfig  | 是       | BsmConfig  | BSM配置                                   |
| rsiConfig  | 是       | RsiConfig  | RSI配置                                   |
| spatConfig | 是       | SpatConfig | SPAT配置                                  |
| rsmConfig  | 是       | RsmConfig  | RSM配置                                   |
| mapConfig  | 是       | MapConfig  | MAP配置                                   |
| ack        | 否       | boolean    | 是否需要确认，true需要，不带或false不需要 |
| seqNum     | 否       | String     | 当需要确认时，用于匹配响应                |

### 1.3.3 数据帧

RSU 业务配置下发的消息 V2X.RSU.CONFIG.DOWN 中各数据元素的数据类型如表 12-表 16 所示。