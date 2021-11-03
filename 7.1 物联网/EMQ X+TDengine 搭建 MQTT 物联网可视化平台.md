- [EMQ X+TDengine 搭建 MQTT 物联网可视化平台](https://blog.51cto.com/lhxsoft/3182385?xiangguantuijian&06)



物联网数据采集涉及到大量设备接入、海量的时序数据传输，EMQ X MQTT 服务器 与 TDengine 大数据平台的组合技术栈完全能够胜任场景中的海量时间序列监测数据的传输、存储和计算。

数据入库后，往往需要其他方式如数据可视化系统将数据按照规则统计、展现出来，实现数据的监控、指标统计等业务需求，以便充分发挥数据的价值，TDengine 搭配开源软件 Grafana 可以快速搭建物联网数据可视化平台。

上述整套方案无需代码开发，涉及的产品均能提供开源软件、企业服务、云端 SaaS 服务不同层次的交付模式，能够根据项目需求实现免费版或企业版私有化落地以及云端部署。

## 方案介绍

### EMQ X 简介

EMQ X 是基于高并发的 Erlang/OTP 语言平台开发，支持百万级连接和分布式集群架构，发布订阅模式的开源 MQTT  消息服务器。EMQ X 内置了大量开箱即用的功能，其 开源版 EMQ X Broker 及 企业版 EMQ X  Enterprise 均支持通过规则引擎将设备消息存储到 TDengine。

### TDengine 是什么

TDengine 是涛思数据专为物联网、车联网、工业互联网、IT 运维等设计和优化的大数据平台。除核心的快 10 倍以上的时序数据库功能外，还提供缓存、数据订阅、流式计算等功能，最大程度减少研发和运维的复杂度，且核心代码，包括集群功能全部开源。

TDengine 提供社区版、企业版和云服务版，安装/使用教程详见 TDengine 使用文档。

### Grafana 简介

Grafana 是一个跨平台、开源的度量分析和可视化工具，可以查询处理各类数据源中的数据，进行可视化的展示。它可以快速灵活创建的客户端图表，面板插件有许多不同方式的可视化指标和日志，官方库中具有丰富的仪表盘插件，比如热图、折线图、图表等多种展示方式；支持  Graphite，TDengine、InfluxDB，OpenTSDB，Prometheus，Elasticsearch，CloudWatch和 KairosDB 等数据源，支持数据项独立/混合查询展示；可以创建自定义告警规则并通知到其他消息处理服务或组件中。

## 业务场景

本文模拟物联网环境数据采集场景，假设现有一定数据的环境数据采集点，所有采集点数据均通过 MQTT 协议 传输至采集平台（MQTT Publish），主题设计如下：

```
sensor/data
```

传感器发送的数据格式为 JSON，数据包括传感器采集的温度、湿度、噪声音量、PM10、PM2.5、二氧化硫、二氧化氮、一氧化碳、传感器 ID、区域、采集时间等数据。

```json
{
    "temperature": 30,
    "humidity" : 20,
    "volume": 44.5,
    "PM10": 23,
    "pm25": 61,
    "SO2": 14,
    "NO2": 4,
    "CO": 5,
    "id": "10-c6-1f-1a-1f-47",
    "area": 1,
    "ts": 1596157444170
}
```

现在需要实时存储以便在后续任意时间查看数据，提出以下的需求：

- 每个设备按照每 5 秒钟一次的频率进行数据上报，数据库需存储每条数据以供后续回溯分析；
- 通过可视化系统查看 任意区域、任意时间区间内 的指标数据，如平均值、最大值、最小值。

## 环境准备

本文所用各个组件均有 Docker 镜像，除 EMQ X 需要修改少数配置为了便于操作使用下载安装外，TDengine 与 Grafana 均使用 Docker 搭建。

安装包资源与使用教程参照各自官网：

- EMQ X：EMQ 官网 https://www.emqx.io/cn/
- TDengine：涛思数据官网 https://www.taosdata.com/cn/
- Grafana：Grafana 官网 https://grafana.com/

### 安装 EMQ X

> 如果您是 EMQ X 新手用户，推荐通过 EMQ X 文档 快速上手

访问 EMQ X 下载 页面下载适合您操作系统的安装包，本文截稿时 EMQ X 开源版最新版本为 v4.1.1，下载 zip 包的启动步骤如下 ：

```bash
## 解压下载好的安装包
unzip emqx-macosx-v4.1.1.zip
cd emqx

## 以 console 模式启动 EMQ X 方便调试
./bin/emqx console
```

启动成功后浏览器访问 http://127.0.0.1:18083 访问 EMQ X 管理控制台 Dashboard，使用 admin public 默认用户名密码完成初次登录。

EMQ X 企业版 4.1.2 提供了原生 TDengine 写入插件，性能更好、使用更方便，请移步规则引擎-写入数据到 TDengine查看

### 安装 TDengine

为了方便测试使用通过 Docker 进行安装（需映射网络端口），也可以使用安装包的方式进行安装：

```bash
## 拉取并启动容器
docker run -d --name tdengine -p 6030-6041:6030-6041 tdengine/tdengine:latest

## 启动后检查容器运行状态
docker ps -a
```

### 安装 Grafana

使用以下命令通过 Docker 安装并启动 Grafana：

```bash
docker run -d --name=grafana -p 3000:3000 grafana/grafana
```

启动成功后浏览器访问 http://127.0.0.1:3000 访问 Grafana 可视化面板，使用 admin admin 默认用户名密码完成初次登录，登录后按照提示修改密码使用新密码登录进入主界面：

## 配置 EMQ X 存储数据到 TDengine

### TDengine 创建数据库与数据表

进入TDengine Docker 容器：

```
docker exec -it tdengine bash
```

创建 test 数据库:

```
taos
create database test;
```

创建 sensor_data 表，关于 TDengine 数据结构以及 SQL 命令参见 TAOS SQL：

```sql
use test;
CREATE TABLE sensor_data (
  ts timestamp,
  temperature float,
  humidity float,
  volume float,
  PM10 float,
  pm25 float,
  SO2 float,
  NO2 float,
  CO float,
  sensor_id NCHAR(255), 
  area TINYINT,
  coll_time timestamp
);
```

### 配置 EMQ X 规则引擎

打开 EMQ X Dashboared，进入 规则引擎 -> 规则 页面，点击 创建 按钮进入创建页面。

#### 规则 SQL

规则 SQL 用于 EMQ X 消息以及事件筛选，以下 SQL 表示从 sensor/data 主题筛选出 payload 数据：

```sql
SELECT
  payload
FROM
  "sensor/data"
```

使用 SQL 测试功能 ，输入测试数据进行筛选结果测试，测试有结果且输出内容如下，标明 SQL 编写正确：

```json
{
  "payload": "{\"temperature\":30,\"humidity\":20,\"volume\":44.5,\"PM10\":23,\"pm2.5\":61,\"SO2\":14,\"NO2\":4,\"CO\":5,\"id\":\"10-c6-1f-1a-1f-47\",\"area\":1,\"ts\":1596157444170}"
}
```

![image20200731104046137.png](https://s4.51cto.com/images/blog/202107/23/378f8f99cf390a2f700101a78415b50f.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

#### 响应动作

为支持各种不同类型平台的开发，TDengine 提供符合 REST 设计标准的 API。通过 RESTful Connector 提供了最简单的连接方式，即使用 HTTP 请求携带认证信息与要执行的 SQL 操作 TDengine。

使用 EMQ X 开源版中的 发送到 Web 服务 即可通过 RESTful Connector 写入数据到 TDengine。即将到来的 EMQ X 企业版 4.1.1 版本将提供原生更高性能的写入 Connector。

发送到 Web 服务需要两个数据，一个是关联资源，另一个是消息内容模板。

- 关联资源：HTTP 服务器配置信息，此处为 TDengine 的 RESTful Connector
- 消息内容模板：此处为携带数据的 INSERT SQL，注意我们应当在 SQL 中指定数据库名，字符类型也要用单引号括起来， 消息内容模板为：

```sql
INSERT INTO test.sensor_data VALUES(
  now,
  ${payload.temperature},
  ${payload.humidity},
  ${payload.volume},
  ${payload.PM10},
  ${payload.pm25},
  ${payload.SO2},
  ${payload.NO2},
  ${payload.CO},
  '${payload.id}',
  ${payload.area},
  ${payload.ts}
)
```

![image20200731145609393.png](https://s4.51cto.com/images/blog/202107/23/0d15e01527967e9503accf40c5f8e757.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

#### 创建过程

点击响应动作下的 添加 按钮，在弹出框内选择 发送数据到 Web 服务，点击 新建资源 新建一个 WebHook 资源。

![image20200731104403456.png](https://s4.51cto.com/images/blog/202107/23/3d383eb7c1b2779d1013697fc9a8051a.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

资源类型选择 Webhook，请求 URL 填写 http://127.0.0.1:6041/rest/sql，请求方法选择 POST， 还需添加 Authorization 请求头作为认证信息 。

Authorization 的值为 Basic + TDengine 的 {username}:{password} 经过 Base64  编码之后的字符串, 例如 root:taosdata 编码后实际填入的值为：Basic cm9vdDp0YW9zZGF0YQ==

在响应动作创建页面选择新建的资源，并填入消息模板内容即可。

![image20200804110459517.png](https://s4.51cto.com/images/blog/202107/23/b12c83cbba3fdcb008be8c5e8eb10b93.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

## 生成模拟数据

以下脚本模拟了 10000 个设备在过去 24 小时内、每隔 5 秒钟上报一条模拟数据并发送到 EMQ X 的场景。

- 总数据量： 24 * 3600 / 5 * 100 = 172 万条
- 消息 TPS： 20

读者安装 Node.js ，按需修改配置参数后可以通过以下命令启动：

```js
npm install mqtt mockjs --save --registry=https://registry.npm.taobao.org
node mock.js
```

附：模拟生成数据并发送到 EMQ X 代码，请根据集群性能调整相关参数

```js
// mock.js
const mqtt = require('mqtt')
const Mock = require('mockjs')

const EMQX_SERVER = 'mqtt://localhost:1883'
const CLIENT_NUM = 100
const STEP = 5000 // 模拟采集时间间隔 ms
const AWAIT = 5000 // 每次发送完后休眠时间，防止消息速率过快 ms
const CLIENT_POOL = []

startMock()


function sleep(timer = 100) {
  return new Promise(resolve => {
    setTimeout(resolve, timer)
  })
}

async function startMock() {
  const now = Date.now()
  for (let i = 0; i < CLIENT_NUM; i++) {
    const client = await createClient(`mock_client_${i}`)
    CLIENT_POOL.push(client)
  }
  // last 24h every 5s
  const last = 24 * 3600 * 1000
  for (let ts = now - last; ts <= now; ts += STEP) {
    for (const client of CLIENT_POOL) {
      const mockData = generateMockData()
      const data = {
        ...mockData,
        id: client.options.clientId,
        ts,
      }
      client.publish('sensor/data', JSON.stringify(data))
    }
    const dateStr = new Date(ts).toLocaleTimeString()
    console.log(`${dateStr} send success.`)
    await sleep(AWAIT)
  }
  console.log(`Done, use ${(Date.now() - now) / 1000}s`)
}

/**
 * Init a virtual mqtt client
 * @param {string} clientId ClientID
 */
function createClient(clientId) {
  return new Promise((resolve, reject) 
```