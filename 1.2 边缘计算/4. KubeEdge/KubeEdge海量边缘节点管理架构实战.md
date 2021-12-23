- [KubeEdge海量边缘节点管理架构实战](https://gotc.oschina.net/uploads/files/02%20%E5%BE%90%E9%A3%9E%20KubeEdge%E6%B5%B7%E9%87%8F%E8%BE%B9%E7%BC%98%E8%8A%82%E7%82%B9%E7%AE%A1%E7%90%86%E6%9E%B6%E6%9E%84%E5%AE%9E%E6%88%98.pdf)

徐飞 @fisherxu		KubeEdge Maintainer，华为云高级工程师

## 边缘计算的形态与定义

![image-20211223091345420](https://gitee.com/er-huomeng/img/raw/master/image-20211223091345420.png)

## 关键挑战

• 边缘计算细分领域众多，互操作性差
• 边云通信网络质量低，时延高，且边缘经常位于私有网络，难以实现双向通信
• 边缘资源受限，需要轻量化的组件管理运行边缘应用
• 边缘离线时，需要具备业务自治和本地故障恢复等能力
• 边缘节点高度分散，如何高效管理，降低运维成本
• 如何对异构资源进行标准化管理和灵活配置

## 云原生的核心优势

![image-20211223091430454](https://gitee.com/er-huomeng/img/raw/master/image-20211223091430454.png)

## Kubernetes架构

![image-20211223091455153](https://gitee.com/er-huomeng/img/raw/master/image-20211223091455153.png)

### Kubernetes的扩展API设计——CRD

![image-20211223091510205](https://gitee.com/er-huomeng/img/raw/master/image-20211223091510205.png)

### Kubernetes List-Watch机制

![image-20211223091526871](https://gitee.com/er-huomeng/img/raw/master/image-20211223091526871.png)

## 基于K8s构建边缘计算平台

![image-20211223091539113](https://gitee.com/er-huomeng/img/raw/master/image-20211223091539113.png)

## KubeEdge 架构

![image-20211223091606981](https://gitee.com/er-huomeng/img/raw/master/image-20211223091606981.png)

### KubeEdge核心理念

![image-20211223091632344](https://gitee.com/er-huomeng/img/raw/master/image-20211223091632344.png)

## KubeEdge架构 -- Cloud

![image-20211223091653097](https://gitee.com/er-huomeng/img/raw/master/image-20211223091653097.png)

### 启动一个边缘应用

![image-20211223091705271](https://gitee.com/er-huomeng/img/raw/master/image-20211223091705271.png)

![image-20211223091714282](https://gitee.com/er-huomeng/img/raw/master/image-20211223091714282.png)

• 非侵入实现Pod边缘运行，支持云边混合管理
• 元数据边缘持久化，支持离线自治
• 增量同步，网络消耗平稳

### 海量边缘节点：静态分区+多对主备

![image-20211223091732779](https://gitee.com/er-huomeng/img/raw/master/image-20211223091732779.png)

### 海量边缘节点：多主运行，自动协商

![image-20211223091753760](https://gitee.com/er-huomeng/img/raw/master/image-20211223091753760.png)

## KubeEdge架构 -- Edge

![image-20211223091815245](https://gitee.com/er-huomeng/img/raw/master/image-20211223091815245.png)

## 边缘设备管理

![image-20211223091838217](https://gitee.com/er-huomeng/img/raw/master/image-20211223091838217.png)

## EdgeMesh

![image-20211223091851063](https://gitee.com/er-huomeng/img/raw/master/image-20211223091851063.png)

## Sedna: AI边云协同套件

![image-20211223091905509](https://gitee.com/er-huomeng/img/raw/master/image-20211223091905509.png)

## 生产案例 — 管理世界最长跨海大桥上的所有监控设备

![image-20211223091923834](https://gitee.com/er-huomeng/img/raw/master/image-20211223091923834.png)

## 生产案例 — 中移在线边缘云平台

![image-20211223091945305](https://gitee.com/er-huomeng/img/raw/master/image-20211223091945305.png)

## 生产案例 — 管理中国高速公路上的十万个边缘节点

![image-20211223092002492](https://gitee.com/er-huomeng/img/raw/master/image-20211223092002492.png)