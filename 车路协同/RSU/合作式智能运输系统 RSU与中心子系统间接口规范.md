# 范围

本标准规定了 RSU 与中心子系统间的接口规范，包括业务数据接口和运维管理接口的要求。

本标准适用于 RSU 向中心子系统上报业务和运维数据，以及中心子系统向 RSU 下发配置和管理数据。

# 规范性引用文件

下列文件对于本文件的应用是必不可少的。凡是注日期的引用文件，仅注日期的版本适用于本文件。

凡是不注日期的引用文件，其最新版本（包括所有的修改单）适用于本文件。

T/ITS 0097-2018 合作式智能运输系统 通信架构

YDT 3709-2020 基于 LTE 的车联网无线通信技术 消息层技术要求

# 术语和定义

## 合作式智能运输系统 cooperative intelligent transportation system,C-ITS

通过人、车、路信息交互，实现车辆和基础设施之间、车辆与车辆、车辆与人之间的智能协同与配合的一种智能运输系统体系。

## 中心子系统 central sub-system, CSS

合作式智能运输系统组成部分，包括交通调度、规划、控制等多种设备，负责协调全局和局部区域交通活动。

## 道路子系统 road sub-system, RSS

合作式智能运输系统组成部分, 包括 RSU、道路传感器、道路交通设施、路侧计算设施等多种设备，负责收集、上报路面交通信息，控制交通流并与其他子系统进行通信。

## 危险工况 hazardous Situation

LSAD 系统工作时，自车若不改变行驶路线和车速，将与检测到的障碍物（如骑行人，车辆，行人等）发生碰撞。

## 路侧单元 road side unit, RSU

在道路子系统中，负责车路通信的交通服务逻辑单元。

# 符号和缩略语

C-ITS 合作式智能运输系统(Cooperative Intelligent Transportation System)

CSS 中心子系统(Central Sub-system)

C-V2X 基于蜂窝的车联网(Cellular Vehicle-to-Everything)

RSM 路侧单元消息(Road Side Message)

RSI 路侧单元信息(Road Side Information)

RSS 道路子系统(Road Sub-system)

RSU 路侧单元(Road Side Unit)

SPAT 信号灯消息(Signal Phase and Timing Message)

CSU 中心服务单元(Central Service Unit)

ESU 边缘服务单元(Edge Service Unit)

OBU 车载单元(Onboard Unit)

PSU 个人服务单元(Personal Service Unit)



# 基本要求

## 基本要求总则

为了实现中心子系统对 RSU 的配置、RSU 上报数据的采集和分发，以及对 RSU 的运维管理，中心子系统与 RSU 之间的接口分为业务数据接口和运维管理接口。

业务数据接口定义 RSU 与中心子系统之间的上下行消息的数据格式，主要包括 RSU 信息上报、RSU配置下发、MAP 数据上报和下发、BSM 数据上报、RSM 数据上报和下发、RSI 数据上报和下发，以及 SpaT数据上报和下发。

运维管理接口定义 RSU 上报的信息，以及中心子系统对 RSU 进行重启和远程升级 OTA 等。

## 通信架构

本标准基于《TITS 0098-2017 合作式智能运输系统 通信架构》定义的 C-ITS 系统逻辑框架中心子系统通过车辆子系统和道路子系统汇聚的数据，提供全局或者局部的 ITS 应用服务。道路子系统通过道路安装的各类传感器和设备为车辆和交通管理提供 ITS 应用所需的信息，并根据应用需求，执行相应控制指示。RSU 属于道路子系统中的一类设备，通过 ITS 边界路由器接入网络通信，并由中心子系统对 RSU进行配置和管理。