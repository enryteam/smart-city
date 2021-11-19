- [V2X、OBU、RSU、V2V之间的协作关系](https://blog.csdn.net/u011754972/article/details/116239660)

## 1. V2X、OBU、RSU、V2V 名词术语解释

OBU： On Board Unit 车载单元
RSU： Road Side Unit 路侧单元
V2V： Vehicle to Vehicle 车与车通信
V2X： Vehicle to Everything 车辆到一切通信

## 2. V2X、OBU、RSU、V2V之间的协作关系

假设有两辆智能驾驶汽车A和B

- A车具备：自动驾驶计算平台mdc、V2X设备OBU
- B车具备：自动驾驶计算平台mdc、V2X设备OBU

智能驾驶道路路侧安装有：路测单元RSU(RSU用来发送交通灯、交通标志、和道路上障碍物的数据给OBU)。

路测单元RSU 和 V2X设备OBU也是通过无线电波进行通信。

## 3. 以A车和B车的车路协同、车车协同 为例：

A车mdc中有自动驾驶的各个节点，包括转发obu设备发来的数据的v2x节点。

（1） A车mdc上的v2x节点收到A车OBU通过UDP协议发来的 {1.RSU数据 + 2.B车辆信息}，然后A车mdc上的v2x节点将OBU消息解析后打包成Autosar的AP消息

发送出去供A车mdc自动驾驶的其他节点订阅。

- 数据类型：1.RSU数据 + 2.B车底盘、定位信息 ；
- 数据流向：A车obu --> A车mdc的v2x节点

（2）车mdc上的v2x节点订阅本车的底盘信息和定位信息等，把这些AP消息打包成proto格式，然后封装到udp数据包中，通过UDP协议发送给A车OBU。

- 数据类型：底盘、定位等信息；
- 数据流向：A车mdc的v2x节点–> A车obu 

（3）A车OBU 将A车底盘、定位等信息 通过无线电波发送给 B车OBU，实现A车B车车辆底盘、定位信息共享。 (V2V)

- 数据类型：底盘、定位等信息；
- 数据流向：双向 A车obu <–> B车obu

### 3.1 车车通讯无RSU：![车车通讯无RSU](https://img-blog.csdnimg.cn/2021052710052496.JPG#pic_center)

### 3.2 车车-车路通讯有RSU：![车车-车路通讯有RSU](https://img-blog.csdnimg.cn/20210527100611744.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTE3NTQ5NzI=,size_16,color_FFFFFF,t_70#pic_center)

## 4. 每辆车的OBU的输入与输出

### 4.1 每辆车的OBU接收三部分的输入：

- (1) 路侧单元RSU数据：
  - 接收路侧单元RSU的 交通灯、交通标志、障碍物数据 （无线电波通信）。
- (2) 其他车obu发来的其他车数据：
  -  接收其他车obu数据，获取其他车的车辆底盘、定位灯信息 （无线电波通信）
- (3) 本车mdc的v2x节点发来的本车数据：
  - 接收本车mdc的v2x节点转发的本车底盘和定位信息（udp）

### 4.2 每辆车的OBU会有两路输出：

- (1) 整合前面第一部分输入(RSU数据) 和 第二部分输入(其他车obu发来的其他车数据)，通过udp发送给本车mdc的v2x节点；
- (2) 将前面第三部分输入(本车mdc的v2x发来的本车数据)，通过本车和其他车的OBU 之间的通信，发给其他车OBU ;

【注意】：目前OBU 上的开发，是我们公司其他部门的obu开发人员根据我们的需求进行开发，我目前没有代码工程开发权限，后面会有。我目前拥有的权限是

mdc的v2x开发权限。

其中，本车OBU 发给 本车v2x节点的 (1.RSU数据) 和 (2.其他车底盘定位信息)，会被本车v2x解析为autosar消息后,转发给本车其他节点。

本车v2x节点 会把 本车定位底盘信息 通过UDP转发给 本车OBU。

OBU 发给自车mdc的v2x节点的UDP数据包，通过包头类似 0x88,0x89标识来确认是否使我们想要的数据。

mdc 发给自车OBU 的UDP数据包，通过包头类似 "obuxxx"等做标识来确认是否使我们想要的数据。

## 5. mdc的v2x节点的 输入 与 输出：

### 5.1 mdc的v2x节点的输入：

- mdc的v2x节点有很多输入，包括车辆底盘、定位、odometry、调度、本车OBU 等。
- 其中，本车OBU 接收到其他车的obu数据后，直接和RSU过来的数据一起打包后透传给mdc的v2x节点。

### 5.2 mdc的v2x节点的输出：

- (1) 将本车OBU 发来的数据解析后，封装成Autosar消息，转发给mdc各节点进行订阅；
- (2) 通过udp将本车信息发送给本车obu。