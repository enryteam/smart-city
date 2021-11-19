## 一、V2X MAP资源管理

### 1.1 获取多个V2X MAP资源

**功能介绍**

获取多个V2X MAP资源

**URI**

GET /v1/{project_id}/nodes

**响应参数**

**状态码：** **200**

![image-20211119160351337](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160351337.png)

![image-20211119160415904](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160415904.png)

![image-20211119160435184](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160435184.png)

![image-20211119160453015](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160453015.png)

![image-20211119160504495](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160504495.png)

![image-20211119160516664](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160516664.png)

![image-20211119160532648](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160532648.png)

![image-20211119160544936](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160544936.png)

![image-20211119160558576](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160558576.png)

![image-20211119160610808](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160610808.png)

![image-20211119160624808](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160624808.png)

![image-20211119160634224](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160634224.png)

![image-20211119160647888](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160647888.png)

**请求示例**

```
GET https://{endpoint}/v1/{project_id}/nodes
```

### 1.2 获取单个V2X  MAP节点信息

**功能介绍**

获取单个V2X MAP节点信息

**URI**

GET /v1/{project_id}/nodes/{global_node_id}

**响应参数**

**状态码：** **200**

![image-20211119160743279](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160743279.png)

![image-20211119160752600](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160752600.png)

![image-20211119160806591](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160806591.png)

![image-20211119160816401](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160816401.png)

![image-20211119160839191](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160839191.png)

![image-20211119160920479](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160920479.png)

![image-20211119160956590](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119160956590.png)

![image-20211119161019576](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161019576.png)

![image-20211119161034120](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161034120.png)

![image-20211119161047913](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161047913.png)

![image-20211119161100904](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161100904.png)

![image-20211119161113055](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161113055.png)

![image-20211119161125728](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119161125728.png)

**请求示例**

```
GET https://{endpoint}/v1/{project_id}/nodes/{global_node_id}
```

## 二、V2X MAPDTO 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

![image-20211119141345583](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119141345583.png)

### 1.1MAPSource 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119141416769](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119141416769.png)

### 1.2 NodeReferenceId 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119141453735](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119141453735.png)

### 1.3 MAPLocation 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119141514583](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119141514583.png)

### 1.4 Link 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119141543129](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119141543129.png)

### 1.5 RegulatorySpeedLimit 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119141640937](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119141640937.png)

### 1.6 Movement 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119141703384](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119141703384.png)

### 1.7 Lane 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119141741352](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119141741352.png)

### 1.8 LaneAttributes 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119141816118](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119141816118.png)

### 1.9 AllowedManeuvers 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119141903928](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119141903928.png)

### 1.10 ConnectionTo 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119141926968](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119141926968.png)

### 1.11 LaneSharingStatus 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119141948145](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119141948145.png)

### 1.12 LaneTypeAttributes 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119142009353](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119142009353.png)

### 1.13 LaneAttributesVehicle 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119142047562](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119142047562.png)

### 1.14 LaneAttributesCrosswalk 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119142128232](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119142128232.png)

### 1.15 LaneAttributesBike 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119142148993](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119142148993.png)

### 1.16 LaneAttributesSidewalk 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119142208256](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119142208256.png)

### 1.17 LaneAttributesBarrier 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119142226776](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119142226776.png)

### 1.18 LaneAttributesStriping 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119142302256](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119142302256.png)

### 1.19 LaneAttributesTrackedVehicle 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119142321799](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119142321799.png)

### 1.20 LaneAttributesParking 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119142350095](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119142350095.png)

### 1.21 ConnectingLane 字段数据结构说明

该字段被如下接口使用

● 获取多个V2X MAP资源 /v1/{project_id}/nodes

● 获取单个V2X MAP节点信息 /v1/{project_id}/nodes/{global_node_id}

![image-20211119142419671](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119142419671.png)

