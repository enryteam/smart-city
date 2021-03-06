雄安新区数字道路分级标准采购方案

# 一、RSU功能

## 1.1 功能要求

- a) 路侧单元 RSU 负责将从交通信号控制机、应用服务平 台等接收到的实时交通信息播报给相关车辆，同时将 从车载单元 OBU 获取的信息上报应用服务平台。 

- b) 目标识别与通讯：RSU 应具有识别一定范围内通行目 标的能力，具备至少一般通讯和专用通讯两种通讯能 力，能够与车载单元、手持移动终端等建立实时通讯， 具备低延迟接收、发送相关信息的能力。 

- c) 路口信号机信息读取：具有读取路口红绿灯信号信息、 路口渠化信息、信号机机箱动力环境、环境变量等信 息的能力。 

- d) 交通信息、交通指令接收与播报：具有与城市交通相 关部门建立实时通讯的能力，能够将交通管理部门下 发的交通信息、交通指令等发送给车载单元、手持移 动终端等载体。 

- e) 接收车载设备单元 OBU、手持移动终端发送的各类信 息：能够通过无线通信接收到车载设备单元 OBU 发送 来的信息，包括车辆基本信息（车牌号）、坐标位置信 息、机器视觉、车辆乘员信息、驾驶员上报信息等； 能够通过无线通信收到手持移动终端发送的行人坐标 位置信息、行人上报信息等。 

- f) 事故播报与二次事故预防：当通行道路发生交通事故、 自然灾害或其他紧急事件时，RSU 能及时获取事件信 息，并将事件信息发送至特定区域的车辆。RSU 可通 过以下方式获取事件信息：交通管理部门下发事件信 息、事故车辆或目击车辆上报事件信息。

## 1.2 性能要求

- a) 支持 C-V2X PC5（3GPP Rel. 14）直接通信。 

- b) 频段范围：5.905~5.925 GHz。 

- c) 调制方式：C-V2X TDD。 

- d) 传输距离：空旷条件下直线传输距离≥700m。

- e) 数据速率：最大 26Mbps（TX）/26Mbps（RX）。

- f) 支持基于 4GLTE 的 UU 通信，预备好 5G 接入条件。 

- g) 内置 GNSS:GPS/GLONASS/Bei Dou/Galileo/QZSS。 

- h) 支持国标 ITS 全协议栈。 

- i) 支持交通设施接入：包括交通信号灯、毫米波雷达检测器 等。

# 二、微波雷达检测器

## 2.1 功能要求

a) 微波雷达检测器的功能应符合 GA/T 1047―2013《道 路交通信息监测记录设备设置规范》、《交通信息采集 微波交通流检测器》 GB/T 20609―2006 中的要求。 

b) 实现中心对部署的雷达设备的统一管理。通过以太网， 可以对各个雷达安装的参数、道路信息、交通配置信 息进行数据下发。 

c) 中心可通过图形化窗口，实时观测路口车辆动态轨迹 和信息，包含目标 ID，XY 坐标，XY 速度等信息的选 择性查看。 

d) 定时（每 1s）输出车辆排队信息，包含排队车辆数、 排队长度、排队次数等。 

e) 定时（每 125ms）输出断面过车信息。 

f) 虚拟线圈检测功能，可提供基于断面的车辆存在信息。 

g) 交通统计信息，包含车流量、时间占有率、存在检测、 平均速度、85%位速度、车头时距和车间距等数据的 统计分析。 

h) 根据预设的车道，提供车辆排队信息，包含排队长度、 排队车辆数等整体参数，每个车辆的排队时间、停车 次数等个体信息。 

i) 远程配置雷达参数，通过以太网，可以对雷达安装的 参数、道路信息、交通配置信息进行数据下发。 

j) 远程监测雷达运行状态。

## 2.2 性能要求

a) 检测范围：横向≥8 个车道，纵向≥250m（以雷达安装位置 计算）。 

b) 目标数量：最大实时目标数量 100 个。 

c) 数据保存时长：≥30 天。 

d) 设备使用寿命：≥10 年。 

e) 外壳防护等级：IP65，可在雨、雪、大雾、大风、扬尘等 恶劣天气全天候工作。 

f) 排队车辆误差≤20%。 g) 排队长度误差≤20%。 

h) 平均速度误差≤5%。 

i) 车流量误差≤5%。 

j) 占有率误差≤5%。

# 三、激光雷达检测器

## 3.1 功能要求

a) 识别路侧激光雷达所在区域的固定结构，如固定顶杆、 路面、道路边界等。 

b) 识别道路环境中的非固定物体。 

c) 通过目标聚类，对大型车辆、小型车辆、行人、非机 动车或其他障碍物进行分类。 

d) 对目标进行连续跟踪，输出目标的位置、大小、速度、 方向，推算目标轨迹。

## 3.2 性能要求

a) 测距能力：200m（@40%反射率）、100m（@10%反射率）。 

b) 测距精度：±6cm。

 c) 水平扫描视场：360°，水平扫描分辨率：0.1°/0.2°/0.3°/0.4°， 垂直扫描视场：37°（-37~0°），垂直扫描分辨率：0.6~3° 疏密分布，扫描频率：5/10/15/20Hz。 

d) 工作温度：-40~+80℃。